# vagrant + consul 本地集群封装服务

> 2017 / 07／31

> 在软件基础设施越来越活跃的环境中，与其他服务及其环境的服务的动态沟通越来越重要。

> 使用REST在服务之间进行通信基本上是一个没有意义的事情，但是使用REST API定位服务或替换配置文件并不是一个决定。 当然，使用GoDaddy GUI将域名连接到IP，或者在几十个服务器上维护配置文件似乎也不是正确的。

> 诸如Consul和Confd等新兴解决方案有助于解决这个问题。 consul采取一种方法，提供REST API的灵活性以及DNS（自定义DNS服务器）的可移植性。 Confd利用由Consul维护的集中式键/值存储库来公开一个静态配置（动态更新）。

> 两者的快速入门指南是相当稳固的，所以我不会做一个设置教程。 相反，我会给你一个工作集群的旅程，并指导你如何做一些常见的事情。 要遵循这一切，您需要在Vagrant中运行6个节点示例环境

看看 [Vagrantfile](https://github.com/javady/vagrantFiles/blob/master/consul-cluster-vagrant/Vagrantfile) 可以帮助我们构建正在做的哪些事情：
* 2 consul server agents
* 1 consul agent hosting a “status” web gui
* 2 example service nodes
* 1 demo web-app that will interact with the service
```
  $ git clone git@github.com:benschw/consul-cluster-vagrant.git
  $ cd consul-cluster-vagrant
  $ vagrant up
```
#### 笔记

* 每个节点都连线使用256mb RAM，所以这个集群在大多数系统上应该运行正常。 我的i7 / 8gb笔记本电脑的负载为1。

### Status Web UI
* 去看看：http://172.20.20.12:8500/ui （vagrant集群明确定义你的ips，所以你可以按照这个链接。）
您可以查看所有已注册的服务，并且您的服务的节点实例正在运行，或者转到“节点”选项卡，并查看每个运行服务的节点列表。 还有健康检查状态和键/值选项卡，稍后我们将讨论CLI工具

* 要尝试使用cli工具，您需要到达其中一个集群节点。 从那里你可以找到更多关于发生的事情

  ```
    $ vagrant ssh demo
    $ consul members
    demo      172.20.20.15:8301  alive  role=node,dc=dc1,vsn=1,vsn_min=1,vsn_max=1
    status    172.20.20.12:8301  alive  role=node,dc=dc1,vsn=1,vsn_min=1,vsn_max=1
    consul1   172.20.20.10:8301  alive  role=consul,dc=dc1,vsn=1,vsn_min=1,vsn_max=1,port=8300,bootstrap=1
    consul2   172.20.20.11:8301  alive  role=consul,dc=dc1,vsn=1,vsn_min=1,vsn_max=1,port=8300
    service2  172.20.20.14:8301  alive  role=node,dc=dc1,vsn=1,vsn_min=1,vsn_max=1
    service1  172.20.20.13:8301  alive  role=node,dc=dc1,vsn=1,vsn_min=1,vsn_max=1
  ```

* 你也可以这样查看:
  * consul info - some general info about your cluster
  * consul monitor - stream log output
  * the documentation…
  
REST API

You can do everything through the REST API. Including managing your cluster, registering services, working with key/values… everything.
$ vagrant ssh demo
$ curl http://localhost:8500/v1/catalog/service/my-svc
[{"Node":"service2","Address":"172.20.20.14","ServiceID":"my-svc","ServiceName":"my-svc","ServiceTags":["microservice"],"ServicePort":8076},{"Node":"service1","Address":"172.20.20.13","ServiceID":"my-svc","ServiceName":"my-svc","ServiceTags":["microservice"],"ServicePort":8045}]
Again, the documentation is good.
DNS

One of the most powerful features of consul, is its custom DNS server. If you want to keep your application decoupled from consul, then you probably don’t want to leverage the REST API. That’s what DNS is for.
$ vagrant ssh demo
$ dig @127.0.0.1 -p 8600 my-svc.service.consul SRV
...

;; ANSWER SECTION:
my-svc.service.consul.  0       IN      SRV     1 1 8076 service2.node.dc1.consul.
my-svc.service.consul.  0       IN      SRV     1 1 8045 service1.node.dc1.consul.

;; ADDITIONAL SECTION:
service2.node.dc1.consul. 0     IN      A       172.20.20.14
service1.node.dc1.consul. 0     IN      A       172.20.20.13

...
Cool, right?
Just remember that its running on a custom port and not wired against your resolv.conf by default, so you will need to manually resolve the address. The demo app/service referenced in this example contains a simple load balancer prototype for working with consul’s SRV records.
Note that we need the SRV records and not just the A records because the SRV entries also have the port our service is running on
Give Confd something to work with

You may have noticed that our service endpoint (http://172.20.20.13:8045/foo) is reporting that Foo = "<no value>". This is because although we wired up confd to sync a key from consul to our local config (in the Vagrantfile,) we never actually added a key to consul.
Here are two methods to set Foo to some value:
1. Navigate to http://172.20.20.12:8500/ui/#/dc1/kv/ and create the key foo.
2. Use the REST API
 $ vagrant ssh demo
 $ curl -X PUT -d 'bar' http://localhost:8500/v1/kv/foo
Confd listens for changes to designated keys in consul and runs them through a template to produce your config file.
Our Demo Webapp

Included in our cluster example is a demo webapp and service named “demo.” Rather then have a separate service app and ui app, I just baked all functions into one application for simplicity. Here are the available urls:
* http://172.20.20.13:8045/status A url for consul to curl to validate that the service is healthy. Both applications use this.
* http://172.20.20.13:8045/foo A REST resource that exposes information about the “my-svc” service (its host name and a value from a config maintained by confd.)
* http://172.20.20.15/demo The web ui: this will use consul to discover “my-svc”, make a request to my-svc/foo, and then emit what it has found to the screen.
If you want to dig around in the demo app, or add to it, here’s the src
Fail a Health Check

Lets see how consul protects us when one of our services starts misbehaving. The demo app exposes a statusendpoint that will emit “OK” when the service is healthy, and something else when it is not. Rather then actually testing health, this endpoint is configured to look for the existance of the file /tmp/fail-healthcheck and if it exists, start emitting “FAIL” instead of “OK”.
Before we induce the failure, run through this punch list to see what a healthy cluster looks like. Since we will be failing the instance of “my-svc” running on “svc1”, keep an eye on that.
* Verify that all checks are passing: http://172.20.20.12:8500/ui
* Verify that our status endpoint is currently “OK”: http://172.20.20.13:8045/status
* Watch the webapp load balance randomly between our two instances: http://172.20.20.15/demo (click refresh a bunch)
* See what the healthy DNS for “my-svc” looks like:
  $ ssh vagrant svc1
  $ dig @127.0.0.1 -p 8600 my-svc.service.consul SRV
OK! Now lets make “my-svc” fail on “svc1”:
$ vagrant ssh svc1
$ touch /tmp/fail-healthcheck
Run back through the punch list to see how everything changed. We’ve got “critical’s” in our status ui, “FAIL” in our endpoint, the demo app is only using “svc2” now, and we can see why by inspecting DNS.
You can go ahead and rm /tmp/fail-healthcheck and everything will be right in the world again.
Why’d we exit 2?

If you paid attention to the consul config for “svc1,” you might have noticed that our health check is exiting with a 2instead of the more traditional 1. This is another pretty cool feature of consul.
curl localhost:8045/status | grep OK || exit 2
Consul uses nagios style checks for its health checks. This meens that exiting with a 0 means everything is passing. Exiting with a 1 is just a warning: things will turn red, but the service will not be taken out of load balance. Exit with anything greater than 1 will result in a “critical” state and the service will not be returned in a DNS lookup etc.
Why is this cool? Lots of monitoring solutions are using this style of check these days, so you can use the same checks for all of them.
Wrapping up

Thanks for walking through my demo! If you just read through it but didn’t run your own cluster, you really should!
One last thing to do with your cluster

Technically speaking, although we needed the -bootstrap flag for the consul1 node when we started the cluster, we don’t need it anymore (and if we ever needed to restart it, we would need to get rid of it.) So to be a little more production like, you can do the following to kill that consul agent and then restart it, re-joining via consul2:
$ vagrant ssh consul1
$ sudo killall daemon
$ sudo daemon -X "consul agent -server -data-dir /tmp/consul -node=consul1 -bind 172.20.20.10 -join 172.20.20.11"
