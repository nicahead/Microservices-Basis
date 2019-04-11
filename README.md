# Microservices-Basis
Spring Cloud微服务开发基础框架

### 0.统一的依赖管理-ctFire-dependencies
Spring Cloud 项目都是基于 Spring Boot 进行开发，并且都是使用 Maven 做项目管理工具。在实际开发中，我们一般都会创建一个依赖管理项目作为 Maven 的 Parent 项目使用，这样做可以极大的方便我们对 Jar 包版本的统一管理。
在实际开发中，我们所有的项目都会依赖这个 dependencies 项目，整个项目周期中的所有第三方依赖的版本也都由该项目进行管理。

### 1.服务注册与发现-ctFire-eureka
我们使用的组件是 Spring Cloud Netflix 的 Eureka，Eureka 是一个服务注册和发现模块
Eureka 是一个高可用的组件，它没有后端缓存，每一个实例注册之后需要向注册中心发送心跳（因此可以在内存中完成），在默认情况下 Erureka Server 也是一个 Eureka Client ,必须要指定一个 Server。

### 2.分布式配置中心-ctFire-config
在分布式系统中，由于服务数量巨多，为了方便服务配置文件统一管理，实时更新，所以需要分布式配置中心组件。在 Spring Cloud 中，有分布式配置中心组件 Spring Cloud Config ，它支持配置服务放在配置服务的内存中（即本地），也支持放在远程 Git 仓库中。在 Spring Cloud Config 组件中，分两个角色，一是 Config Server，二是 Config Client。

### 3.服务监控-ctFire-admin
随着开发周期的推移，项目会不断变大，切分出的服务也会越来越多，这时一个个的微服务构成了错综复杂的系统。对于各个微服务系统的健康状态、会话数量、并发数、服务资源、延迟等度量信息的收集就成为了一个挑战。Spring Boot Admin 应运而生，它正式基于这些需求开发出的一套功能强大的监控管理系统。

### 4.服务链路追踪-ctFire-zipkin
ZipKin 是一个开放源代码的分布式跟踪系统，由 Twitter 公司开源，它致力于收集服务的定时数据，以解决微服务架构中的延迟问题，包括数据的收集、存储、查找和展现。
每个服务向 ZipKin 报告计时数据，ZipKin 会根据调用关系通过 ZipKin UI 生成依赖关系图，显示了多少跟踪请求通过每个服务，该系统让开发者可通过一个 Web 前端轻松的收集和分析数据，例如用户每次请求服务的处理时间等，可方便的监测系统中存在的瓶颈。

### 5.路由网关统一访问接口-ctFire-zuul
在 Spring Cloud 微服务系统中，一种常见的负载均衡方式是，客户端的请求首先经过负载均衡（Zuul、Ngnix），再到达服务网关（Zuul 集群），然后再到具体的服。服务统一注册到高可用的服务注册中心集群，服务的所有的配置文件由配置服务管理，配置服务的配置文件放在 GIT 仓库，方便开发人员随时改配置。
Zuul 的主要功能是路由转发和过滤器。路由功能是微服务的一部分，比如 /api/user 转发到到 User 服务，/api/shop 转发到到 Shop 服务。Zuul 默认和 Ribbon 结合实现了负载均衡的功能。
