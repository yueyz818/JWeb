# `JWeb`：一个完整的大型网站后端，基于微服务，详述整个搭建历程
有幸从头开始搭建一个大型网站，但基于太多的不确定以及技术上的不足，
这里先做一个 Demo，算作**实战演练**，后续也会进行**性能压测**，不 “空口无凭”。
<br/>
致力于实现“三高”，关于网站搭建的技术问题也会补充完善，尽快成长！

<font color='blue'>场景模拟：</font>

**用户购买商品**：

1. 获取商品价格；
2. 生成订单；
3. 用户支付成功；
4. 商品数量减少；
5. 流程结束。

<br/>

## 服务
服务分为：
- 业务服务：
  - 基础服务：用户服务（`Q-User`），订单服务（`Q-Order`），商品服务（`Q-Goods`）；
  - 接口服务：rest接口服务（`Q-Rest`）
- 服务治理服务：服务发现与注册服务（`Q-EurekaServer`），路由服务（暂无）
- 系统服务：暂无

<br/>



## 部署

1. docker 部署：参考 *文档* 文件夹中的 *docker部署*； 

<br/>

## 性能压测历程

**`JMeter` 测试计划会放在项目`测试计划`目录里，按标签进行的命名**；



日期：2020-04-17，`tag：v1.0`，完成功能：基础服务业务逻辑完成，使用 `EurekaDiscoveryClient` 帮助完成远程服务调用；

1. 环境：Docker 搭的服务，使用的全部是默认配置，查了下虚拟机的堆大小：`492MB`
2. 测试：单个用户购买某个商品一个，50 个线程执行20 次，共1000个请求，由于所有的都在我自己的电脑上运行，所以最终的 `TPS=2.18`，有些请求的执行时间高达了快八九秒，最终数据也有一点问题，现在装有 `Docker` 的虚拟机已经卡死了，所以，在一台电脑上进行测试，还请慎重！
3. 优化：还是需要结合硬件来看
   - 优化 `Eureka` 参数（主要是优化线程数）：
   - 使用 `Ribbon` ，每个基础服务都新增一个；
   
   > 关于优化的后续，暂时未给出，这是因为我无法在一台电脑上验证我的优化是否生效...
