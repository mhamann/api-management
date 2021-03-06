---

copyright:
  years: 2017,2018
lastupdated: "2018-08-23"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理 API
{: #manage_apis}

在您整合 API 以透過 API Management 系統進行管理及監視之後，即可檢視及修改 API 設定。如果您尚未整合 API，則必須完成[從 {{site.data.keyword.openwhisk_short}} 動作建立 API](manage_openwhisk_apis.html) 或[啟用 API 受管理端點](manage_cf_apis.html)中的程序來整合 API。 

若要管理 API 的設定，請完成下列步驟：

如果您已建立新的 API，並且已在介面中開啟它，則可以跳過前三個步驟。

1. 從 {{site.data.keyword.Bluemix}}「儀表板」中選取您要管理的 API，或者，如果尚未顯示 API 的資訊，請在 {{site.data.keyword.openwhisk_short}} 服務「儀表板」上選取動作，以選取您要管理的 API。
2. 按一下導覽中 **API Management**，或者選取 **API** 標籤（如果它是 {{site.data.keyword.openwhisk_short}} 動作）。
3. 選取您要管理的 API（必要的話）。建立連線之後，即可檢視及更新下列選項：
    * 摘要
    * 定義
    * 共用
    * API 瀏覽器
4. 選取「公開受管理 API」調節器來啟動它，並公開您的 API。附註：未公開 API 時，無法設定某些設定。  

## API 設定摘要
{: #overview_api}

「摘要」標籤預設會在您選取 API 時選取且分成兩個區段：
* 內容 - 在「內容」區段中，您可以檢視下列資訊：
    * API 的基本資訊
	* 安全原則
	* 比率限制資訊
    * 共用詳細資料
* 「分析及記載」區段 - 在「分析及記載」區段中，您可以檢視下列統計資料：
	* 最後一個所指定時間間隔期間的回應數目及平均回應時間
    * 每分鐘的 API 呼叫數目，為圖形格式
    * 「回應日誌」表格中的最後 100 個回應
	
*回應* 圖形可快速呈現 API 所收到的回應數目，以及回應狀態的分解。這可協助您判斷是否收到大部分的錯誤回應。大部分的錯誤回應都會指出您的資料流量高於比率設定中所容許的資料流量。將游標移至資訊圖示上方，即可依回應碼來查看回應的數值分解。下列是常見回應碼：
* 200  OK
* 201  Created
* 302  Found
* 304  Not Modified
* 400  Bad Request
* 401  Unauthorized
* 403  Forbidden
* 500  Internal Server Error
* 503  Service Unavailable

「回應日誌」表格包含最後 100 個回應的個別詳細資料。您可以選取直欄標題，以根據直欄中的項目來排序資訊。您可以使用*搜尋回應* 列來搜尋「回應日誌」表格中的特定項目。事件詳細資訊的取得方式是選取它，或在項目旁邊的選項清單功能表（三個垂直點）中選取**檢視詳細資料**。


## 編輯 API 設定
{: #settings_api}

在**定義**標籤中，您可以更新 API 的基本資訊。此資訊包括文件、名稱及基本 URL。使用「安全及比率限制」區段來指定呼叫及間隔限制，確保每秒、每分鐘或每小時只執行特定的呼叫數量。您也需要鑑別才能建立 API 呼叫，以防止不必要的資料使用或收集 API 統計資料。

若要變更 API 的設定，請完成下列步驟：

1. 在 API Management 儀表板中，按一下**定義**標籤。
2. 您可以命名或更新 API 的名稱，以及在「API 資訊」區段中匯入 API 定義。
3. 在「安全及比率限制」區段中，您可以更新下列原則：
    * 需要 API 金鑰 - 指定是否只有在提供正確的 API 金鑰時才能處理 API 呼叫。預設值不需要額外金鑰。
    * 安全方法 - 選取 API 金鑰選項時，指定處理 API 時只需要 API 金鑰，還是同時需要 API 金鑰及 API 密碼。
    * API 金鑰及密碼的位置 - 根據方法的設定，指定如何在呼叫中包括 API 安全資訊。「呼叫名稱」指定如何識別安全資訊。如需使用金鑰和密碼的相關資訊，請參閱[管理金鑰和密碼](keys_secrets.html)。
    * 限制 API 呼叫率 - 設定所指定時間間隔期間容許的 API 呼叫數目，而方法是使用針對每一個金鑰設定它的選項。請注意，會使用 rate-limiting 方法的 burst-type。平均 API 呼叫率是跨比率中所指定的總時間間隔計算而來。如果間隔期間的 API 呼叫速超出平均 API 呼叫率，則拒絕呼叫的期間最高可到比率中所指定的時間限制。   
    * OAuth 提供者 - 確定具有正確安全參數的使用者可以存取 API，而方法是透過提供者（如 Google、Facebook、IBM App ID 及 GitHub）的社交登入認證來強制執行 OAuth。
    **附註：**您必須指定 {{site.data.keyword.Bluemix_notm}} 中已配置的現有 App ID 服務實例，在使用 **App ID** 作為 OAuth 提供者時提供識別資料。如果沒有現有的 App ID 服務，您可以在 OAuth 區段選取**建立**，以在新視窗中建立一個新的 App ID 服務，然後回來為 API Management 指定它。您也可以選取**編輯**，以變更選取的服務實例。
4. 啟用 CORS - 跨原點要求 (CORS) 可啟用來自不同網域的一些有限要求。
5. 按一下**儲存**。

## 共用 API
{: #share_api}

您可以與 {{site.data.keyword.Bluemix_notm}} 組織內外部的其他使用者共用 API。 

當您與 {{site.data.keyword.Bluemix_notm}} 組織內外部的其他人共用 API 時，可以建立 API 的金鑰和密碼。每一個受管理 API 都支援可建立並指派該 API 的 5 個金鑰。將唯一金鑰傳送至個人或公司，以追蹤 API 使用方式的一些統計資料。例如，您可以追蹤該人員或公司的 API 呼叫數目。您也可以停用金鑰，或限制來自金鑰的呼叫數。這在測試、工作負載平衡、定為貨幣或用於處理一些安全狀況期間十分有用。

*金鑰* 是與 API 相關聯的唯一字元字串。您可以指派多個金鑰給 API，其可協助您追蹤每個客戶的 API 使用情形。例如，您可以將一個金鑰提供給一位客戶，而將另一個金鑰提供給另一位客戶。每次客戶呼叫 API 時，他們會包括其已指派的金鑰。透過追蹤該金鑰，您可以知道哪位客戶呼叫 API。

有兩種類型的金鑰：

* 與可存取 {{site.data.keyword.Bluemix_notm}} 組織的客戶共用 API 的金鑰。 
* 與無法存取 {{site.data.keyword.Bluemix_notm}} 組織的客戶共用 API 的金鑰。 

以相同的方式建立、維護及刪除不同類型的金鑰。唯一的差異是誰能夠使用金鑰。

在為您的 API 建立一個以上的金鑰之後，您可將依金鑰來限制 API 的呼叫率。透過啟用*定義* 標籤上的**按每一個金鑰限制 API 呼叫率**調節器，您可將所建立的每個金鑰的呼叫數目限制為所設定的比率限制。   

*密碼* 類似於金鑰，如同用來維護對 API 本身的存取一樣。密碼是可自訂的，且可在不變更金鑰的情況下進行變更。如果沒有金鑰，就不會有密碼。例如，只有具有正確密碼的人才能上傳新版本的 API。您可以為您的 API 呼叫要求一個 API 和一個密碼，或者只使用一個金鑰。如果您需要變更密碼，但不想要變更金鑰，則密碼可能會有所幫助。 

1. 在 API Management 儀表板中，按一下**共用**標籤。
2. 在「在 {{site.data.keyword.Bluemix_notm}} 組織內共用」區域內，如果您要 API 可讓其他人存取您的 {{site.data.keyword.Bluemix_notm}}組織，請選取**公開受管理 API**。必須選取此選項，才能產生金鑰。
3. 按一下**建立 API 金鑰**，以建立 API 的唯一金鑰。隨即會顯示「建立 API 金鑰」對話框。會自動產生 API 金鑰。
4. 使用 API 金鑰，透過傳送使用者的唯一金鑰來判斷哪位使用者正在存取 API。閘道可以判斷哪個金鑰（及客戶）正在產生呼叫。
5. 按一下金鑰旁邊的**功能表**圖示（三個垂直點），以「編輯」或「刪除」該 API 金鑰。

在「在 {{site.data.keyword.Bluemix_notm}} 組織外共用」區段中，您可以與沒有 {{site.data.keyword.Bluemix_notm}} 帳戶的使用者共用 API。這個共用方法提供在「API 瀏覽器」中檢視 API 資訊的直接鏈結。API 包含可在「API 瀏覽器」視圖中執行 API 的按鈕。若要要求 API 的鏈結，請完成下列步驟：

1. 在「在 {{site.data.keyword.Bluemix_notm}} 組織外共用」區段內，按一下**建立 API 金鑰**。隨即會顯示「建立 API 金鑰」對話框。請注意，使用者具有您無法控制的密碼。
2. 提供 API 金鑰的唯一名稱。
3. 選取**建立金鑰**。 
4. 將「API 入口網站鏈結」傳送給沒有 {{site.data.keyword.Bluemix_notm}} 帳戶的客戶。API 金鑰及密碼（如果使用的話）會包括在鏈結中，因此，您仍然可以判斷哪一個金鑰已產生鏈結。
  
API 文件鏈結會在 **API 瀏覽器**標籤中開啟 API。

如需使用金鑰和密碼的相關資訊，請參閱[管理金鑰和密碼](keys_secrets.html)。

## 使用 API 瀏覽器檢視及測試
{: #explore_api}

選取「API 瀏覽器」標籤，以檢視從 Swagger 文件中產生的 HTML。 

「API 瀏覽器」會顯示套用至 API 的所有 API 動作及文件。您可以從使用者介面來檢視作業及動作、其說明，以及測試 API。您也可以下載 Swagger 文件，以重複使用其內容。

若要測試 API，請完成下列步驟：
1. 預設會選取*範例*。這會顯示所選取 API 的程式碼範例。
2. 從所指定語言旁的功能表中選取語言，以變更範例格式（必要的話）。 
3. 選取**試用**。
4. 選取**呼叫作業**。 

隨即會顯示要求的回應。 

## 自訂網域
{: #custom_domains}

在部分實例中，您可能想要自訂或「虛擬」網域，而非 API 閘道的預設網域。API Management 功能可支援具有您選擇之網域名稱的前端 API。

完成下列步驟以起始設定自訂網域。如果您之前已完成設定網域的步驟，請參閱[對您的 API 使用自訂網域](manage_apis.html#custom_domains_bind)。

自訂網域不會隔離的成單一 API，而是將範圍設為一群 API，其由下列項目定義：
- 產生端的 {{site.data.keyword.Bluemix_notm}} 服務（例如 {{site.data.keyword.openwhisk_short}}）
- Cloud Foundry 空間

例如，自訂網域的範圍會設為在 "dev" Cloud Foundry 空間中建立的所有 {{site.data.keyword.openwhisk_short}} API。

### 設定

若要開始使用，請先在支援整合式 API Management 特性的 {{site.data.keyword.Bluemix_notm}} 服務中建立新的 API，或使用 {{site.data.keyword.Bluemix_notm}} API 主控台建立 API Proxy。

#### 準備憑證

為了登錄自訂網域，在設定期間必須提供有效的 TLS 憑證。請使用 [Certificate Manager](../services/certificate-manager) 服務來上傳憑證及私密金鑰。

*附註：API 呼叫只能使用 TLS（埠 443）。不支援一般 HTTP。*

### 對您的 API 使用自訂網域
{: #custom_domains_bind}

完成起始設定之後，請透過完成下列步驟，從 {{site.data.keyword.Bluemix_notm}} API 的**自訂網域**區段中，將一個以上的 API 連結到已登錄的網域：

1. 在可用的目標清單中，找到自訂網域應該連接的服務或預設網域。
2. 在個別的瀏覽器視窗或標籤中，導覽至 DNS 提供者的設定頁面，然後為想要的網域建立 CNAME 記錄。請使用 {{site.data.keyword.Bluemix_notm}} 自訂網域管理頁面中的**預設網域 / 別名**直欄，作為 CNAME 目錄，然後儲存您的 DNS 設定。
  
    *附註：DNS 變更可能需要長達 48 小時才能傳播，不過變更通常發生的速度比那快。*
  
3. 在自訂網域頁面上，按一下包含目錄「預設網域」之列上的三個點，然後從功能表選取**編輯**。
4. 在結果對話框中，選取**指派自訂網域**勾選框。
5. 在**網域名稱**欄位中，指定想要的自訂網域（例如 *api.mycompany.com*）
6. 從 Certificate Manager 複製在起始設定期間上傳之憑證的「雲端資源名稱 (CRN)」。
7. 將您複製的 CRN 貼到**憑證 CRN** 欄位。
8. 按一下**儲存**。指定的網域名稱應該出現在預設網域旁的列，指出它已順利套用。

*附註：套用自訂網域之前，將會驗證 DNS 指標，方法是確定自訂網域 CNAME 指向與 API 相關聯的預設網域。如果尚未完成 DNS 設定，或是來自步驟 2 的 DNS 變更尚未傳播，將會出現錯誤且不會儲存網域設定。若發生此情況，請在變更 DNS 設定之後定期重試，最多 48 小時。如果在 48 小時之後錯誤仍持續發生，請驗證您的 DNS 設定，或與 {{site.data.keyword.Bluemix_notm}} 支援中心聯絡。*
