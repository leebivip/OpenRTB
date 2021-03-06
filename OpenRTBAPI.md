
``# OpenRTB_API_Specification中文版(V2.3.1)

#名词解释
**IAB:** Interactive Advertising Bureau 交互式广告局。

# 前言
## 简介

RTP工程， 前身为OpenRTB组织， 在2010年11月份组建。致力于为数字媒体自动化交易开发一套全新的开放标准，以应对更大范围的平台，设备以及广告解决方案。本文档就是RTB工程努力的结晶，你可以在[www.iab.net](www.iab.net)找到最新的官方文档。

## 关于IAB的广告网络和交易协会

IAB 广告网络和交易协会主要由广告网络和广告交易平台成员公司的高层领导组成。该协会致力于促进当今世界日益复杂的广告市场中数字生态系统的利益。协会目标是促进完成在广告商，发布者，中间商，代理协会之间专业性和责任心的最高标准， 开发能够保证收入增长的程序以及创建保护消费者和行业的最佳实践。

RTB工程是IAB广告科技理事会下的一个工作小组。

## IAB 联系方式
Melissa Gallo
产品总监 – 数据和程序自动化, IAB 科学实验室
[melissa@iab.net](melissa@iab.net)

## 许可证

OpenRTB 规范是在[Creative Commons Attribution 3.0 License](https://creativecommons.org/licenses/by/3.0/)许可之下，基于[http://openrtb.info](http://openrtb.info)的工作。 在该许可证之外的权限你可以在[http://openrtb.info](http://openrtb.info)找到。如果要查看该许可证的副本， 可以访问[https://creativecommons.org/licenses/by/3.0/](https://creativecommons.org/licenses/by/3.0/)或者写信给Creative Commons, 171 Second Street, Suite 300, San Francisco, CA 94105, USA.

# 新手入门

本规范包含了实时竞价接口的详细解释。以下相关解释中多处涉及“对象”这个概念， 所以这里提前说明以下：并不是所有的对象都是必须的，每个对象可能包含多个可选的属性参数。为了帮助第一次接触本文档的读者，我们已经在文档中标注了不同场景下（比如banner, video等等）要完成一个最小可行的实时竞价接口，哪些参数是不可缺少的以及哪些属性是可忽略的。

最小可行接口应该包括标识有**required**以及**recommended**的参数，但是这些参数的作用范围与其特定的使用场景相关。在这些场景的参数描述表中， [Description] 列可能会进一步的标识及注解参数的**required**或者**recommended**状态。为了尽可能填充对象， 可选参数也是可以被填充的，这都取决于该行为的参与者（对象填充者）。

下表展示了不同修饰符的作用：
* 带有**required**为必须参数，带有**recommended**的选项是推荐参数，其余的（带有**default**修饰符或者什么都不带）则是可选参数。
* 按照习惯，通常会按照 **required-->recommended->default->none** 的顺序防止参数。

| Attribute | Type | Description |
| --- |---| ---|
|id|string;**required**|...|
|site|object;**recommended**|...|
|test|integer;**default** 0|...|
|tmax|integer|...|

> 注意： 由于**recommended**属性不是必须的， 所以并不是从每个数据源都可以获取到的。 所以建议所有的OpenRTB事务参与者完成下页中的集成清单来标识供应方在竞价请求中支持，哪些属性是需求方需要用来做广告决策的。

# 集成清单列表

![](https://raw.githubusercontent.com/leeowenowen/OpenRTB_API_Specification-/master/res/integration_checklist.png)
# 1. 介绍
## 1.1 目标/概览
OpenRtb工程的任务是为广告买家和广告位库存买家之间的通信提供开放的工业标准，以刺激实时竞价市场的增长。标准涉及到很多方面，包括但不限于实时竞价协议，信息分类，离线配置同步以及其他很多。

本文档为从早期”block list"项目和"OpenRTB Mobile"项目发展而来的实时竞价接口规范标准。这些标准旨在简化广告媒体库存的提供商（例如，广告交易， 代表发布商利益的广告网络， 卖方平台） 与其有竞争力的买家（例如，竞价者， 需求方平台以及代表广告商利益的广告网络）之间的关系。

![](https://raw.githubusercontent.com/leeowenowen/OpenRTB_API_Specification-/master/res/openrtb_ecosystem.png)

OpenRTB总的目标是为买家和卖家之间的沟通创造一种通用语言，这种倾向不是精确的规定每个交易的操作。 作为一个工程， 我们的目标是让参与的各方可以更容易的集成， 从而促进生态系统中交易的各方都能够进行更深层次的创新。

## 1.2 OpenRTB的历史
OpenRTB于2010年的11月份在三个需求方平台（DataXu, MediaMath和Turn）以及三个卖方平台（Admeld, PubMatic以及The Rubicon Project)上作为试点项目启动的。 第一个目标是使交易block lists各方的沟通标准化。OpenRTB 1.0 block list规范在2010年的12月发布。

在得到了业界普遍的正面响应之后， Nexage 介入 OpenRTB工程，并建议在实时竞价请求和响应协议上为OpenRTB创建API规范，尤其是为支持手机移动广告。 移动小组委员会在买方公司（DataXu, Fiksu以及[X+1]和卖方公司(Nexage, Pubmatic, Smaato以及Jumptap)之间形成了。这个项目促成了OpenRTB Mobile 1.0标准， 该标准在2011年2月发布。

随着移动规范的发布， 在与DataXu和ContextWeb协作的视频广告交易（BrightRoll以及Adap.tv)中，一个视频小组委员会也形成了，其目标在于合作支持将普通展示型广告，视频广告以及移动广告规范在一个文档中。这个努力最终促成了一个统一的标准-OpenRTB2.0,在2011年6月发布。

由于业界的广泛采纳， 随着OpenRTB在2012年1月2.1版本的发布，它被采纳为美国互动广告局（Interactive Advertising Bureau）的一项标准。

## 1.3 版本历史
**OpenRTB 实时竞价API**

 - 2.3 支持原生广告以及多个微小改动
 - 2.2 为私有市场直接交易，视频，移动广告以及regulatory signals做出的一些新的改动
 - 2.1 按照QAG规范进行一些修正，一些小的改动以及错误修正。
 - 2.0 将展示广告，移动广告以及视频广告标准归一到一个统一的标准
 - 1.0 OpenRTB 移动版的最初发布版

**OpenRTB 展示 Block List分支**

 - 1.2 发布商API
 - 1.1 为包含creative attributes的实时交易进行小改动
 - 1.0 OpenRTB block list规范的最初发布。


## 1.4 资源
 - OpenRTB Google Groups: [http://openrtb.info](http://openrtb.info)
 - OpenRTB Github 地址 [http://github.com/openrtb/OpenRTB](http://github.com/openrtb/OpenRTB)
 - 开发者社区邮件列表 [http://groups.google.com/group/openrtb-dev](http://groups.google.com/group/openrtb-dev)
 - 用户社区邮件列表 [http://groups.google.com/group/openrtb-user](http://groups.google.com/group/openrtb-user)

## 1.5 术语
| 术语 | 解释 |
| --- |---|
| RTB |实时竞价 Real-Time Bidding|
| Exchange | 为一次展现管理不同竞价者之间的竞拍行为的服务 |
| Bidder | 在实时竞拍中为获取一次展示参与竞价的实体 |
| Seat | 期望获取展示并使用竞拍者代表他们进行竞拍的实体 |
| Publisher | 操作一个或者多个网站的实体 |
| Site | 如果没有特殊说明，指的是一个支持广告内容的网页或者应用 |
| Deal ID | 标识在特定场景下Publisher与Seat之间预先安排用于购买展示的协议 |

# 2. OpenRTB 基础知识

下图展示了广告交易平台和它的竞拍者之间的交互行为。
广告请求首先从发布者的站点发起。
对于每一个请求，广告交易平台都会向多个竞拍者广播竞价请求，从竞拍者返回的竞拍响应信息会按照常用的竞拍规则进行决策，获胜者会被通知， 广告审定结果被返回。获胜通知地址以及广告审定结果可能包含任何标准宏以保证广告交易平台能够与竞拍者之间沟通竞拍相关的关键数据。

![](https://raw.githubusercontent.com/leeowenowen/OpenRTB_API_Specification-/master/res/rtb_sequence.png)

注意对于通知是否会丢失并没有显式规定。 这是由于该操作会消耗一定的系统性能和带宽。建议广告交易平台在请求/响应协议之外通过离线或者独立的处理流程来提供丢失的竞拍数据信息。

本规范专注于实时竞价交互中的竞价请求和响应以及胜出通知及其响应。其他的交互（比如阻塞列表同步， 流量控制）要么是未来执行的可选行为，要么是已经被OpenRTB定义的。

## 2.1 数据传输

交易平台和它的竞拍者之间的基础通讯协议是HTTP. 特别要说明的是，在发起竞价请求的时候需要使用HTTP POST方式，因为它比HTTP GET可以附带更多的内容，并且也更容易支持二进制数据。 胜出通知则可以使用HTTP POST 或者 GET, 这个是由交易平台决定的。除了空的竞价响应应当返回HTTP 204之外， 所有的调用都应当返回HTTP 200（例如，推荐的方式是在响应体中指明"no bid"), 

> **最佳实践:** 一种最简单和最有效的提高连接性能的方式是启用HTTP长连接， 也就是我们通常说的Keep-Alive. 通过减少两端的连接管理以及CPU使用， 对整个过程会有明显的性能提升。

## 2.2 安全性

SSL(Secure Socket Layer) 不是必须的， 因为这些调用都是服务器之间的调用， 可以用其他方式对数据的安全进行保护。除此之外， SSL 不被推荐使用也由于它额外的处理负载。

## 2.3 数据格式

JSON(Javascript Object Notation) 是竞价请求和响应的推荐数据格式。 JSON被选择是因为它的可读性以及紧凑性。数据负载的相关信息我们会在第3节和第4节详细描述。

交易平台可能需要提供额外的内容信息给有需要的竞价者。这些内容可能包括一个JSON, XML, Apache Avro, ProtoBuf, Thrift以及其他种类的格式的压缩形式。

竞价请求需要使用HTTP的Content-Type头在mime-type中指明内容的类型。标准JSON类型的mime-type是"application/json". 竞价响应的数据格式必须跟竞价请求相同。
···
 Content-Type: application/json
···

如果要使用其他可选的二进制类型， 交易平台或者SSP应当适当的指明Content-Type, 例如"Content-Type: avro/binary" 或者 "Content-Type:application/x-protobuf", 如果没有content-type头， 竞拍者应当认为类型是"application/json", 除非交易平台选择了另一种不同的默认类型。

作为约定，某个属性的确实有其确定的意义，大多数情况下，这标识该属性值是未知的，除非被特殊指明。

## 2.4 OpenRTB 版本号 HTTP 头

OpenRTB版本号应当在竞价请求的头中使用自定义头传递。这可以让竞价者在解析请求体之前判断消息的版本号。
此外，建议竞价者在响应头中使用相同的格式信息标识自己实现的协议版本，这个版本号可能与请求头中的版本号是不同的。

```
 x-openrtb-version: 2.3
```
版本号应当以 <主版本号>.<次版本号>的格式（例如， 2.3). 第一位或者第二位数字的变动标识着协议的改变。通常，第二位版本的改变应当向兼容，第一位版本的改动不需要向后兼容。任何第三位版本号的改动（例如2.0.1)都不应当改变协议自身， 而仅仅改变不影响协议内容的描述和注释。第三位的版本号不应当在HTTP头中包含，因为他们对整个实现不会有技术上的影响。

## 2.5 隐私设计

OpenRTB工程支持广告中卖方和买方之间的隐私策略。特别是OpenRTB支持 do-not-track(3.2.11节）， COPPA restriction signaling(7.1节）， 以及从卖方向买房通过User　Object传递用户数据（3.2.13节）的能力。

## 2.6 与 IAB 质量保证指南 之间的关系

OpenRTB与IAP的质量保证指南（QAG)完全兼容， 你可以在这里找到[http://www.iab.net/ne_guidelines](http://www.iab.net/ne_guidelines). 特别是本文档中的分类标准是从QAG继承而来。

## 2.7 定制与扩展

OpenRTB规范允许交易病态对其进行定制和扩展。每一个对象都可以包含扩展。为了保证扩展字段的一致性，扩展字段应当始终使用"ext"命名。

# 3. 竞价请求规范

RTB 事务在交易平台或者其他广告提供源向竞价者发起竞价请求是被发起。竞价请求由顶级请求对象组成，至少一个展示对象， 以及可能有选择性的包含一些其他的对象用于提供展示相关的上下文信息。

## 3.1 对象模型。

下图展示了竞价请求的对象模型。顶级对象（例如， 在JSON中没有命名的最外层对象）在这个模型中是表示`BidRequest`的。在它的直属子对象中，只有`Imp`是技术上必须的，因为它是描述一次展示的基础信息，必须使用`Banner`, `Video`以及`Native`中的至少一个来定义展示的类型（例如， 无论一个或者多个展示者想要接收；尽管一次竞价是这些指明类型中的明确的一种）。一个展示对象可能包含一组私有市场。

![](https://raw.githubusercontent.com/leeowenowen/OpenRTB_API_Specification-/master/res/bid_request_object_model.png)

竞价请求的其他直属子对象用于为竞价者的用户定向及广告定价提供多种形式的辅助信息。这包括用户的详细信息以及他们使用的设备，位置信息，监管约束条件以及广告的展示载体。

对于后者，在站点（即web站点）以及应用（即手机中安装的非浏览器应用）有一个区别。抽象类`DistributionChannel` 仅仅是一个模型上的抽象， 用于表明一个`BidRequest`与一个`Site`或者`App`相关联，但不会同时与他们关联（即一个发布渠道是一个抽象的站点或者一个应用). 站点和应用都可以被更进一步的描述， 比如他们的发布者， 内容，内容产生者。

上图中没有展示的是扩展对象。这是一个未定义的但是可以附加到任意其他对象中用于传达交易相关的扩展信息的对象。使用这些对象的交易平台有责任将这些扩展信息传递给竞拍者。

下表总结了竞价请求模型中用到的对象，可以作为以下子章节的索引。

| 对象 | 章节 | 描述 |
| --- | --- | --- |
| BidRequest | 3.2.1 | 顶级对象 |
| Imp | 3.2.2 | 包含某个指定展示的详细信息， 每个请求至少一个 |
| Banner | 3.2.3 | 一个Banner展示（包括banner视频）或者有视频的广告的详细信息 |
| Video | 3.2.4 | 一个视频展示或者Native展示的视频物料的详细信息 | 
| Native | 3.2.5 | 符合Native广告规范的Native展示的容器 | 
| Site | 3.2.6 | 调用展示的站点的详细信息 |
| App | 3.2.7 | 调用展示的应用的详细信息　|
| Publisher | 3.2.8 | 控制发布站点或应用内容的实体 |
| Content | 3.2.9 | 被发布内容的详细信息， 广告将会在其中展示 |
| Producer | 3.2.10 | 内容的产生着， 不一定是发布者（例如联合组织） |
| Device | 3.2.11 | 展示广告内容的设备的详细信息 |
| Geo | 3.2.12 | 设备的位置或者用户家的位置，由其父对象决定 |
| User | 3.2.13 | 设备的用户， 广告的受众 |
| Data | 3.2.14 | 来自特定数据源的附加的用户定向数据集合 |
| Segment | 3.2.15 | 来自特定数据源的关于一个用户的某个数据点 | 
| Regs | 3.2.16 | 影响该竞价请求中所有展示的监管条件 |
| Pmp | 3.2.17 | 适用于此次展示的一组私有市场协议 |
| Deal | 3.2.18 | 本次展示中买家和卖家之间的交易条款 |


##　3.2 对象规范

以下部分将会详细介绍竞价请求模型中的每个对象。 首先介绍下适用于所有如下内容的公约：

- 带有`required`修饰的属性的缺失将会技术上导致协议的破坏。
- 处于某些可选属性的业务重要性， 会被标识为`recommended`。
- 除非默认值被显示指定，一个缺失的属性被解释为`unknown`。

### 3.2.1 BidRequest

顶层竞价请求对象， 包含一个全局唯一的竞价请求或拍卖ID。 `id`属性是必须的因为其中至少包含一个展示对象（见3.2.2节）。 在这个对象中的所有其他对象所建立的规则和限制适用于其中的所有展示对象。

有一些子对象用于提供潜在买家的详细信息，在这些对象中个，`Site`和`App`对象，用于描述展示广告的发布媒体的类型。这些对象是高度推荐使用的， 但是每个竞价请求中只能使用一个，这取决于发起广告请求的是基于浏览器的页面内容或者非浏览器应用。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string;**required** | 竞价请求的唯一ID, 由广告交易平台提供 |
| imp | object array; **required** | 代表提供的展示信息的数组， 要求至少有一个 |
| site | object; **recommended** | `Site`对象，表示发布者站点相关的详细信息， 仅仅对站点适用且推荐填充 |
| app | object; **recommended** | `App`对象，表示发布应用的详细信息。仅对应用适用且推荐填充 |
| device | object; **recommended** | `Device`对象， 表示展示将要被发送到的用户设备的信息 |
| user | object;**recommended** | `User`对象， 表示使用设备的对象， 广告的受众 |
| test | integer; default 0 | 标识测试模式，拍卖不计价。 0表示实况（非测试）模式，1表示测试模式 |
| at | integer; default 2 | 拍卖类型（胜出策略）1表示第一价格 ，2标识第二价格。交易特定的拍卖类型可以用大于500的值定义 |
| tmax | integer | 用于在提交竞价请求时避免超时的最大时间，以毫秒为单位，这个值通常是线下沟通的 |
| wseat | string array | 允许在本次展现上进行竞拍的买家白Seat名单。 交易平台和竞拍者必须提前协商好Seat IDs |
| allimps | integer; default 0 | 用于标识交易平台是否可以验证当前的展示列表包含了当前上下文中所有展示。（例如，一个页面上的所有广告位，所有的视频广告点（视频前，视频中，时候后））用于支持路由封锁。 0表示不支持或未知， 1表示提供的展示列表代表所有可用的展示。 |
| cur | string array | 本次竞价请求允许的货币列表， 使用ISO-4217 字母码。 仅在交易平台接收多种货币的时候推荐填充。
| bcat | string array | 被封锁的广告主类别，使用IAB 内容类别，参考列表5.1。 |
| badv | string array | 域名封锁列表（比如 ford.com) |
| regs | object | `Reg`对象， 指明对本次请求有效的工业，法律或政府条例 |

### 3.2.2 Imp

这个对象描述了一个广告位或者将要参与竞拍的展现。一个竞价请求可以包含多个`Imp`	对象，这种状况的一个示例是一个交易平台支持售卖一个页面的所有广告位。 为了便于竞拍者区分， 每一个`Imp`对象都要有一个唯一标识（ID).

`Banner`, `Video`以及`Native`对象都属于`Imp`对象，只是标明了各自的展示类型。 展示者可以选择其中的一种类型或者混合使用多种类型。 但是，对于展示的任何给定的竞价请求必须属于提供的类型之一。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string;**required** | 在当前竞价请求上下文中唯一标识本次展示的标识（通常从1开始并以此递增)|
| banner | object | `Banner`对象， 如果展示需要以banner的形式提供则需要填充 |
| video | object | `Video`对象， 如果展示需要以视频的形式提供则需要填充 |
| native | object | `Native`对象， 如果展示需要以Native广告的形式提供则需要填充 |
| displaymanager | string | 广告媒体合作伙伴的名字， 用于渲染广告的SDK技术或者播放器（通常是视频或者移动广告）某些广告服务需要根据合作伙伴定制广告代码， 推荐在视频广告或应用广告中填充 |
| displaymanagerver | string | 广告媒体合作伙伴， 用于渲染广告的SDK技术或者播放器（通常是视频或者移动广告）的版本号。 某些广告服务需要根据合作伙伴定制广告代码， 推荐在视频广告或应用广告中填充 |
| instl | integer; default 0 | 1标识广告是插屏或者全屏广告， 0表示不是插屏广告 |
| tagid | string | 某个特定广告位或者广告标签的标识，用于发起竞拍。 为了方便调试问题或者进行买方优化 |
| bidfloor | float; default 0 | 本次展示的最低竞拍价格， 以CPM表示 |
| bidfloorcur | string; default "USD" | ISO-4217规定的字母码表标识的货币类型。 如果交易平台允许，可能与从竞拍者返回的竞价货币不同。|
| secure | integer | b标识展示请求是否需要使用HTTPS加密物料信息以及markup以保证安全， 0标识不需要使用安全链路， 1标识需要使用安全链路， 如果不填充，则表示未知， 可以认为是不需要使用安全链路。|
| iframebuster | string array | 特定交易支持的iframe buster的名字数组 |
| pmp | object | `Pmp`对象， 包含对本次展示生效的任何私有市场交易 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.3 Banner

Banner是最常见的展示类型。 虽然“banner”这个名词在其他的场景有很特别的意思， 在这里它可以是包括静态图像， 可扩展的广告单元或者一个在banner中播放的视频在内的很多东西。一组Banner对象可以出现在Video对象中来描述可选择在VAST贵方中定义的附加广告。

Banner作为Imp的子对象出现表示它是一个具有banner类型的展示对象. 同样的展示也可以是一个视频或者Native广告， 只要包含Video对象或者Native对象。然而， 任何为展示给定的竞价请求必须符合提供类型中的一个。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| w | integer; **recommended** | 展示的宽度，以像素为单位，如果没有指定`wmin`以及`wmax`, 这个值指的就是需要的展示宽度，否则指的是一个期望宽度 |
| h | integer; **recommended** | 展示的高度，以像素为党委，如果没有指定`hmin`以及`hmax`, 这个值指的就是需要的展示高度， 否则指的是一个期望高度 |
| wmax | integer | 展示宽度的最大值，以像素为单位， 如果和`w`一起出现， 则`w`应该被解释为推荐宽度或者期望宽度 |
| wmin | integer | 展示宽度的最小值，以像素为单位， 如果和`w`一起出现， 则`w`应该被解释为推荐宽度或者期望宽度 |
| hmax | integer | 展示高度的最大值，以像素为单位， 如果和`h`一起出现， 则`h`应该被解释为推荐宽度或者期望宽度 |
| hmin | integer | 展示高度的最小值，以像素为单位， 如果和`h`一起出现， 则`h`应该被解释为推荐宽度或者期望宽度 |
| id | string | banner对象的唯一标识。在一个Ad中包含Banner与Video的时候使用。值往往从1开始并依次递增，在依次展示中应当是唯一的 |
| btype | integer array | 限制的banner类型。参考表5.2 |
| battr | integer array | 限制的物料属性， 参考表5.3 |
| pos | integer | 广告在屏幕上的位置，参考表5.4 |
| mimes | string array | 支持的内容mime-type. 常用的mime-type包括application/x-shockwave-flash, image/jpg以及 image/gif. |
| topframe | integer | banner是在顶层frame中而不是iframe中， 0表示不是， 1表示是 |
| expdir | integer array | banner可以扩展的方向，参考表5.5 |
| api | integer array | 本次展示支持的API框架列表， 参考表5.6. 如果一个API没有被显式在列表中指明，则表示不支持|
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.4 Video

这个对象表示一个流式视频展示。 许多属性对于最小可用功能不是必须的，但是为了在需要的时候提供更好的控制能力会被使用。OpenRTB中的视频通常都是与标准一致的，复合广告的概念也是支持的， 可以包含用于定义复合广告的一组Banner对象。

Video作为Imp的子对象出现表示它是一个具有视频类型的展示对象。 同样的展示也可以是一个Banner或者Native广告， 只要包含Banner对象或者Native对象。然而， 任何为展示给定的竞价请求必须符合提供类型中的一个。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| mimes | string array; **required** | 支持的内容mime-type， 常用的类型包括用于windows媒体的video/x-ms-wmv以及用于Flash视频的video/x-flv. |
| minduration | integer; **recommended** | 最小的视频长度， 以秒为单位 |
| maxduration | integer; **recommended** | 最大的视频长度， 以秒为单位 |
| protocol | integer; **DEPRECATED** | 注意，使用`protocols`是高度推荐的。 支持的视频竞价响应协议。参考表5.8.至少一个支持的协议必须在protocol或者protocols属性中被指定 |
| protocols | integer array; **recommended** | 支持的视频竞价响应协议数组。参考表5.8.至少一个支持的协议必须在protocol或者protocols属性中被指定 |
| w | integer; **recommeded** | 视频播放器的宽度，像素为单位 |
| h | integer; **recommeded** | 视频播放器的高度，像素为单位 |
| startdelay | integer; **recommended** | 视频前，中及之后的广告位中视频广告的启动延时，以秒为单位, 参考表5.10|
| linearity | integer | 展示是否必须是线性的， 如果没有指定，则标识都是被允许的，参考表5.11 |
| sequence | integer | 如果在同一个竞价请求中提供了多个展示， 则需要考虑多个物料传输的顺序 |
| battr | integer array | 限制的物料属性，参考表5.3 |
| maxextended | integer | 最大的视频广告延长时间长度（如果支持延长）。如果为空或者0，表示不允许延长， 如果为-1，表示允许延时，且没有时间限制， 如果为大于0的数字， 则表示可以延长的时间长度比maxduration大的值 |
| minbitrate | integer | 最小的比特率，以Kbps为单位。交易平台可以动态的设置这个值或者为所有发布者统一设置该值 |
| maxbitrate | integer | 最大的比特率，以Kbps为单位。交易平台可以动态的设置这个值或者为所有发布者统一设置该值 |
| boxingallowed | integer; default 1 | 是否允许将4：3的内容展示在16：9的窗口， 0表示不允许，1表示允许 |
| playbackmethod | integer array | 允许的播放方式， 如果没有指定，表示支持全部，参考表5.9 |
| delivery | integer array | 支持的传输方式 （例如流式传输，逐步传输），如果没有指定，表示全部支持，参考表5.13|
| pos | integer | 广告在屏幕上的位置，参考表5.4 |
| companionad | object array | 如果支持复合广告，表示一组Banner对象 |
| api | integer array | 本次展示支持的API框架列表， 参考表5.6. 如果一个API没有被显式在列表中指明，则表示不支持|
| companiontype | integer array | 支持的VAST companion 广告类型， 参考表5.12。 如果在companionad中填充了Banner对象则推荐使用 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.5 Native

表示一个Native类型的展示。Native广告单元需要无缝的插入其周围的内容中（例如， 一个对Twitter或Facebook赞助）。 因此，响应必须具有良好的结构， 让展示者能够在细粒度上控制渲染过程。

Native小组委员会为OpenRTB开发了一个组合规范，名为Native Ad规范。 定义了Native广告的请求参数以及响应结构。这个对象以字符串的形式提供请求参数， 这样的话具体的请求参数就可以按照Native Ad规范独立演进。同样的， 广告markup也会按照该文档指定的结构提供。

Native作为Imp的子对象出现表示它是一个具有native类型的展示对象。 同样的展示也可以是一个Banner或者Video广告， 只要包含Banner对象或者Video对象。然而， 任何为展示给定的竞价请求必须符合提供类型中的一个。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| request | string; **required** | 遵守Native Ad规范的请求体 |
| ver | string; **recommended** | Native Ad规范的版本， 为了高效解析强烈推荐 |
| api | integer array | 本次展示支持的API框架列表， 参考表5.6. 如果一个API没有被显式在列表中指明，则表示不支持|
| battr | integer array | 限制的物料属性，参考表5.3 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.6 Site

如果广告载体是一个网站时应该包含这个对象，如果是非浏览器应用时则不需要。 一个竞价请求一定不能同时包含Site对象和App对象。 提供一个站点标识或者页面地址是很有用的， 但是不是严格必须的。
| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string; **recommended** | 交易特定的站点标识|
| name | string | 站点名称 （可以在展示者请求中作为别名标识）|
| domain | string | 站点的域名 （例如，"mysite.foo.com") |
| cat | string array | 站点的一组IAB 内容类型，参考表5.1 |
| sectioncat | string array | 描述站点当前部分的一组IAB内容类型，参考表5.1 |
| pagecat | string array | 描述站点当前视图的一组IAB内容类型，参考表5.1 |
| page | string | 展示广告将要被展示的页面地址 |
| ref | string | 引导到当前页面的referrer地址 |
| search | string | 引导到当前页面的搜索字符串 |
| mobile | integer | 移动优化标志， 0表示否，1表示是 |
| privacypolicy | integer | 表示该站点是否有隐私策略， 0表示没有， 1表示有 |
| publisher | Object |`Publisher`对象， 站点发布者的详细信息 |
| content | Object | `Content`对象， 该站点内容的详细信息 |
| keywords | string | 逗号分隔的站点的关键字信息 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.7 App

如果广告载体是非浏览器应用（通常是移动设备）时应该包含该对象， 网站则不需要包含。一个竞价请求一定不能同时包含Site对象和App对象。 提供一个App标识或者`bundle`是很有用的， 但是不是严格必须的。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string; **recommended** | 交易特定的应用标识|
| name | string | 应用名称 （可以在展示者请求中作为别名标识）|
| bundle | string | 应用信息或者包名（例如， com.foo.mygame); 需要是在整个交易过程中唯一的标识 |
| domain | string | 应用的域名（例如， "mygame.foo.com" ) |
| storeurl | string | 应用的商店地址， 遵循AQG 1.5 |
| cat | string array | 应用的IAB内容类型数组， 参考表5.1 |
| sectioncat | string array | 应用当前部分的IAB内容类型数组，参考表5.1 |
| pagecat | string array | 应用当前视图的IAB内容类型数组，参考表5.1 |
| ver | string | 应用版本号 |
| privacypolicy | integer | 表示该应用是否有隐私策略， 0表示没有， 1表示有 |
| paid | integer | 应用是否需要付费， 0表示免费， 1表示付费 |
| publisher | Object |`Publisher`对象， 应用发布者的详细信息 |
| content | Object | `Content`对象， 该应用内容的详细信息 |
| keywords | string | 逗号分隔的应用的关键字信息 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.8 Publisher

