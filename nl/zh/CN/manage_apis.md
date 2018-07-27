---

copyright:
  years: 2017,2018
lastupdated: "2018-03-28"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理 API
{: #manage_apis}

集成 API 以使其由 API Management 系统进行管理和监视后，可以查看和修改 API 设置。如果尚未集成 API，那么必须完成[通过 {{site.data.keyword.openwhisk_short}} 操作创建 API](manage_openwhisk_apis.html) 或[启用 API 受管端点](manage_cf_apis.html)中的过程来集成 API。 

要管理 API 的设置，请完成以下步骤：

如果已创建新的 API，并且已在界面中打开该 API，那么可以跳过前三个步骤。

1. 如果要管理的 API 的信息尚未显示，请通过 {{site.data.keyword.Bluemix}} 仪表板或选择 {{site.data.keyword.openwhisk_short}} 服务仪表板上的操作来选择该 API。
2. 在导航中单击 **API 管理**，或者选择 **API** 选项卡（如果其为 {{site.data.keyword.openwhisk_short}} 操作）。
3. 根据需要，选择要管理的 API。建立连接后，您可查看和更新以下选项：
    * 摘要
    * 定义
    * 共享
    * API Explorer
4. 选择“公开受管 API”滑块以激活该项并公开 API。注：API 未公开时，无法设置某些设置。  

## API 设置摘要
{: #overview_api}

选择 API 时，缺省情况下会选择“摘要”选项卡，该选项卡分为两个部分：
* 属性 - 在“属性”部分中，可以查看以下信息：
    * 关于 API 的基本信息
	* 安全策略
	* 速率限制信息
    * 共享详细信息
* “分析和日志记录”部分 - 在“分析和日志记录”部分中，可以查看以下统计信息：
	* 上一个指定时间间隔内的响应数和平均响应时间
    * 图格式的每分钟 API 调用数
    * “响应日志”表中的最近 100 个响应
	
*响应*图显示了 API 收到的响应数和响应状态细目的情况速览。这可帮助您确定收到的响应中是否绝大多数是错误响应。如果绝大多数是错误响应，可能指示您的流量高于速率设置中允许的流量。您可以通过将鼠标悬停在信息图标上，按响应代码查看响应的数字细目。下面是常见的响应代码：
* 200  正常
* 201  已创建
* 302  已找到
* 304  未修改
* 400  请求错误
* 401  未授权
* 403  已禁止
* 500  内部服务器错误
* 503  服务不可用

“响应日志”表包含最近 100 个响应中每个响应的详细信息。可以通过选择列标题以根据列中的条目对信息排序。您可以使用*搜索响应*栏，在“响应日志”表中搜索特定条目。通过选择事件，或通过选择条目旁选项菜单（三个纵向点）列表中的**查看详细信息**，可查看该事件的更多信息。


## 编辑 API 设置
{: #settings_api}

在**定义**选项卡中，可以更新有关 API 的基本信息。这些信息包括文档、名称和基本 URL。使用“安全性和速率限制”部分可指定调用和时间间隔限制，以确保每秒、每分钟或每小时只发起特定数量的调用。您还可以要求认证才能创建 API 调用，以避免不恰当地使用您的数据，或收集有关 API 的统计信息。

要更改 API 的设置，请完成以下步骤：

1. 在 API Management 仪表板中，单击**定义**选项卡。
2. 可以对 API 命名或更新其名称，然后在“API 信息”部分中导入 API 定义。
3. 在“安全性和速率限制”部分中，可以更新以下策略：
    * 需要 API 密钥 - 指定是否仅当提供正确的 API 密钥时，才能处理 API 调用。缺省设置是不需要其他密钥。
    * 安全方法 - 选择了 API 密钥选项时，指定处理 API 是仅需要 API 密钥，还是同时需要 API 密钥和 API 私钥。
    * API 密钥和私钥的位置 - 根据方法的设置，指定 API 安全信息如何包含在调用中。调用名称指定如何识别安全信息。有关使用密钥和私钥的更多信息，请参阅[管理密钥和私钥](keys_secrets.html)。
    * 限制 API 调用速率 - 设置在指定时间间隔内允许的 API 调用数，可选择为每个密钥设置此项。请注意，这将使用脉冲串传输类型的速率限制方法。API 调用平均速率是基于在速率中指定的总时间间隔计算的。如果某个时间间隔内的 API 调用速率超过 API 调用平均速率，那么在速率中指定的时间限制之前，可能会出现拒绝调用的时间段。   
    * OAuth 提供者 - 确保具有正确安全参数的用户可以通过提供者（例如，Google、Facebook、IBM App ID 和 GitHub）的社交登录凭证强制实施 OAuth 来访问 API。**注：**必须指定在 {{site.data.keyword.Bluemix_notm}} 中配置的现有 App ID 服务实例，才能在将 **App ID** 用作 OAuth 提供者时提供标识数据。如果没有现有的 App ID 服务，那么可以在 OAuth 部分中选择**创建**以在新窗口中创建 App ID 服务，然后返回以将其指定用于 API Management。此外，还可以选择**编辑**来更改所选服务实例。
4. 启用 CORS - 跨源请求 (CORS) 支持来自其他域的一些有限请求。
5. 单击**保存**。

## 共享 API
{: #share_api}

您可以与 {{site.data.keyword.Bluemix_notm}} 组织内部或外部的其他用户共享 API。 

与 {{site.data.keyword.Bluemix_notm}} 组织内部或外部的其他人共享 API 时，可以为 API 创建密钥和私钥。每个受管 API 支持创建 5 个密钥并将其分配给该 API。通过向个人或公司发送唯一密钥，可以跟踪有关该 API 使用情况的一些统计信息。例如，可以跟踪该人员或公司对 API 的调用数。您还可以禁用某个密钥或限制来自某个密钥的调用。这在测试、均衡工作负载和计算费用期间或用于解决某些安全情况时，会非常有用。

*密钥*是与 API 关联的唯一字符串。您可以将多个密钥分配给一个 API，以帮助您跟踪每位客户对该 API 的使用情况。例如，您为一个客户提供了一个密钥，为另一个客户提供了另一个密钥。客户每次调用 API 时，都会包含分配给自己的密钥。通过跟踪该密钥，您就知道哪个客户调用了该 API。

有两种类型的密钥：

* 用于与有权访问 {{site.data.keyword.Bluemix_notm}} 组织的客户共享 API 的密钥。 
* 用于与无权访问 {{site.data.keyword.Bluemix_notm}} 组织的客户共享 API 的密钥。 

不同类型的密钥采用相同的方式来创建、维护和删除。唯一的区别是能够使用密钥的对象不同。

为 API 创建一个或多个密钥后，可以按密钥限制对 API 的调用速率。通过在*定义*选项卡上启用**按密钥限制 API 调用速率**滑块，可将创建的每个密钥的调用次数限制为您设置的速率限制。   

*私钥*与密钥类似，用于维护对 API 本身的访问权。私钥是可定制的，并可以在不更改密钥的情况下进行更改。如果没有密钥，就不可能有私钥。例如，只有具有正确私钥的人才能上传新版本的 API。您可以要求将 API 密钥和私钥用于 API 调用，或者只使用密钥。如果需要更改私钥，但不想更改密钥，那么私钥会非常有用。 

1. 在 API Management 仪表板中，单击**共享**选项卡。
2. 如果希望 API 可供有权访问 {{site.data.keyword.Bluemix_notm}} 组织的其他人使用，请在“在 {{site.data.keyword.Bluemix_notm}} 组织内共享”区域中，选择**公开受管 API**。必须选择此项才能生成密钥。
3. 单击**创建 API 密钥**来为 API 创建唯一密钥。这将显示“创建 API 密钥”对话框。API 密钥会自动生成。
4. 使用 API 密钥可通过向用户发送唯一密钥来确定哪个用户在访问该 API。网关可以确定哪个密钥（和客户）在生成调用。
5. 单击密钥旁的**菜单**图标（三个纵向点）可“编辑”或“删除”该 API 密钥。

在“在 {{site.data.keyword.Bluemix_notm}} 组织外部共享”部分中，可以将 API 与没有 {{site.data.keyword.Bluemix_notm}} 帐户的用户共享。此共享方法提供了一个直接链接，用于在 API Explorer 中查看有关 API 的信息。在 API Explorer 视图中，API 包含一个用于运行该 API 的按钮。要请求 API 的链接，请完成以下步骤：

1. 在“在 {{site.data.keyword.Bluemix_notm}} 组织外部共享”部分中，单击**创建 API 密钥**。这将显示“创建 API 密钥”对话框。请注意，用户具有您无法控制的私钥。
2. 为 API 密钥提供唯一名称。
3. 选择**创建密钥**。 
4. 将 API 门户网站链接发送给没有 {{site.data.keyword.Bluemix_notm}} 帐户的客户。该 API 密钥和私钥（如果使用）会包含在链接中，所以您仍可以确定哪个密钥生成了链接。
  
API 文档链接会在 **API Explorer** 选项卡中打开 API。

有关使用密钥和私钥的更多信息，请参阅[管理密钥和私钥](keys_secrets.html)。

## 使用 API Explorer 查看和测试
{: #explore_api}

选择 API Explorer 选项卡，以查看从 Swagger 文档生成的 HTML。 

API Explorer 会显示适用于 API 的所有 API 操作和文档。可以在 UI 中查看操作、其描述，并可测试 API。还可以下载 Swagger 文档以复用其内容。

要测试 API，请完成以下步骤：
1. 缺省情况下已选择*示例*。这将显示所选 API 的代码示例。
2. 根据需要，通过从指定语言旁的菜单中选择语言来更改示例格式。 
3. 选择**试试看**。
4. 选择**调用操作**。 

这将显示对请求的响应。 

## 定制域
{: #custom_domains}

在某些情况下，您可能需要定制域或“空”域，而不使用 API 网关的缺省域。只要定制域在 {{site.data.keyword.Bluemix_notm}} 环境中注册后，API Management 功能就支持将该域放在 API 前端。

完成以下步骤以初始设置定制域。如果先前完成了设置域的步骤，请参阅[将定制域用于 API](manage_apis.html#custom_domains_bind)。

### 设置

要将定制域放在 API 前端，请先向 {{site.data.keyword.Bluemix_notm}} 注册域。这可以通过“组织管理”屏幕来完成：

1. 在 {{site.data.keyword.Bluemix_notm}} 标题中的组织选择器中，选择**管理组织**。
2. 找到应该在其中注册域的所需组织，然后选择**查看详细信息**。
3. 单击组织名称旁边的**编辑组织**链接。
4. 选择**域**选项卡。
5. 单击**添加域**，然后输入域名。
6. 域出现在列表中后，选择屏幕顶部的**保存**。
7. 上传此域的 SSL 证书。这可以通过选择域名旁边的**上传**图标来完成。公用证书和对应的私钥都是必需的。  
	**注：**
	* API Management 网关仅支持基于 HTTPS 协议的流量，因此必须提供 SSL 证书。
	* {{site.data.keyword.Bluemix_notm}} 试用帐户限制为每个组织一个 SSL 证书。如果需要更多证书，您必须将帐户升级到付费或预订层。
	* 如果计划对 API 流量使用一个或多个子域，那么需要通配符证书或包含所需*使用者备用名称* (SAN) 的证书。
8. 配置域的 DNS 设置。 
9. 根据哪个区域托管目标 API，针对以下其中一个安全端点创建域的 CNAME 记录：
	- **美国南部：**secure.us-south.bluemix.net。
	- **英国：**secure.eu-gb.bluemix.net。
	- **法兰克福：**secure.eu-de.bluemix.net。
	- **悉尼：**secure.au-syd.bluemix.net。

### 将定制域用于 API
{: #custom_domains_bind}

初始设置完成后，通过完成以下步骤，将一个或多个 API 绑定到 API 的**定义**部分中的注册域：
1. 在 *API 基本信息*中，选择“API 域”菜单，然后从先前步骤中配置的域中，选择定制域。

2. 可选：为此 API 提供唯一的子域。
	**注**：为了使用子域，在`设置`的步骤 7 中上传的 SSL 证书必须包含有效的通配符配置，*或者*每个子域必须列为使用者备用名称 (SAN)。

3. 保存 API。域设置可能需要几分钟时间才能生效。

有关更多信息，请参阅：[管理域](../admin/manageorg.html#managedomains)或[创建和使用定制域](../manageapps/updapps.html#domain)。