## YH 工作日志

1. logstash @timestamp 时区问题

2. springcloud的服务列表改造 并 提供拉取api

   > @浮华 应用列表/接口列表
   >
   > http/dubbo

3. 提供Pod重启 扩容 缩容 api (追@牟良 )

4. 资源依赖 , TOPN , 实例的负载均衡（参考@张超  http://skywalking.yonghuivip.com/#/monitor/service

5.  



本周事项：

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

   

3. 日志收集 @牟良

4. 服务列表

5. 日志区分容器/vm   @changyuli

6. 

7. 