用于描述展示广告的媒体的发布者。通常发布者就是OpenRTB事务中的卖方。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string; **recommended** | 交易特定的发布者标识|
| name | string | 发布者名称 （可以在展示者请求中作为别名标识）|
| cat | string array | 发布者的IAB内容类型数组， 参考表5.1 |
| domain | string | 发布者的顶级域名（例如， "publisher.com" ) |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.9 Content

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string | 内容唯一标识 |
| episode | integer | 情节数目（通常用于视频内容） |
| title | string | 内容标题。 视频示例： “Search Committee"(电视）， ”A New Hope"(电影), "Endgame"(为网络制作） 非视频示例： “Why an Antarctic Glacier is Melting So Quickly"(时报杂志文章）|
| series | string | 内容系列。 视频示例：“The Office"(电视）， ”Start Wars"(电影,"Arby 'N' The Chief"(为网络制作） 非视频示例： “Ecocentric"(时报杂志博客）|
| season | string | 内容季数， 通常用于视频内容（例如，“第三季”）|
| producer | object | 内容提供者的详细信息 |
| url | string | 内容的url, 用于买方了解使用的上下文或者审查 |
| cat | string array | 内容生产者的IAB内容类型数组， 参考表5.1 |
| videoquality | integer | 视频质量，按照IAB的分类，参考表5.11 |
| context | integer | 内容类型（游戏，视频，文本等）， 参考表5.14 |
| contentrating | string | 内容分级（例如， MPAA美国电影分级制度) |
| userrating | string | 内容的用户评分（比如，星数，点赞数等） |
| qagmediarating | integer | 媒体评分，按照QAG规范。参考表5.15 |
| keywords | string | 逗号分隔的内容的关键字信息 |
| livestream | integer | 0表示不是实时，1表示实时 |
| sourcerelationship | integer | 0表示间接源， 1表示直接源 |
| len | integer | 内容长度， 用于音频或者视频 |
| language | string | 内容语言， 使用ISO-639-1-alpha-2 | 
| embeddable | integer | 表示内容是否可嵌套（例如一个可嵌套的视频播放器）， 0表示不可以， 1表示可以 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.10 Producer

定义内容的提供者， 广告会在这些内容中展示。 当内容会被多个发布者展示时是对于区分发布者和生产者是否是同一实体是有用的。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string| 内容生产者标识， 当内容会被多个发布者展示且可能使用嵌套标签展示在一个站点的时候有用 |
| name | string | 内容提供者名称 （例如， “Warner Bros"）|
| cat | string array | 内容提供者的IAB内容类型数组， 参考表5.1 |
| domain | string | 内容提供者的顶级域名（例如， "producer.com" ) |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.11 Device

提供用户使用的设备的详细信息。设备信息包括硬件，平台以及附加信息。设备可以是一部移动手机， 桌面电脑，机顶盒或者其他数码设备。 

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| ua | string; **recommended** | 浏览器User-Agent字符串 |
| geo | object; **recommended** | `Geo`对象，用用户当前位置表示设备位置 |
| dnt | integer; **recommended** | 浏览器在HTTP头中设置的标准的 “Do Not Track"标识， 0表示不限制追踪， 1表示限制（不允许）追踪 |
| ip | string; **recommended** | 最接近设备的IPv4地址 |
| ipv6 | string | 最接近设备的IPV6地址 | 
| devicetype | integer | 设备类型，参考被5.17 |
| make | string |　设备制造商，例如 "Apple" |
| model | string | 设备型号，例如 "iphone" |
| os | string | 设备操作系统， 例如 “ios" |
| osv | string | 设备操作系统版本号， 例如 “3.1.2” |
| hwv | string | 设备硬件版本， 例如 “5S” |
| h | integer | 屏幕的物理高度， 以像素为单位 |
| w | integer | 屏幕的物理宽度，以像素为单位 |
| ppi | integer | 以像素每英寸表示的屏幕尺寸|
| pxratio | float | 设备物理像素与设备无关像素的比率 |
| js | integer | 支持javascript, 0表示不支持， 1表示支持 |
| flashver | string | 浏览器支持的Flash版本 |
| language | string | 浏览器语言，使用ISO-639-1-alpha-2 |
| carrier | string | ISP的附带信息（如版本号）。“WIFI"通常在移动设备中表示高带宽。（例如,video freendly vs. cellular). |
| connectiontype | integer | 网络连接类型， 参考表5.18 |
| ifa | string | 广告主标识， 明文表示 |
| didsha1 | string | 硬件设备ID(例如 IMEI),使用SHA1哈希算法 |
| didmd5 | string | 硬件设备ID(例如 IMEI),使用md5哈希算法 |
| dpidsha1 | string | 设备平台ID(例如 Android ID),使用SHA1哈希算法 |
| dpidmd5 | string | 设备平台ID(例如 Android ID),使用md5哈希算法 |
| macidsha1 | string | 设备mac地址,使用SHA1哈希算法 |
| macidmd5 | string | 设备mac地址,使用md5哈希算法 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

>**最佳实践:** 当前没有关于设备生产商，型号，操作系统或其他附加信息的有效的开源列表。 交易平台通常使用商业产品或者其他专有列表来填充这些属性。 在适当的开放标准可用之前， 推荐交易平台向竞拍者发布他们支持的设备生产商， 型号，操作系统以及附加信息。

>**最佳实践:** 对于移动设备的IP合理的检测方式不是去直接检测的，通常存在于HTTP 的x-forwarded-for头中， 跳过私有的网络（例如10.x.x.x或者192.x.x.x), 扫描出已知的IP. 当交易平台向竞拍者传递设备的IP地址的时候， 要求交易平台仔细的研究并实现该属性。

