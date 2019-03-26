## 	YH 工作日志

1. y5ozFhxR

2. logstash @timestamp 时区问题

3. springcloud的服务列表改造 并 提供拉取api

   > @浮华 应用列表/接口列表
   >
   > http/dubbo

4. 提供Pod重启 扩容 缩容 api (追@牟良 )

5. ~~资源依赖 , TOPN , 实例的负载均衡（参考@张超  http://skywalking.yonghuivip.com/#/monitor/service~~

6. 参考下/flow/ajax_overflow_utf8.jsp 对于指定 限流框架的异常 指定一个输出资源 b2c-platform发布一个优化

7. springcloud 接口列表 resturn type待优化

8. 



##### 2019 第13周工作笔记： 服务治理平台接口详细梳理

1. /v1/service_governance/services 应⽤列表-查询
1. /v1/sentinel/monitor/http/history 接⼝流控监控-历史查询
1. /v1/sentinel/monitor/dubbo/history
1. /v1/interface_monitor/flow/dubbo 接⼝流控，熔断监控指标-实时查询
1. /v1/interface_monitor/flow/http

##### 2019 第12周工作笔记：服务治理平台接口详细梳理

1. > ? 无法根据feature来看限流日志
   >
   > ? 日志是根据rn聚合的（不能区分feature）

1. ~~dubbo 服务列表注册到zk中，缺少清理~~

1. ~~服务列表（怎么表示）~~

1. 服务监控/实例管理数据在哪

1. 接口监控详解

1. 流控

   > todo 无法配置应用级别开关（流控/日志）
   >
   > todo 无法按应用展示流控规则
   >
   > todo 无手动添加页面

1. 接口实现

   1. /v1/service_governance/rest/services 获取所有应用列表
   1. /v1/service_governance/dubbo/services 获取所有应用列表
   1. 
   1. /v1/service_governance/dubbo/interfaces  Dubbo接⼝列表-查询
   1. /v1/service_governance/rest/interfaces 
   1. 
   1. /v1/service_governance/dubbo/interfaces/{servicesName} Dubbo接⼝列表-应⽤级别查询
   1. /v1/service_governance/rest/interfaces/{servicesName} 
   1. 
   1. /v1/sentinel_rules/check/dubbo 接⼝流控配置-查询是否存在配置
   1. /v1/sentinel_rules/check/http
   1. /v1/sentinel_rules/new/dubbo 接⼝流控配置-新增
   1. /v1/sentinel_rules/new/http
   1. /v1/sentinel_rules/update/duboo 接⼝流控配置-更新
   1. /v1/sentinel_rules/update/http
   1. /v1/sentinel_rules/get/dubbo 接⼝流控配置-查询
   1. /v1/sentinel_rules/get/http
   1. /v1/sentinel_rules/delete/dubbo 接⼝流控配置-删除
   1. /v1/sentinel_rules/delete/http
   1. /v1/sentinel_rules/{applicationName}/config 获取应用的限流配置（限流开关/日志开关）
   1. /v1/sentinel/monitor/http 接⼝流控监控-实时查询
   1. /v1/sentinel/monitor/dubbo



##### 2019 第11周工作笔记：

1. ~~skywalking 接口测试~~

2. ~~服务体验接口封装~~

   ```
   /v1/service_check/services
   /v1/service_check/services/{serviceId}/instance_throughput
   /v1/service_check/services/{serviceId}/topology
   /v1/service_check/services/{serviceId}/rt
   /v1/service_check/services/{serviceId}/slow_end_point
   请求参数中请携带start/end时间参数
   http://192.168.20.237:9300/v1/service_check/services/1441/instance_throughput?start=2019-03-13 16:35&end=2019-03-13 16:50
   ```

   

3. dubbo服务列表

   1. ~~优化服务列表在zk中的数据结构~~
   1. RESTFul uri



#####2019 第10周工作笔记：

1. ~~日志中环境问题~~
2. ~~http异步Client~~，可深入学习下[实现原理](https://hc.apache.org/httpcomponents-core-ga/tutorial/html/index.html)
3. ~~ES 集群模式~~
4. ~~联合测试@卢乾坤开发@李靖春调低限流阀值~~
5. Pod重启 扩容 缩容 api (追@牟良 )
6. 

#####2019 第9周事项：

1. ~~上线确认 @李靖春~~

2. ~~限流规则生成 @李靖春~~

   sentinel_rules/partner-center/config:

   ```
   {
       "flow": true,
       "logOnlyWhenBlocked": true
   }
   ```

   sentinel_rules/partner-center/flow:

   ```
   [
       {
           "resource": "com.yonghui.partner.api.PartnerService:findPartner(long,long,java.lang.String,com.yonghui.partner.api.model.developing.AddressInfo)",
           "count": 1000000
       },
       {
           "resource": "com.yonghui.partner.api.PartnerService:findPartner(long,long)",
           "count": 1000000
       },
       {
           "resource": "com.yonghui.partner.api.PartnerService:getOrder(long)",
           "count": 1000000
       },
       {
           "resource": "com.yonghui.partner.api.PartnerService:getCountOfDeliveryOrder(java.lang.Integer,com.yonghui.partner.api.model.order.PartnerOrderStatus)",
           "count": 1000000
       }
   ]
   ```

   

3. ~~日志收集 @牟良~~

4. 服务列表

5. 日志区分容器/vm   @changyuli


####本地环境搭建

vm1/vm2

cd /usr/local/spring-cloud-provider;/usr/local/jdk/bin/java -Xms32m -Xmx32m -Dcsp.sentinel.log.dir=/usr/local/spring-cloud-provider/logs -jar spring-cloud-provider.jar &>/dev/null &