### 3.2.12 Geo

用于封装一个地理位置信息的多种不同属性。 当作为`Device`对象的子节点的时候，标识设备的地理位置或者用户当前的地理位置。 当作为`User`的子节点的时候，标识用户家的位置（也就是说，不必是用户的当前位置）。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| lat | float | 纬度信息，取值范围-90.0到+90.0， 负值表示南方 |
| lon | float | 经度信息， 取值返回-180.0到+180.0， 负值表示西方 |
| type | integer | 位置信息的源， 当传递lat/lon的时候推荐填充， 参考表5.16 |
| country | string | 国家码， 使用 ISO-3166-1-alpha-3|
| region | string | 区域码， 使用ISO-3166-2; 如果美国则使用2字母区域码 |
| regionfips104 | string | 国家的区域，使用 FIPS 10-4 表示。 虽然OpenRTB支持这个属性，它已经与2008年被NIST撤销了 |
| metro | string | 谷歌metro code; 与Nielsen DMA相似但不完全相同， 参见附录A |
| city | string | 城市名，使用联合国贸易与运输位置码， 参见附录A |
| zip | string | 邮政编码或者邮递区号 |
| utcoffset | integer | 使用UTC加或者减分钟数的方式表示的本地时间 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.13 User

描述了解或者持有设备的用户的信息（也就是广告的受众）。 用户`id`是一个exchange artifact, 可能随着屏幕旋转或者其他的隐私策略改变。 尽管如此，用户id必须在足够长的一段时间内保持不变，以为目标用户定向和用户访问频率限制提供合理的服务。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string; **recommended** | 交易特定的用户标识， 推荐`id`和`buyeruid`中至少提供一个。 |
| buyeruid | string; **recommended** | 买方为用户指定的ID，由交易平台为买方映射。推荐`id`和`buyeruid`中至少提供一个。|
| yob | integer | 生日年份，使用4位数字表示 |
| gender | strnig | 性别， M表示男性， F表示女性， O标识其他类型，不填充表示未知|
| keywords | string | 逗号分隔的关键字， 兴趣或者意向列表 |
| customdata | string | 可选特性， 用于传递给竞拍者信息，在交易平台的cookie中设置。字符串必须使用base85编码的 cookie，可以是任意格式。 JSON加密的时候必须包括转义的引号。 |
| geo | object | `Geo`对象， 用户家的位置信息。不必是用户的当前位置 |
| data | object array | 附加的用户信息， 每个 `Data`对象表示一个不同的数据源 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |


### 3.2.14 Data

`Data`和`Segment`对象一起允许指定用户附加信息。数据可能来自多个数据源， 可能来自交易平台自身或者第三方提供的信息， 可以使用`id`属性区分。 一个竞价请求可以混合来自多个提供者的数据信息。 交易平台应该优先提供正在使用的数据提供者的信息。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string | 交易特定的数据提供者标识 |
| name | string | 交易特定的数据提供者名称 |
| segment | object array | 包含数据内容的一组`Segment`对象 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.15 Segment

数据字段， 描述用户信息数据的键值对。 其父对象`Data`是某个给定数据提供者的数据字段的集合。交易平台必须优先将字段的名称和值传递给竞拍者。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string | 数据提供者的特定数据段的ID |
| name | string | 数据提供者的特定数据段的名称 |
| value | string | 表示数据字段值的字符串 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.16 Regs

描述任何适用于该请求的法律，政府或者工业管控条例。 `coppa`(Children’s Online Privacy Protection Act)标志着是否该请求是否符合美国联邦贸易委员会颁布的美国儿童在线隐私保护法案，详情可参考7.1节。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| coppa | integer | 标志着该请求是否遵从COPPA法案， 0表示不遵从， 1表示遵从 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.17 Pmp

包含本展示涉及的买卖双方的直接交易相关的私有市场信息。 真实的交易信息使用一组`Deal`对象表示， 详情可参考7.2节。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| private_auction | integer | 标识在`Deal`对象中指明的席位的竞拍合格标准， 0标识接受所有竞拍， 1标识竞拍受`deals`属性中描述的规则的限制  |
| deals | object array | 一组`Deal`对象， 用于传输适用于本次展示的交易信息 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 3.2.18 Deal

描述限制买卖双方之间交易的一些条款。 它在`Pmp`集合中的出现表示该展示符合交易描述的条款。详情参考7.2节。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string; **required** | 直接交易的唯一ID | 
| bidfloor | float; default 0 | 本次展示的最低竞价，以CPM为单位 |
| bidfloorcur | string; default 'USD' | 使用ISO-4217码表指定的货币。 如果交易平台允许，这可能与竞价者返回的竞价货币类型不一致 |
| at | integer | 可选的覆盖竞价请求中的竞拍类型， 1表示第一价格竞拍，2标识第二价格竞拍， 3表示使用bidfloor可以作为交易价格 | 
| wseat | string array | 允许参与本次交易竞价的买方席位白名单。 席位ID需要交易平台和竞拍者提前协商， 忽略本属性标示没有席位限制 |
| wadomain | string array | 允许参与本次交易竞价的广告主域名列表（例如， advertiser.com). 忽略本属性标示没有广告主限制。 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

# 4. Bid Response 规范

RTB响应包含着一个对特定展示的出价信息。 出价信息本质上是一个购买要约。竞价响应由顶层的竞价响应对象和用于描述该出价信息的一些可选对象组成。 表示不出价的最节省带宽的方式是使用空的HTTP响应。 不符合标准格式的响应或者没有包含实际出价信息的响应都可以解释为不出价。

## 4.1 Object Model

下边是竞价响应的对象模型。模型中的顶级对象（即没有名字的最外层的JSON对象）表示 `BidResponse`. 一个竞价响应可能包含来自多个席位（即来自实际出价者的购买实体）。 实际上一个响应可能包含来自同一个席位的多个出价； 通常来自不同的camapigns,但也不一定总是这样。 这样可以提高席位的胜出可能性， 因为大多数交易平台会为了展示者的利益强制设置了一些限制列表。

![](https://raw.githubusercontent.com/leeowenowen/OpenRTB_API_Specification-/master/res/bid_response_object_model.png)

从上图可以看出，真实的响应对象都显示在左边：顶级对象`BidResponse`, 表示席位的`SeatBid`以及`Bid`对象。 其他展示的对象都是与竞价响应相关的来自竞价请求的对象。特别要指出的是出于积极的追踪目的， `BidResponse`包含了`BidRequest`的ID。由于一个竞价请求可以包含多个展示， 所以`Bid`对象包含了`Imp`的ID, 用以表示是对该展示的出价。 如果某个出价符合某个私有交易市场的交易管制信息， `Bid`也应当包含特定`Deal`对象的ID.

图中没有展示的是扩展对象。扩展对象是一个没有定义结构的对象， 它可以添加到任何对象中以纯属交易相关的扩展信息。 使用这些对象的竞拍者有责任将这些扩展信息传递给交易平台。

下表总结了竞价响应中的对象， 可以作为作为下文详细信息描述的索引。

| 对象 | 章节 | 描述 |
| --- | --- | --- |
| BidResponse | 4.2.1 | 顶级对象 |
| SeatBid | 4.2.2 | 竞拍者给出的一组出价信息 |
| Bid | 4.2.3 | 在特定商业条款下购买某个指定展示的要约 | 

## 4.2 Object Specifications

以下部分将会详细介绍竞价响应模型中的每个对象。 首先介绍下适用于所有如下内容的公约：

- 带有`required`修饰的属性的缺失将会技术上导致协议的破坏。
- 处于某些可选属性的业务重要性， 会被标识为`recommended`。
- 除非默认值被显示指定，一个缺失的属性被解释为`unknown`。

### 4.2.1 BidResponse

顶级的竞价形影对象（即没有名称的最外层JSON对象）。 `id`属性是竞价请求的ID,用于记录日志。 同样的`bidid`是一个可选的响应追踪标识， 如果指定了该标识， 如果之后竞拍者胜出了，则在胜出通知子流程中，需要将该标识填充进去。 至少一个 `seatbid`对象是必须的， 表示对该展示的至少一个出价。 其他的属性都是可选的。

如果要表示不出价， 可以选择使用空的HTTP响应体以及HTTP 204响应码。 如果竞拍者想要向交易平台传递不出价的原因， 可以返回一个只填充nbr属性的`BidResponse`对象。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string; **required** | 竞价请求的标识 |
| seatbid | object array | 一组`SeatBid`对象， 如果出价，则至少应该填充一个 |
| bidid | string | 竞拍者生成的响应ID, 辅助日志或者交易追踪 |
| cur | string; default 'USD' | 使用ISO-4217码表标识货币类型 |
| customdata | string | 可选特性，允许出价者以设置cookie的方式向交易平台传递信息。 字符串可以是任何格式， 必须使用base85编码，JSON编码必须包含转义的引号。 |
| nbr | integer | 不出价的原因， 参考表5.19 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 4.2.2 SeatBid

一个竞价响应可以包含多个`SeatBid`对象， 每个代表着不同的出价者且包含一个或多个独立的出价信息。 如果请求中有多个展示信息， `group`属性可以用来指定一个席位对胜出任何展示感兴趣（可以不是全部展示）或者它仅对胜出所有展示感兴趣。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| bid | object array; **required** | 至少一个`Bid`对象的数组，每个对象关联一个展示。多个出价可以关联同一个展示 |
| seat | string | 出价者席位标识， 代表本次出价的出价人 |
| group | integer; default 0 | 0 标识展示可以独立胜出， 1标识展示必须整组胜出或失败 |
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

### 4.2.3 Bid

一个`SeatBid`对象包括一个或者多个`Bid`对象， 每一个`Bid`对象通过`impid`关联竞价请求中的一个展示, 由一个对该展示出价组成。

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| id | string; **required** | 竞拍者生成的竞价ID，用于记录日志或行为追踪 |
| impid | string; **required** | 关联的竞价请求中的`Imp`对象的ID |
| price | float; **required** | 虽然本次只是对某一个展示的出价，但是竞拍价格是以CPM表示。需要注意数据类型是float,所以在处理货币的时候强烈建议使用相关的数学处理对象（比如，Java中的BigDecimal) |
| adid | string | 预加载的广告ID, 可以在交易胜出的时候使用 |
| nurl | string | 胜出通知地址， 如果竞价胜出的时候由交易平台调用； 可选标识serving ad markup |
| adm | string | 竞拍胜出之后可选的传输ad markup的方式， 如果胜出通知中包含ad markup则优先使用adm |
| adomain | string array | 用于限制检测的广告主域名， 对于旋转的物料可以是一个数组， 交易平台可以限制只允许一个域名 |
| bundle | string | 被广告的应用的包名或者其他信息， 如果可以，倾向于使用交易内唯一的ID |
| iurl | string | 用于质量或者安全监测的表示广告活动内容的图像地址， 不允许缓存 |
| cid | string | Campaign ID , 辅助广告质量检查，iurl代表的一组物料 |
| crid | string | Creative ID, 辅助广告质量检查 |
| cat | string array | creative的IAB内容类型，参考表5.1 |
| attr | integer array | 描述creative的属性集合，参考表5.3 |
| dealid | string | 如果出价从属与某个私有市场直接交易规则， 则指向竞价请求中该交易规则的deal.id |
| h | integer |　creative 的高度， 以像素为单位 |
| w | integer | creative 的宽度， 以像素为单位 | 
| ext | object | 特定交易的OpenRTB协议的扩展信息占位符 |

对于每一个`Bid`对象， `nurl`属性包含了一个胜出通知地址，如果竞拍者胜出了一个展示， 交易平台会通过通知地址通知竞拍者胜出信息并通过替换通知地址中的宏向竞拍者传递特定的信息。 胜出通知的返回或者`adm`书慈宁宫可以用于提供markup. 不管使用哪种方式， 交易平台需要对markup执行前面提到的宏替换操作。

## 4.3 Ad Serving Options

在OpenRTB规范范围内的RTB过程实现核心在与markup的传输。 随着展示以及其他广告类型的限制， markup可以使XHTML, 带有内嵌Javascript的XHTML，用于视频的超大文档， 一个Native广告单元结果以及其他未来可能出现的类型。

除了宏替换以及传输到提供方， OpenRTB标准没有要求对ad markup做任何处理。 然而， 还是有很多标准方式用于从竞拍者向交易平台传输markup信息。具体的方式由竞拍者决定， 一个遵从OpenRTB协议的交易平台应当支持以下定义的所有方式。

### 4.3.1 Markup Served on the Win Notice

在这种实现方式中， ad markup是通过胜出通知返回给交易平台的。 在这种情况下， 胜出通知的响应体包含且仅包含ad markup信息。 响应体中必须不能再有其他数据， 使用这种方式， `bid.adm`属性必须被忽略。

### 4.3.2 Markup Served in the Bid

在这种实现方式中， ad markup在`bid`实体中被返回。 这需要通过`bid.adm`属性完成， 如果`adm`属性和胜出通知都返回数据， `adm`内容会被使用。

### 4.3.3 Comparison of Ad Serving Approaches

每种广告提供方式有它自己的优势，且这种优势随着交易平台和竞拍者不同而不同。

** Ad Served on the Win Notice**

- 较少带宽： 仅仅在胜出之后提供ad markup可以节省大量的带宽使用， 尤其是对于交易平台， 其代价是非常巨大的。
- 额外的竞拍者灵活性： 竞拍者可能在竞拍的时候已经知道了将要提供的广告信息， 但是这种方式在结算价格发布之后提供了附加的可选决策点。

** Ad Served in the Bid**

- 减少广告丢失的风险： 一次广告丢失是这样的场景， 一个竞拍者胜出了， 但是在提供广告内容的时候失败了。 但是额外的HTTP 失败可能被减少了。
- 潜在的并发： 交易平台可以选择并发的返回ad markup和进行胜出通知， 从而提高用户体验。

## 4.4 Substitituion Macros

胜出通知地址以及它的格式是由竞拍者定义的。为了让交易平台可以向胜出的竞价者传输确定的信息，可以在胜出通知地址中插入一些可替换的宏。在调用胜出通知地址之外， 交易平台会在竞拍者提供的胜出通知地址中查找已定义的宏并使用合适的数据进行替换。
注意这个替换过程是非常简单的，仅仅是在查找到宏的地方直接进行替换， 不会进行任何的语法校验。如果响应的值是可选的且没有被指定， 响应的宏就会直接被删除掉（即使用空字符串替换）。

相同的替换宏业可以出现在ad markup中。 交易平台会做相同的数据替换操作。  这个操作是不会关心markup是在胜出通知中返回或者通过`bid.adm`属性在竞价响应中传递。 将宏用在ad markup中的一个用例是当竞拍者希望从设备本身接收官方胜出通知。 为了完成这些， 竞拍者需要在ad markup中包含一个追踪像素， 该追踪像素的地址可能包含任何可用的宏。


| Micro | Description |
| --- | --- |
| ${AUCTION_ID} | 竞价请求的ID; 来自 BidRequest.id 属性. | 
| ${AUCTION_BID_ID}  | `Bid`的ID; 来自 BidResponse.bidid 属性. |
| ${AUCTION_IMP_ID} | 胜出的展示的ID ; 来自 imp.id 属性. |
| ${AUCTION_SEAT_ID} | 竞拍者的席位ID | 
| ${AUCTION_AD_ID} | 竞拍者要提供的广告的ID ; 来自 bid.adid 属性. |
| ${AUCTION_PRICE} | 拍卖价格，与`Bid`使用相同的货币类型 |
| ${AUCTION_CURRENCY}  | 竞价使用的货币类型（隐式或者显式）， 仅仅用于确认 |

在替换之前， 处于安全性考虑， 宏对应数据的信息是可以使用多种混淆或者加密算法加密的。 当比如价格信息通过广告信息中的一个追踪像素被带出交易平台， 通过发布者，最终到达设备浏览器这种场景下， 这种做法就尤其有用。

要制定某个特定的宏是被加密的，需要将“:X”后缀附加到宏名称之后， X是一个表示所使用算法的字符串。 本规范并没有规定的具体的算法选项，这需要交易平台和竞拍者之间进行协商。  举个例子， 假设表示价格的宏使用Base64加密其使用加密码“B64", 宏就会被写成如下模样：

```
${AUCTION_PRICE:B64}
```

>最佳实践： 应该尽量少的对宏进行加密，因为这需要额外的处理消耗（加解密）。 对于完全在竞拍者和交易平台之间的通信（比如， 从交易平台发起的一个胜出通知）， 加密通常是没有必要的。

# 5. 枚举列表规范

所有的参考列表由IAB维护并及时更新到OpenRTB的网站上。 介于此， 实现者应当保证他们是根据最新的列表和枚举来实现。

## 5.1 内容类型

以下列表描述了IAB的类型分类信息。 为了方便对象之间对第一级和第二级类型的沟通方便，已经采用了标准的ID标识。

这个OpenRTB表中的值都是继承自IAB的质量保证指南（QAG). 实现者应当与IAB.net上的QAG中的值保持同步。

| 值 | 描述 | 中文释义 |
| --- | --- | --- |
| IAB1 | Arts & Entertainment | 艺术与娱乐 |
| IAB1-1 | Books & Literature | 书籍与文学 |
| IAB1-2 | Celebrity Fan/Gossip | 名人粉丝/八卦 |
| IAB1-3 | Fine Art | 美术 |
| IAB1-4 | Humor | 幽默 |
| IAB1-5 | Movies | 电影 |
| IAB1-6 | Music | 音乐 |
| IAB1-7 | Television | 电视 |
| IAB2 | Automotive | 汽车 |
| IAB2-1 | Auto Parts | 汽车配件 |
| IAB2-2 | Auto Repair | 汽车维修 |
| IAB2-3 | Buying/Selling Cars | 汽车买卖 |
| IAB2-4 | Car Culture | 汽车文化 |
| IAB2-5 | Certified Pre-Owned | 二手车买卖 |
| IAB2-6 | Convertible | |
| IAB2-7 | Coupe | 双门跑车 |
| IAB2-8 | Crossover | 跨界车 |
| IAB2-9 | Diesel | 柴油机 |
| IAB2-10 | Electric Vehicle | 电动汽车 |
| IAB2-11 | Hatchback | 有仓门式后背的汽车 |
| IAB2-12 | Hybrid | 混合动力车 |
| IAB2-13 | Luxury | 豪华车 |
| IAB2-14 | Minivan | 小货车 |
| IAB2-15 | Motorcycles | 摩托车 |
| IAB2-16 | Off-Road Vehicles | 越野车 |
| IAB2-17 | Performance Vehicles | 车辆性能 |
| IAB2-18 | Pickup | 皮卡 |
| IAB2-19 | Road-Side Assistance | 路边援助 |
| IAB2-20 | Sedan | 轿车 |
| IAB2-21 | Trucks & Accessories | 卡车及配件 |
| IAB2-22 | Vintage Cars | 老爷车 |
| IAB2-23 | Wagon | 马车 |
| IAB3 | Business | 商业 |
| IAB3-1 | Advertising | 广告 |
| IAB3-2 | Agriculture | 农艺 |
| IAB3-3 | Biotech/Biomedical | 生物技术/生物医学 |
| IAB3-4 | Business Software | 商业软件 |
| IAB3-5 | Construction | 建筑 |
| IAB3-6 | Forestry | 林业 |
| IAB3-7 | Government | 政府 |
| IAB3-8 | Green Solutions | 绿色解决方案 |
| IAB3-9 | Human Resources | 人力资源 |
| IAB3-10 | Logistics | 物流 |
| IAB3-11 | Marketing | 市场营销 |
| IAB3-12 | Metals | 金属 |
| IAB4 | Careers | 职业生涯 |
| IAB4-1 | Career Planning | 职业规划 |
| IAB4-2 | College | 大学 |
| IAB4-3 | Financial Aid | 助学金|
| IAB4-4 | Job Fairs | 招聘会 |
| IAB4-5 | Job Search | 找工作 |
| IAB4-6 | Resume Writing/Advice | 简历书写与建议 |
| IAB4-7 | Nursing | 护理 |
| IAB4-8 | Scholarships | 奖学金 |
| IAB4-9 | Telecommuting | 远程办公 |
| IAB4-10 | U.S. Military | 美国军方 |
| IAB4-11 | Career Advice | 职业建议 |
| IAB5 | Education | 教育 |
| IAB5-1 | 7-12 | Education |  7-12岁教育 |
| IAB5-2 | Adult Education | 成人教育 |
| IAB5-3 | Art History | 艺术历史 |
| IAB5-4 | College Administration | 大学管理 |
| IAB5-5 | College Life | 大学生活 |
| IAB5-6 | Distance Learning | 远程教育 |
| IAB5-7 | English as a 2nd Language | 英语作为第二语言 |
| IAB5-8 | Language Learning | 语言学习 |
| IAB5-9 | Graduate School | 研究生院 |
| IAB5-10 | Homeschooling | 在家教育 |
| IAB5-11 | Homework/Study Tips | 作业/学习 |
| IAB5-12 | K-6 or Educators | K-6年级教育工作者 |
| IAB5-13 | Private School | 私立学校 |
| IAB5-14 | Special Education | 特殊教育 |
| IAB5-15 | Studying Business | 学习商业 |
| IAB6 | Family & Parenting | 家庭和父母 |
| IAB6-1 | Adoption | 收养 |
| IAB6-2 | Babies & Toddlers | 婴幼儿 |
| IAB6-3 | Daycare/Pre School | 托儿所 |
| IAB6-4 | Family Internet | 家庭网络 |
| IAB6-5 | Parenting - K-6 or Kids | K-6年级小孩的教育 |
| IAB6-6 | Parenting teens | 青少年教育 |
| IAB6-7 | Pregnancy | 怀孕 |
| IAB6-8 | Special Needs Kids | 特殊需要的孩子 |
| IAB6-9 | Eldercare | 老年人照顾 |
| IAB7 | Health & Fitness | 健康与健身 |
| IAB7-1 | Exercise | 锻炼 |
| IAB7-2 | ADD | 注意力缺陷障碍 |
| IAB7-3 | AIDS/HIV | 艾滋病 |
| IAB7-4 | Allergies | 过敏症 |
| IAB7-5 | Alternative Medicine | 替代医学 |
| IAB7-6 | Arthritis | 关节炎 |
| IAB7-7 | Asthma | 哮喘 |
| IAB7-8 | Autism/PDD | 自闭症/发育迟缓者  |
| IAB7-9 | Bipolar Disorder | 抑郁狂躁型忧郁症 |
| IAB7-10 | Brain Tumor | 脑瘤 |
| IAB7-11 | Cancer | 癌症 |
| IAB7-12 | Cholesterol | 胆固醇 |
| IAB7-13 | Chronic Fatigue Syndrome | 慢性疲劳综合症 |
| IAB7-14 | Chronic Pain | 慢性疼痛 |
| IAB7-15 | Cold & Flu | 感冒和流感 |
| IAB7-16 | Deafness | 耳聋 |
| IAB7-17 | Dental Care | 牙科保健 |
| IAB7-18 | Depression | 抑郁症 |
| IAB7-19 | Dermatology | 皮肤病学 |
| IAB7-20 | Diabetes | 糖尿病 |
| IAB7-21 | Epilepsy | 癫痫 |
| IAB7-22 | GERD/Acid Reflux |  胃食管反流/胃酸倒流 |
| IAB7-23 | Headaches/Migraines | |
| IAB7-24 | Heart Disease | |
| IAB7-25 | Herbs for Health | |
| IAB7-26 | Holistic Healing | |
| IAB7-27 | IBS/Crohn’s Disease | |
| IAB7-28 | Incest/Abuse Support | |
| IAB7-29 | Incontinence | |
| IAB7-30 | Infertility | |
| IAB7-31 | Men’s Health | |
| IAB7-32 | Nutrition | |
| IAB7-33 | Orthopedics | |
| IAB7-34 | Panic/Anxiety Disorders | |
| IAB7-35 | Pediatrics | |
| IAB7-36 | Physical Therapy | |
| IAB7-37 | Psychology/Psychiatry | |
| IAB7-38 | Senior Health | |
| IAB7-39 | Sexuality | |
| IAB7-40 | Sleep Disorders | |
| IAB7-41 | Smoking Cessation | |
| IAB7-42 | Substance Abuse | |
| IAB7-43 | Thyroid Disease | |
| IAB7-44 | Weight Loss | |
| IAB7-45 | Women's Health | |
| IAB8 | Food & Drink | |
| IAB8-1 | American Cuisine | |
| IAB8-2 | Barbecues & Grilling | |
| IAB8-3 | Cajun/Creole | |
| IAB8-4 | Chinese Cuisine | |
| IAB8-5 | Cocktails/Beer | |
| IAB8-6 | Coffee/Tea | |
| IAB8-7 | Cuisine-Specific | |
| IAB8-8 | Desserts & Baking | |
| IAB8-9 | Dining Out | |
| IAB8-10 | Food Allergies | |
| IAB8-11 | French Cuisine | |
| IAB8-12 | Health/Low-Fat Cooking | |
| IAB8-13 | Italian Cuisine | |
| IAB8-14 | Japanese Cuisine | |
| IAB8-15 | Mexican Cuisine | |
| IAB8-16 | Vegan | |
| IAB8-17 | Vegetarian | |
| IAB8-18 | Wine | |
| IAB9 | Hobbies & Interests | |
| IAB9-1 | Art/Technology | |
| IAB9-2 | Arts & Crafts | |
| IAB9-3 | Beadwork | |
| IAB9-4 | Bird-Watching | |
| IAB9-5 | Board Games/Puzzles | |
| IAB9-6 | Candle & Soap Making | |
| IAB9-7 | Card Games | |
| IAB9-8 | Chess | |
| IAB9-9 | Cigars | |
| IAB9-10 | Collecting | |
| IAB9-11 | Comic Books | |
| IAB9-12 | Drawing/Sketching | |
| IAB9-13 | Freelance Writing | |
| IAB9-14 | Genealogy | |
| IAB9-15 | Getting Published | |
| IAB9-16 | Guitar | |
| IAB9-17 | Home Recording | |
| IAB9-18 | Investors & Patents | |
| IAB9-19 | Jewelry Making | |
| IAB9-20 | Magic & Illusion | |
| IAB9-21 | Needlework | |
| IAB9-22 | Painting | |
| IAB9-23 | Photography | |
| IAB9-24 | Radio | |
| IAB9-25 | Roleplaying Games | |
| IAB9-26 | Sci-Fi & Fantasy | |
| IAB9-27 | Scrapbooking | |
| IAB9-28 | Screenwriting | |
| IAB9-29 | Stamps & Coins | |
| IAB9-30 | Video & Computer Games | |
| IAB9-31 | Woodworking | |
| IAB10 | Home & Garden | |
| IAB10-1 | Appliances | |
| IAB10-2 | Entertaining | |
| IAB10-3 | Environmental Safety | |
| IAB10-4 | Gardening | |
| IAB10-5 | Home Repair | |
| IAB10-6 | Home Theater | |
| IAB10-7 | Interior Decorating | |
| IAB10-8 | Landscaping | |
| IAB10-9 | Remodeling & Construction | |
| IAB11 | Law, Government, & Politics | |
| IAB11-1 | Immigration | |
| IAB11-2 | Legal Issues | |
| IAB11-3 | U.S. Government Resources | |
| IAB11-4 | Politics | |
| IAB11-5 | Commentary | |
| IAB12 | News | |
| IAB12-1 | International News | |
| IAB12-2 | National News | |
| IAB12-3 | Local News | |
| IAB13 | Personal Finance | |
| IAB13-1 | Beginning Investing | |
| IAB13-2 | Credit/Debt & Loans | |
| IAB13-3 | Financial News | |
| IAB13-4 | Financial Planning | |
| IAB13-5 | Hedge Fund | |
| IAB13-6 | Insurance | |
| IAB13-7 | Investing | |
| IAB13-8 | Mutual Funds | |
| IAB13-9 | Options | |
| IAB13-10 | Retirement Planning | |
| IAB13-11 | Stocks | |
| IAB13-12 | Tax Planning | |
| IAB14 | Society | |
| IAB14-1 | Dating | |
| IAB14-2 | Divorce Support | |
| IAB14-3 | Gay Life | |
| IAB14-4 | Marriage | |
| IAB14-5 | Senior Living | |
| IAB14-6 | Teens | |
| IAB14-7 | Weddings | |
| IAB14-8 | Ethnic Specific | |
| IAB15 | Science | |
| IAB15-1 | Astrology | |
| IAB15-2 | Biology | |
| IAB15-3 | Chemistry | |
| IAB15-4 | Geology | |
| IAB15-5 | Paranormal Phenomena | |
| IAB15-6 | Physics | |
| IAB15-7 | Space/Astronomy | |
| IAB15-8 | Geography | |
| IAB15-9 | Botany | |
| IAB15-10 | Weather | |
| IAB16 | Pets | |
| IAB16-1 | Aquariums | |
| IAB16-2 | Birds | |
| IAB16-3 | Cats | |
| IAB16-4 | Dogs | |
| IAB16-5 | Large Animals | |
| IAB16-6 | Reptiles | |
| IAB16-7 | Veterinary Medicine | |
| IAB17 | Sports | |
| IAB17-1 | Auto Racing | |
| IAB17-2 | Baseball | |
| IAB17-3 | Bicycling | |
| IAB17-4 | Bodybuilding | |
| IAB17-5 | Boxing | |
| IAB17-6 | Canoeing/Kayaking | |
| IAB17-7 | Cheerleading | |
| IAB17-8 | Climbing | |
| IAB17-9 | Cricket | |
| IAB17-10 | Figure Skating | |
| IAB17-11 | Fly Fishing | |
| IAB17-12 | Football | |
| IAB17-13 | Freshwater Fishing | |
| IAB17-14 | Game & Fish | |
| IAB17-15 | Golf | |
| IAB17-16 | Horse Racing | |
| IAB17-17 | Horses | |
| IAB17-18 | Hunting/Shooting | |
| IAB17-19 | Inline Skating | |
| IAB17-20 | Martial Arts | |
| IAB17-21 | Mountain Biking | |
| IAB17-22 | NASCAR Racing | |
| IAB17-23 | Olympics | |
| IAB17-24 | Paintball | |
| IAB17-25 | Power & Motorcycles | |
| IAB17-26 | Pro Basketball | |
| IAB17-27 | Pro Ice Hockey | |
| IAB17-28 | Rodeo | |
| IAB17-29 | Rugby | |
| IAB17-30 | Running/Jogging | |
| IAB17-31 | Sailing | |
| IAB17-32 | Saltwater Fishing | |
| IAB17-33 | Scuba Diving | |
| IAB17-34 | Skateboarding | |
| IAB17-35 | Skiing | |
| IAB17-36 | Snowboarding | |
| IAB17-37 | Surfing/Body-Boarding | |
| IAB17-38 | Swimming | |
| IAB17-39 | Table Tennis/Ping-Pong | |
| IAB17-40 | Tennis | |
| IAB17-41 | Volleyball | |
| IAB17-42 | Walking | |
| IAB17-43 | Waterski/Wakeboard | |
| IAB17-44 | World Soccer | |
| IAB18 | Style & Fashion | |
| IAB18-1 | Beauty | |
| IAB18-2 | Body Art | |
| IAB18-3 | Fashion | |
| IAB18-4 | Jewelry | |
| IAB18-5 | Clothing | |
| IAB18-6 | Accessories | |
| IAB19 | Technology & Computing | |
| IAB19-1 | 3-D Graphics | |
| IAB19-2 | Animation | |
| IAB19-3 | Antivirus Software | |
| IAB19-4 | C/C++ | |
| IAB19-5 | Cameras & Camcorders | |
| IAB19-6 | Cell Phones | |
| IAB19-7 | Computer Certification | |
| IAB19-8 | Computer Networking | |
| IAB19-9 | Computer Peripherals | |
| IAB19-10 | Computer Reviews | |
| IAB19-11 | Data Centers | |
| IAB19-12 | Databases | |
| IAB19-13 | Desktop Publishing | |
| IAB19-14 | Desktop Video | |
| IAB19-15 | Email | |
| IAB19-16 | Graphics Software | |
| IAB19-17 | Home Video/DVD | |
| IAB19-18 | Internet Technology | |
| IAB19-19 | Java | |
| IAB19-20 | JavaScript | |
| IAB19-21 | Mac Support | |
| IAB19-22 | MP3/MIDI | |
| IAB19-23 | Net Conferencing | |
| IAB19-24 | Net for Beginners | |
| IAB19-25 | Network Security | |
| IAB19-26 | Palmtops/PDAs | |
| IAB19-27 | PC Support | |
| IAB19-28 | Portable | |
| IAB19-29 | Entertainment | |
| IAB19-30 | Shareware/Freeware | |
| IAB19-31 | Unix | |
| IAB19-32 | Visual Basic | |
| IAB19-33 | Web Clip Art | |
| IAB19-34 | Web Design/HTML | |
| IAB19-35 | Web Search | |
| IAB19-36 | Windows | |
| IAB20 | Travel | |
| IAB20-1 | Adventure Travel | |
| IAB20-2 | Africa | |
| IAB20-3 | Air Travel | |
| IAB20-4 | Australia & New Zealand | |
| IAB20-5 | Bed & Breakfasts | |
| IAB20-6 | Budget Travel | |
| IAB20-7 | Business Travel | |
| IAB20-8 | By US Locale | |
| IAB20-9 | Camping | |
| IAB20-10 | Canada | |
| IAB20-11 | Caribbean | |
| IAB20-12 | Cruises | |
| IAB20-13 | Eastern Europe | |
| IAB20-14 | Europe | |
| IAB20-15 | France | |
| IAB20-16 | Greece | |
| IAB20-17 | Honeymoons/Getaways | |
| IAB20-18 | Hotels | |
| IAB20-19 | Italy | |
| IAB20-20 | Japan | |
| IAB20-21 | Mexico & Central America | |
| IAB20-22 | National Parks | |
| IAB20-23 | South America | |
| IAB20-24 | Spas | |
| IAB20-25 | Theme Parks | |
| IAB20-26 | Traveling with Kids | |
| IAB20-27 | United Kingdom | |
| IAB21 | Real Estate | |
| IAB21-1 | Apartments | |
| IAB21-2 | Architects | |
| IAB21-3 | Buying/Selling Homes | |
| IAB22 | Shopping | |
| IAB22-1 | Contests & Freebies | |
| IAB22-2 | Couponing | |
| IAB22-3 | Comparison | |
| IAB22-4 | Engines | |
| IAB23 | Religion & Spirituality | |
| IAB23-1 | Alternative Religions | |
| IAB23-2 | Atheism/Agnosticism | |
| IAB23-3 | Buddhism | |
| IAB23-4 | Catholicism | |
| IAB23-5 | Christianity | |
| IAB23-6 | Hinduism | |
| IAB23-7 | Islam | |
| IAB23-8 | Judaism | |
| IAB23-9 | Latter-Day Saints | |
| IAB23-10 | Pagan/Wiccan | |
| IAB24 | Uncategorized | |
| IAB25 | Non-Standard Content | |
| IAB25-1 | Unmoderated UGC | |
| IAB25-2 | Extreme Graphic/Explicit Violence | |
| IAB25-3 | Pornography | |
| IAB25-4 | Profane Content | |
| IAB25-5 | Hate Content | |
| IAB25-6 | Under Construction | |
| IAB25-7 | Incentivized | |
| IAB26 | Illegal Content | |
| IAB26-1 | Illegal Content | |
| IAB26-2 | Warez | |
| IAB26-3 | Spyware/Malware | |
| IAB26-4 | Copyright Infringement | |


## 5.2 Banner 广告类型

下表展示了除被展示者站点设置限制的交易平台可以接受的广告类型。

| 值 | 描述 |
| --- | --- |
| 1 | XHTML 文本广告（通常用于移动手机）|
| 2 | XHTML Banner 广告 （通常用于移动手机）|
| 3 | javascript 广告， 必须是合法的XHTML(即用script标签包裹) |
| 4 | iframe广告 |

## 5.3 Creative 属性

下表展示了广告物料属性的标准列表， 用于描述一个被提供的广告或者作为限制提供。

| 值 | 描述 |
| --- | --- |
| 1 | 音频广告（自动播放）|
| 2 | 音频广告 （用户触发）|
| 3 | 可伸展 （自动）|
| 4 | 可伸展 （用户点击触发）|
| 5 | 可伸展 （用户翻转触发）|
| 6 | Banner内视频广告 （自动播放）|
| 7 | Banner内视频广告 （用户触发）|
| 8 | 弹出广告 （例如， 在退出之前，之后或者当退出的时候）|
| 9 | Provocative or Suggestive Imagery |
| 10 | Shaky, Flashing, Flickering, Extreme Animation, Smileys |
| 11 | 调查问卷 |
| 12 | 文本广告 |
| 13 | 用户互动 （比如，嵌入式游戏）|
| 14 | 窗口对话框或弹出提示框 |
| 15 | 具有音频开关按钮 |
| 16 | 广告可以被跳过（例如，片头广告视频的跳过按钮）|

## 5.4 广告位置

下表描述了广告相对于可见范围的位置。表中的**值**继承自IAB QAG. 实现者应当保持与QAG中值同步。

| 值 | 描述 |
| --- | --- |
| 0 | 未知 |
| 1 | Above the Fold |
| 2 | DEPRECATED - May or may not be initially visible depending on screen size/resolution |
| 3 | Below the Fold |
| 4 | Header |
| 5 | Footer |
| 6 | Sidebar |
| 7 | Full Screen |


## 5.5 伸展方向

下表罗列了一个可伸展广告可以伸展的方向，考虑了广告单元在页面汇总的位置以及被内容的限制。

| 值 | 描述 |
| --- | --- |
| 1 | Left |
| 2 | Right |
| 3 | Up |
| 4 | Down |
| 5 | Full Screen |

## 5.6 API 框架
下表罗列了展示者支持的API框架。 注意MRAID-1是MRAID-2的子集。在OpenRTB2.1及之前版本，“3”对应的是"MRAID", 然而并不是所有MARID兼容的API可以理解MRAID-2的特性，所以最安全的方式是将3理解为MRAID-1.在OpenRTB2.2中， 该值已经被显式标明了， MRAID-2也使用值5被加入。

| 值 | 描述 |
| --- | --- |
| 1 | VPAID 1.0 |
| 2 | VPAID 2.0 |
| 3 | MARID-1 |
| 4 | ORMMA |
| 5 | MRAID-2 |

## 5.7 视频 Linearity
下表描述了视频 linearity的选项， “in-stream" 或者 ”linear" 表示在视频开始，中间或者结束插入的视频广告， 用户被强制观看广告内容。 “overlay"或者”non-linear"指那种在视频内容之上的广告。

这个实行是可选的， 竞拍者可以根据其是否在竞价请求中出现按照如下规则解析：
- 如果该值没有被设置， 任何广告（不管是否是linear)都可以在竞价响应中出现。
- 如果被设置了，仅指定类型的关高可以在竞价响应中出现。

读者需要注意：该表中的值继承自IAB QAG.实现者应当与最新的QAG值保持一致。

| 值 | 描述 |
| --- | --- |
| 1 | Linear/in-stream |
| 2 | Non-Linear/Overlay |

## 5.8 视频竞价响应协议

下表罗列了交易平台需要支持的视频广告竞价响应协议。

| 值 | 描述 |
| --- | --- |
| 1 | VAST 1.0 |
| 2 | VAST 2.0 |
| 3 | VAST 3.0 |
| 4 | VAST 1.0 Wrapper |
| 5 | VAST 2.0 Wrapper |
| 6 | VAST 3.0 Wrapper |

## 5.9 视频播放方式

下表罗列了不同种类的视频播放方式

| 值 | 描述 |
| --- | --- |
| 1 | 自动播放（有声）|
| 2 | 自动播放 （静音）|
| 3 | 点击播放 |
| 4 | 鼠标经过播放 |

## 5.10 视频播放延时

下表罗列了视频播放延时的各种选项。如果播放延时值大于0， 表示视频中广告且该值表示广告开始播放的延时。

| 值 | 描述 |
| --- | --- |
| >0 | 视频中广告，值表示广告播放延时，以秒为单位 |
| 0 | 视频前广告 |
| -1 | 普通视频中广告 |
| -2 | 普通视频后广告 |

## 5.11 视频质量

下表罗列了视频质量选项。这些值在IAB的[long-form-video-final.pdf](http://www.iab.net/media/file/long-form-video-final.pdf)中有定义。

| 值 | 描述 |
| --- | --- |
| 0 | 未知 |
| 1 | Professionally Produced 专业制作 |
| 2 | Prosumer 专业级 |
| 3 | User Generated (UGC) 用户生成 |

## 5.12 VAST 伴随类型
下表罗列了允许的视频伴随广告的类型。表格继承自IAB VAST2.0+, 更多信息参考[www.iab.net/vast](http://www.iab.net/vast).

| 值 | 描述 |
| --- | --- |
| 1 | 静态资源 |
| 2 | HTML资源 |
| 3 | iframe资源 |

## 5.13 内容传输方式
下表罗列了视频内容传输的不同方式。

| 值 | 描述 |
| --- | --- |
| 1 | Streaming |
| 2 | Progressive |

## 5.14 内容上下文

下表罗列了广告可能出现的内容类型选项。
该表继承自QAG,实现者应当与QAG的相关描述保持一致。

| 值 | 描述 |
| --- | --- |
| 1 | 视频（一个别用户观看的视频文件或者视频流， 包括网络电视广播）|
| 2 | 游戏 (用户正在玩的游戏）|
| 3 | 音乐 （一个用户正在听的音频文件或者音频流， 包括网络无线广播）|
| 4 | 应用 （用户正在使用的交互式软件） |
| 5 | 文本 （用户正在浏览或者阅读的文本文档， 包括web页面，电子书或者新闻文章 |
| 6 | 其他 （其他用户正在消费的位置类型的内容） |
| 7 | 未知 |

## 5.15 QAG 媒体级别

下表罗列了基于QAG的媒体内容级别。详细信息参考[http://www.iab.net/ne_guidelines](http://www.iab.net/ne_guidelines).

| 值 | 描述 |
| --- | --- |
| 1 | 所有受众|
| 2 | 大于12岁 |
| 3 | 成年人 |

## 5.16 位置类型

下表罗列了位置信息来源相关的选项。

| 值 | 描述 |
| --- | --- |
| 1 | GPS/定位服务 |
| 2 | IP地址 |
| 3 | 用户提供 （例如注册信息） |

## 5.17 设备类型

下表罗列了广告展示所在的视频类型。

OpenRTB规范版本2.2区分了手机和平板， 建议任何竞价者添加对2.2的支持， 可以将1等价4&5解析。
该表继承自QAG,实现者应当与QAG的相关描述保持一致。

| 值 | 描述 | 备注 |
| --- | --- | --- |
| 1 | 手机/平板 | Version 2.0 |
| 2 | 个人电脑 | Version 2.0 |
| 3 | 联网电视 | Version 2.0 |
| 4 | 手机 | New for Version 2.2 |
| 5 | 平板 | New for Version 2.2 |
| 6 | 联网设备 | New for Version 2.2 |
| 7 | 机顶盒 | New for Version 2.2 |

## 5.18 Connection Type

下表罗列了设备网络连接方式的各种选项。

| 值 | 描述 |
| --- | --- |
| 0 | 未知 |
| 1 | Ethernet以太网 |
| 2 | WIFI |
| 3 | 移动网络，未知类型 |
| 4 | 移动网络-2G |
| 5 | 移动网络-3G |
| 6 | 移动网络-4G |

## 5.19 No-Bid Reason Codes

下表罗列了竞拍者不能为交易平台的展示请求提供广告的原因类型。
| 值 | 描述 | 中文释义 |
| --- | --- | --- | 
| 0 | Unknown Error | 未知错误 |
| 1 | Technical Error | 技术错误 |
| 2 | Invalid Request | 非法请求 |
| 3 | Known Web Spider | 已知的网络爬虫 |
| 4 | Suspected Non-Human Traffic | 怀疑非人为请求 | 
| 5 | Cloud, Data Center, or Proxy IP | 来自云，数据中心或者代理的IP |
| 6 | Unsupported Device | 不支持的设备类型 | 
| 7 | Blocked Publisher or Site | 来自受限展示者或站点 | 
| 8 | Unmatched User | 用户不匹配 |

# 6. 竞价请求/响应 示例
## 6.1 Github 仓库地址

官方的OpenRTB Github仓库地址现在包括一系列已经验证的请求示例，实现者可以在实现协议的时候作为参考。
[https://github.com/openrtb/examples](https://github.com/openrtb/examples)

## 6.2 验证器

OpenRTB提供了一个用于验证请求及响应json是否是有效openrtb请求或响应json的库.源文档给出的链接已经不能使用（404），可能的Github地址如下：
[https://github.com/openrtb/openrtb2x/tree/2.0/openrtb-validator](https://github.com/openrtb/openrtb2x/tree/2.0/openrtb-validator)

## 6.3 竞价请求 
### 6.3.1 Banner请求示例

以下是一个Banner广告的竞价请求示例，示例中也包含了一些可选参数。

```
{
    "id": "80ce30c53c16e6ede735f123ef6e32361bfc7b22",
    "at": 1,
    "cur": [
        "USD"
    ],
    "imp": [
        {
            "id": "1",
            "bidfloor": 0.03,
            "banner": {
                "h": 250,
                "w": 300,
                "pos": 0
            }
        }
    ],
    "site": {
        "id": "102855",
        "cat": [
            "IAB3-1"
        ],
        "domain": "www.foobar.com",
        "page": "http://www.foobar.com/1234.html ",
        "publisher": {
            "id": "8953",
            "name": "foobar.com",
            "cat": [
                "IAB3-1"
            ],
            "domain": "foobar.com"
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/537.13
(KHTML, like Gecko) Version/5.1.7 Safari/534.57.2",
        "ip": "123.145.167.10"
    },
    "user": {
        "id": "55816b39711f9b5acf3b90e313ed29e51665623f"
    }
}

```

### 6.3.2 可伸展广告物料

本示例是第一个示例的改进版，增加了一些用于描述可伸展广告物料支持的参数， 并使用“Data Provider 1"传输用户相关的信息。

```
{
    "id": "123456789316e6ede735f123ef6e32361bfc7b22",
    "at": 2,
    "cur": [
        "USD"
    ],
    "imp": [
        {
            "id": "1",
            "bidfloor": 0.03,
            "iframebuster": [
                "vendor1.com",
                "vendor2.com"
            ],
            "banner": {
                "h": 250,
                "w": 300,
                "pos": 0,
                "battr": [
                    13
                ],
                "expdir": [
                    2,
                    4
                ]
            }
        }
    ],
    "site": {
        "id": "102855",
        "cat": [
            "IAB3-1"
        ],
        "domain": "www.foobar.com",
        "page": "http://www.foobar.com/1234.html",
        "publisher": {
            "id": "8953",
            "name": "foobar.com",
            "cat": [
                "IAB3-1"
            ],
            "domain": "foobar.com"
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/537.13
(KHTML, like Gecko) Version/5.1.7 Safari/534.57.2",
        "ip": "123.145.167.10"
    },
    "user": {
        "id": "55816b39711f9b5acf3b90e313ed29e51665623f",
        "buyeruid": "545678765467876567898765678987654",
        "data": [
            {
                "id": "6",
                "name": "Data Provider 1",
                "segment": [
                    {
                        "id": "12341318394918",
                        "name": "auto intenders"
                    },
                    {
                        "id": "1234131839491234",
                        "name": "auto enthusiasts"
                    },
                    {
                        "id": "23423424",
                        "name": "data-provider1-age",
                        "value": "30-40"
                    }
                ]
            }
        ]
    }
}
```

### 6.3.3 手机信息

本示例使用Device对象来描述移动手机设备， 以及一个App对象来描述该请求所来自的移动端应用。

```
{
    "id": "IxexyLDIIk",
    "at": 2,
    "bcat": [
        "IAB25",
        "IAB7-39",
        "IAB8-18",
        "IAB8-5",
        "IAB9-9"
    ],
    "badv": [
        "apple.com",
        "go-text.me",
        "heywire.com"
    ],
    "imp": [
        {
            "id": "1",
            "bidfloor": 0.5,
            "instl": 0,
            "tagid": "agltb3B1Yi1pbmNyDQsSBFNpdGUY7fD0FAw",
            "banner": {
                "w": 728,
                "h": 90,
                "pos": 1,
                "btype": [
                    4
                ],
                "battr": [
                    14
                ],
                "api": [
                    3
                ]
            }
        }
    ],
    "app": {
        "id": "agltb3B1Yi1pbmNyDAsSA0FwcBiJkfIUDA",
        "name": "Yahoo Weather",
        "cat": [
            "IAB15",
            "IAB15-10"
        ],
        "ver": "1.0.2",
        "bundle": "com.yahoo.wxapp",
        "storeurl": "https://itunes.apple.com/id628677149",
        "publisher": {
            "id": "agltb3B1Yi1pbmNyDAsSA0FwcBiJkfTUCV",
            "name": "yahoo",
            "domain": "www.yahoo.com"
        }
    },
    "device": {
        "dnt": 0,
        "ua": "Mozilla/5.0 (iPhone; CPU iPhone OS 6_1 like Mac OS X)
AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9A334 Safari/7534.48.3",
        "ip": "123.145.167.189",
        "ifa": "AA000DFE74168477C70D291f574D344790E0BB11",
        "carrier": "VERIZON",
        "language": "en",
        "make": "Apple",
        "model": "iPhone",
        "os": "iOS",
        "osv": "6.1",
        "js": 1,
        "connectiontype": 3,
        "devicetype": 1,
        "geo": {
            "lat": 35.012345,
            "lon": -115.12345,
            "country": "USA",
            "metro": "803",
            "region": "CA",
            "city": "Los Angeles",
            "zip": "90049"
        }
    },
    "user": {
        "id": "ffffffd5135596709273b3a1a07e466ea2bf4fff",
        "yob": 1984,
        "gender": "M"
    }
}
```

### 6.3.4 视频广告示例

以下示例展示了一个包含两个附加广告（其中一个可伸展）的视频广告展示， 此外， 视频内容本身在"content"对象中描述，对于本示例一些特殊需要注意的点如下：

- **protocol:** 仅VAST2.0和VAST3.0允许。
- **sequence:** 没有被指定，所以默认为1.
- **battr:** 对于视频以及它的附加广告， 用户交互以及提示型广告（分别是13和14）被显式的限制。
- **pos:** 展示了本次展示是“在内容之上”的广告。
- **api:** 标识VPAID 1.0容器被显式支持。因此，VPAID支持的 mime-type仅仅是"application/x-shockwave-flash"以及“application/javascript".需要注意有一个隐式的限制是对于不同的mime-type有哪些类型的协议是允许的。Javascript支持在VPAID2.0之前是没有指定的， 而VPAID1.0和2.0都支持Flash.
- **companiontype:** 标识只有静态和HTML资源被允许。

```
{
    "id": "1234567893",
    "at": 2,
    "tmax": 120,
    "imp": [
        {
            "id": "1",
            "bidfloor": 0.03,
            "video": {
                "w": 640,
                "h": 480,
                "pos": 1,
                "startdelay": 0,
                "minduration": 5,
                "maxduration": 30,
                "maxextended": 30,
                "minbitrate": 300,
                "maxbitrate": 1500,
                "api": [
                    1,
                    2
                ],
                "protocols": [
                    2,
                    3
                ],
                "mimes": [
                    "video/x-flv",
                    "video/mp4",
                    "application/x-shockwave-flash",
                    "application/javascript"
                ],
                "linearity": 1,
                "boxingallowed": 1,
                "playbackmethod": [
                    1,
                    3
                ],
                "delivery": [
                    2
                ],
                "battr": [
                    13,
                    14
                ],
                "companionad": [
                    {
                        "id": "1234567893-1",
                        "w": 300,
                        "h": 250,
                        "pos": 1,
                        "battr": [
                            13,
                            14
                        ],
                        "expdir": [
                            2,
                            4
                        ]
                    },
                    {
                        "id": "1234567893-2",
                        "w": 728,
                        "h": 90,
                        "pos": 1,
                        "battr": [
                            13,
                            14
                        ]
                    }
                ],
                "companiontype": [
                    1,
                    2
                ]
            }
        }
    ],
    "site": {
        "id": "1345135123",
        "name": "Site ABCD",
        "domain": "siteabcd.com",
        "cat": [
            "IAB2-1",
            "IAB2-2"
        ],
        "page": "http://siteabcd.com/page.htm",
        "ref": "http://referringsite.com/referringpage.htm",
        "privacypolicy": 1,
        "publisher": {
            "id": "pub12345",
            "name": "Publisher A"
        },
        "content": {
            "id": "1234567",
            "series": "All About Cars",
            "season": "2",
            "episode": 23,
            "title": "Car Show",
            "cat": [
                "IAB2-2"
            ],
            "keywords": "keyword-a,keyword-b,keyword-c"
        }
    },
    "device": {
        "ip": "64.124.253.1",
        "ua": "Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.6; en-US; rv:1.9.2.16)
Gecko/20110319 Firefox/3.6.16",
        "os": "OS X",
        "flashver": "10.1",
        "js": 1
    },
    "user": {
        "id": "456789876567897654678987656789",
        "buyeruid": "545678765467876567898765678987654",
        "data": [
            {
                "id": "6",
                "name": "Data Provider 1",
                "segment": [
                    {
                        "id": "12341318394918",
                        "name": "auto intenders"
                    },
                    {
                        "id": "1234131839491234",
                        "name": "auto enthusiasts"
                    }
                ]
            }
        ]
    }
}
```

### 6.3.5 带有直接交易规则的私有广告市场

以下是一个带有直接交易规则的Banner广告竞价请求示例，其中包含了一些可选参数。

```
{
    "id": "80ce30c53c16e6ede735f123ef6e32361bfc7b22",
    "at": 1,
    "cur": [
        "USD"
    ],
    "imp": [
        {
            "id": "1",
            "bidfloor": 0.03,
            "banner": {
                "h": 250,
                "w": 300,
                "pos": 0
            },
            "pmp": {
                "private_auction": 1,
                "deals": [
                    {
                        "id": "AB-Agency1-0001",
                        "at": 1,
                        "bidfloor": 2.5,
                        "wseat": [
                            "Agency1"
                        ]
                    },
                    {
                        "id": "XY-Agency2-0001",
                        "at": 2,
                        "bidfloor": 2,
                        "wseat": [
                            "Agency2"
                        ]
                    }
                ]
            }
        }
    ],
    "site": {
        "id": "102855",
        "domain": "www.foobar.com",
        "cat": [
            "IAB3-1"
        ],
        "page": "http://www.foobar.com/1234.html",
        "publisher": {
            "id": "8953",
            "name": "foobar.com",
            "cat": [
                "IAB3-1"
            ],
            "domain": "foobar.com"
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/537.13
(KHTML, like Gecko) Version/5.1.7 Safari/534.57.2",
        "ip": "123.145.167.10"
    },
    "user": {
        "id": "55816b39711f9b5acf3b90e313ed29e51665623f"
    }
}
```

### 6.3.6 原生广告

以下是一个Native广告的竞价请求示例， 与6.3.1节描述的请求示例有点像，需要注意的是`native`对象中的`request`属性包含的是一个已编码的native广告请求字符串。字符串的具体格式需要符合Native广告请求规范，`ver`属性指明了Naitve广告符合的规范版本是1.0.

```
{
    "id": "80ce30c53c16e6ede735f123ef6e32361bfc7b22",
    "at": 1,
    "cur": [
        "USD"
    ],
    "imp": [
        {
            "id": "1",
            "bidfloor": 0.03,
            "native": {
                "request": "...Native Spec request as an encoded string...",
                "ver": "1.0",
                "api": [
                    3
                ],
                "battr": [
                    13,
                    14
                ]
            }
        }
    ],
    "site": {
        "id": "102855",
        "cat": [
            "IAB3-1"
        ],
        "domain": "www.foobar.com",
        "page": "http://www.foobar.com/1234.html ",
        "publisher": {
            "id": "8953",
            "name": "foobar.com",
            "cat": [
                "IAB3-1"
            ],
            "domain": "foobar.com"
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/537.13
(KHTML, like Gecko) Version/5.1.7 Safari/534.57.2",
        "ip": "123.145.167.10"
    },
    "user": {
        "id": "55816b39711f9b5acf3b90e313ed29e51665623f"
    }
}
```

## 6.4 竞价响应
### 6.4.1 在胜出通知响应中返回的广告内容。

以下展示了在胜出通知响应中返回的竞价响应， 对于该次展示的竞拍价格是$9.43 CPM.

```
{
    "id": "1234567890",
    "bidid": "abc1123",
    "cur": "USD",
    "seatbid": [
        {
            "seat": "512",
            "bid": [
                {
                    "id": "1",
                    "impid": "102",
                    "price": 9.43,
                    "nurl": "http://adserver.com/winnotice?impid=102",
                    "iurl": "http://adserver.com/pathtosampleimage",
                    "adomain": [
                        "advertiserdomain.com"
                    ],
                    "cid": "campaign111",
                    "crid": "creative112",
                    "attr": [
                        1,
                        2,
                        3,
                        4,
                        5,
                        6,
                        7,
                        12
                    ]
                }
            ]
        }
    ]
}
```

### 6.4.2 VAST XML Document Returned Inline

以下是返回VAST文档格式的广告竞价响应示例。示例中需要注意的点如下：

- 展示的竞拍价格是￥3.00CPM
- Note that since there both a win notice URL and an inline VAST document in the adm attribute, which constitutes the ad markup. The win notice is still called, but if it were to return markup it would be ignored in favor of the contents of the adm attribute

```
{
    "id": "123",
    "seatbid": [
        {
            "bid": [
                {
                    "id": "12345",
                    "impid": "2",
                    "price": 3,
                    "nurl": "http://example.com/winnoticeurl",
                    "adm": "%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-
8%22%3F%3E%0A%3CVAST%20version%3D%222.0%22%3E%0A%20%20%20%20%3CAd%20id%3D%2212345%22
%3E%0A%20%20%20%20%20%20%20%20%3CInLine%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%3C
AdSystem%20version%3D%221.0%22%3ESpotXchange%3C%2FAdSystem%3E%0A%20%20%20%20%20%20%2
0%20%20%20%20%20%20%20%20%20%3CAdTitle%3E%3C!%5BCDATA%5BSample%20VAST%5D%5D%3E%3C%2F
AdTitle%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3CImpression%3Ehttp%3A
%2F%2Fsample.com%3C%2FImpression%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%
20%3CDescription%3E%3C!%5BCDATA%5BA%20sample%20VAST%20feed%5D%5D%3E%3C%2FDescription
%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3CCreatives%3E%0A%20%20%20%20
%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3CCreative%20sequence%3D%221%22%20i
d%3D%221%22%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%
20%20%3CLinear%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%
20%20%20%20%20%20%20%3CDuration%3E00%3A00%3A30%3C%2FDuration%3E%0A%20%20%20%20%20%20
%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3CTrackingEvents%
3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%
20%20%3C%2FTrackingEvents%3E%20%20%20%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%2
0%20%20%20%20%20%20%20%20%20%20%20%20%20%3CVideoClicks%3E%0A%20%20%20%20%20%20%20%20
%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3CClickThro
ugh%3E%3C!%5BCDATA%5Bhttp%3A%2F%2Fsample.com%2Fopenrtbtest%5D%5D%3E%3C%2FClickThroug
h%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%2
0%20%20%3C%2FVideoClicks%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20
%20%20%20%20%20%20%20%20%20%20%3CMediaFiles%3E%0A%20%20%20%20%20%20%20%20%20%20%20%2
0%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3CMediaFile%20delivery
%3D%22progressive%22%20bitrate%3D%22256%22%20width%3D%22640%22%20height%3D%22480%22%
20type%3D%22video%2Fmp4%22%3E%3C!%5BCDATA%5Bhttp%3A%2F%2Fsample.com%2Fvideo.mp4%5D%5
D%3E%3C%2FMediaFile%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%2
0%20%20%20%20%20%20%20%20%3C%2FMediaFiles%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%
20%20%20%20%20%20%20%20%20%20%20%20%3C%2FLinear%3E%0A%20%20%20%20%20%20%20%20%20%20%
20%20%20%20%20%20%20%20%20%20%3C%2FCreative%3E%0A%20%20%20%20%20%20%20%20%20%20%20%2
0%20%20%20%20%3C%2FCreatives%3E%0A%20%20%20%20%20%20%20%20%3C%2FInLine%3E%0A%20%20%2
0%20%3C%2FAd%3E%0A%3C%2FVAST%3E"
                }
            ]
        }
    ]
}
```

### 6.4.3 Direct Deal Ad Served on Win Notice

以下示例展示了一个在胜出通知响应中提供广告内容的竞价响应。 此次展示的竞标价格是$5.00 CPM, 且依赖一个直接交易规则。

```
{
    "id": "1234567890",
    "bidid": "abc1123",
    "cur": "USD",
    "seatbid": [
        {
            "seat": "512",
            "bid": [
                {
                    "id": "1",
                    "impid": "102",
                    "price": 5,
                    "dealid": "ABC-1234-6789",
                    "nurl": "http: //adserver.com/winnotice?impid=102",
                    "adomain": [
                        "advertiserdomain.com"
                    ],
                    "iurl": "http: //adserver.com/pathtosampleimage",
                    "cid": "campaign111",
                    "crid": "creative112",
                    "adid": "314",
                    "attr": [
                        1,
                        2,
                        3,
                        4
                    ]
                }
            ]
        }
    ]
}
```

### 6.4.4 直接在竞价请求中返回原生广告

以下是一个返回Native广告的竞价响应，`adm`属性包含了一个Native广告竞价响应的字符串，该字符串的内容需符合Native广告OpenRTB规范。 另外， 如果广告内容是在胜出通知的响应中提供的话， 就可以不提供`adm`属性。

# 7. 实现注意事项

以下部分会简要介绍某些特定的对象和域是如何被解析以及实现的。

## 7.1 COPPA Regulation Flag

美国联邦交易委员会已经修改了儿童在线隐私保护法案的规则， 从2013年7月1日起生效。该提议对网站和相关的服务进行了明确的分类，如下：
- 直接面向低于13岁的用户。
- 从低于13岁的群体的用户收集信息。

联邦委员会同时撰写了一个便于理解的FAQ, 你可以在这里找到：
[http://business.ftc.gov/documents/Complying-with-COPPA-Frequently-Asked-Questions](http://business.ftc.gov/documents/Complying-with-COPPA-Frequently-Asked-Questions)

联邦委员会的CTO, Steve Bellovin, 在2013年1月发表了一片博文， 主张为该协议建立一套统一的标准， 你可以在这里找到(翻译时本文已经被删除)：
[https://techatftc.wordpress.com/2013/01/02/coppa-and-signaling/](https://techatftc.wordpress.com/2013/01/02/coppa-and-signaling/)

**影响**

FAQ中也特别指出在OpenRTB中指明是“个人信息”的相关领域信息也不能被收集。
- 足够确认街道名称或者城市名称的地理位置信息。
- 可以跨站点或者在线服务能够长时间稳定识别用户的信息。

**实现者建议**

OpenRTB的交易平台和竞价者应当：
- 为站点提供设施，让他们能标识自己是“直接面向儿童的”。
- 实现规则对象扩展。
- 在广告活动中提供设施来标明其是否是针对儿童。
- 降低地理位置信息的精确度，仅仅用于支持日志或者数据传输。
- 根据使用状况合理控制用户标识的提取和同步。

## 7.2 PMP & Direct Deals
## 7.3 No-Bid Signaling

# 附录A. 附加信息
# 附录B. 规范版本更新日志
