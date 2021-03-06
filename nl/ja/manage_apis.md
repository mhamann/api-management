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

# API の管理
{: #manage_apis}

API が API Management システムによって管理およびモニターされるように API を統合すると、API 設定を表示および変更できるようになります。 API を統合していない場合は、『[{{site.data.keyword.openwhisk_short}} アクションからの API の作成](manage_openwhisk_apis.html)』または『[API 管理対象エンドポイントの有効化](manage_cf_apis.html)』の手順を実行して、API を統合する必要があります。 

API の設定を管理するには、以下のステップを実行します。

新規 API を作成した場合、それが既にインターフェースで開いていれば、最初の 3 つのステップをスキップすることができます。

1. API の情報がまだ表示されていない場合は、{{site.data.keyword.Bluemix}}ダッシュボードから管理する API を選択するか、または {{site.data.keyword.openwhisk_short}} サービスのダッシュボードでアクションを選択することにより管理する API を選択します。
2. ナビゲーションで**「API Management」**をクリックします。あるいは、{{site.data.keyword.openwhisk_short}} アクションである場合は **「API」**タブを選択します。
3. 必要な場合は、管理する API を選択します。 接続が確立されると、以下の選択項目を表示および更新できるようになります。
    * サマリー
    * 定義 (Definition)
    * 共有 (Sharing)
    * API エクスプローラー
4. 「管理対象 API の公開 (Expose Managed API)」スライダーを選択してアクティブ化し、API を公開します。 注: API が公開されていない場合、設定の一部は設定できません。  

## API の設定のサマリー
{: #overview_api}

API を選択すると「サマリー」タブがデフォルトで選択されています。これは 2 つのセクションに分かれています。
* 「プロパティー」 - 「プロパティー」セクションでは、以下の情報を参照できます。
    * API に関する基本情報
	* セキュリティー・ポリシー
	* レート制限情報
    * 共有の詳細
* 「分析とロギング (Analytics and Logging)」セクション - 「分析とロギング (Analytics and Logging)」セクションでは、以下の統計を参照できます。
	* 指定された最後の時間間隔中の応答数および平均応答時間
    * 1 分当たりの API 呼び出しの回数 (グラフ形式)
    * 「応答ログ (Response Log)」テーブル内の最後の 100 回の応答
	
*「応答」*グラフは、API が受け取った応答の数と、応答の状況の明細を、素早く確認できるようになっています。 これは、過半数のエラー応答を受け取っているかどうかを判断するのに役立ちます。 過半数のエラー応答は、レート設定で許可されているよりも多くのトラフィックがあることを示す可能性があります。 情報アイコンにカーソルを置くことにより、応答コードごとに応答の数値明細を表示できます。 一般的な応答コードを以下に示します。
* 200  OK
* 201  作成済み
* 302  検出済み
* 304  変更なし
* 400  間違った要求
* 401  認証が必要
* 403  禁止
* 500  内部サーバー・エラー
* 503  サービス使用不可

「応答ログ (Response Log)」テーブルには、最後の 100 回の応答の個別の詳細情報が含まれています。 列見出しを選択すると、列内の項目に従って情報をソートすることができます。 *「応答の検索 (Search responses)」*バーを使用して、「応答ログ (Response Log)」テーブル内で特定の項目を検索できます。 イベントを選択するか、項目の横にあるオプション・メニュー (垂直に並んだ 3 個のドット) のリストで**「詳細を表示」**を選択すると、イベントについてさらに詳細な情報を利用できます。


## API 設定の編集
{: #settings_api}

**「定義 (Definition)」**タブで、API に関する基本情報を更新できます。 この情報には、資料、名前、および基本 URL が含まれています。 「セキュリティーおよびレート制限 (Security and Rate Limiting)」セクションを使用して、呼び出しおよび間隔の制限を指定することで、1 秒、1 分、または 1 時間ごとに特定の数の呼び出しのみが行われるようにします。 データを望ましくない方法で使用されないようにするため、または API に関する統計を収集するために、API 呼び出しを行うときに認証を要求することも可能です。

API の設定を変更するには、以下のステップを実行します。

1. API Management ダッシュボードで、**「定義 (Definition)」**タブをクリックします。
2. 「API 情報 (API Info)」セクションで、API の名前を指定したり更新したりすることができ、API 定義をインポートすることもできます。
3. 「セキュリティーおよびレート制限 (Security and Rate Limiting)」セクションで、以下のポリシーを更新できます。
    * API キーが必要 (Require API key) - 正しい API キーが提供された場合のみ API 呼び出しを処理できるようするかを指定します。 デフォルト設定では、追加のキーは必要ありません。
    * セキュリティー方式 (Security method) - API キー・オプションが選択されている場合、API を処理するために API キーのみが必要であるか、API キーと API 秘密の両方が必要であるかを指定します。
    * API キーおよび秘密のロケーション (Location of the API key and secret) - 方式の設定に応じて、API セキュリティー情報がどのように呼び出しに組み込まれるかを指定します。 呼び出し名は、セキュリティー情報の識別方法を指定します。 キーおよび秘密の処理について詳しくは、『[キーおよび秘密の管理](keys_secrets.html)』を参照してください。
    * API 呼び出しレートの制限 (Limit API call rate) - 指定された時間間隔中に許可される API 呼び出しの数を、キーごとに設定するオプションを使用して設定します。 バースト・タイプのレート制限方式が使用されていることに注意してください。 API 呼び出しの平均レートは、レートで指定した合計時間間隔にわたって計算されます。 間隔中の API 呼び出しのレートが API 呼び出しの平均レートを超えた場合、レートで指定した制限時間まで、呼び出しが拒否される期間が存在する可能性があります。   
    * OAuth プロバイダー (OAuth provider) - 正しいセキュリティー・パラメーターを指定したユーザーが、Google、Facebook、IBM App ID、および GitHub のようなプロバイダーのソーシャル・ログイン資格情報を通じて OAuth を適用することにより、API にアクセスできるようにします。
	    **注:** **App ID** を OAuth プロバイダーとして使用する場合は、{{site.data.keyword.Bluemix_notm}} に構成されている既存の App ID サービス・インスタンスを指定して、ID 情報を提供する必要があります。 既存の App ID サービスがない場合は、OAuth セクションで**「作成」**を選択し、新しいウィンドウで App ID サービスを作成してから戻り、それを API Management 用に指定できます。 **「編集」**を選択して、選択したサービス・インスタンスを変更することもできます。
4. CORS の有効化 (Enable CORS) - クロス・オリジン要求 (CORS) により、異なるドメインからのいくつかの制限された要求が可能になります。
5. **「保存」**をクリックします。

## API の共有
{: #share_api}

自分が属する {{site.data.keyword.Bluemix_notm}} 組織の内部または外部の他のユーザーと、API を共有することができます。 

{{site.data.keyword.Bluemix_notm}} 組織の内部または外部の他のユーザーと API を共有するときに、API 用のキーおよび秘密を作成できます。 管理対象 API ごとに、5 つのキーを作成してその API に割り当てることができます。 個人または会社に固有のキーを送信することによって、その API がどのように使用されているかに関する統計情報を追跡できます。 例えば、その個人または会社による API 呼び出しの回数を追跡できます。 キーを無効にしたり、特定のキーからの呼び出しを制限したりすることもできます。 これは、テスト、ワークロード・バランシング、収益化の際、あるいはある種のセキュリティー状況に対処するために役立ちます。

*キー* とは、API に関連付けられた固有の文字ストリングです。 API に複数のキーを割り当てることができます。これは、各利用者による API の使用を追跡するのに役立ちます。 例えば、あるキーをある利用者に付与し、別のキーを別の利用者に付与します。 利用者は、API を呼び出すたびに、自分に割り当てられたキーを含めます。 そのキーを追跡することによって、API を呼び出した利用者が分かります。

キーには以下の 2 つのタイプがあります。

* {{site.data.keyword.Bluemix_notm}} 組織へのアクセス権限を持つ利用者と API を共有するためのキー。 
* {{site.data.keyword.Bluemix_notm}} 組織へのアクセス権限を持たない利用者と API を共有するためのキー。 

異なるタイプのキーでも、作成、保守、および削除の方法は同じです。 違いは、誰がそのキーを使用できるかという点のみです。

API に 1 つ以上のキーを作成した後で、キーごとに API の呼び出しレートを制限することができます。 *「定義」*タブで**「キーごとに API 呼び出しレートを制限する」**スライダーを有効にすることによって、作成したキーごとの呼び出し回数が、設定したレート制限までに限られます。   

*秘密* は、API 自体へのアクセスを維持するために使用されるため、キーに類似しています。 秘密はカスタマイズ可能であり、キーを変更しなくても秘密を変更できます。 キーがない場合、秘密は存在できません。 例えば、正しい秘密を持つユーザーのみが、API の新バージョンをアップロードできます。 API 呼び出しで API と秘密を必須とすることも、キーのみを使用することもできます。 秘密を変更する必要があるが、キーを変更したくない場合に、秘密は有用です。 

1. API Management ダッシュボードで、**「共有 (Sharing)」**タブをクリックします。
2. {{site.data.keyword.Bluemix_notm}} 組織へのアクセス権限を持つ他のユーザーが API を使用できるようにしたい場合は、「{{site.data.keyword.Bluemix_notm}} 組織内での共有 (Sharing within Bluemix Organization)」領域内で**「管理対象 API の公開」**を選択します。 キーを生成するには、これを選択する必要があります。
3. **「API キーの作成」**をクリックして、API の固有キーを作成します。 「API キーの作成」ダイアログ・ボックスが表示されます。 API キーが自動的に生成されます。
4. ユーザーに固有キーを送信することにより、API キーを使用して、どのユーザーが API にアクセスしているかを判別します。 ゲートウェイは、どのキー (および利用者) が呼び出しを生成しているかを判別できます。
5. キーの横にある**「メニュー」**アイコン (垂直に並んだ 3 個のドット) をクリックして、その API キーを編集または削除します。

「{{site.data.keyword.Bluemix_notm}} 組織の外部での共有 (Sharing Outside of Bluemix Organization)」セクションで、{{site.data.keyword.Bluemix_notm}} アカウントを持たないユーザーと API を共有できます。 この共有方式では、API エクスプローラー内で API に関する情報を表示するための直接リンクが提供されます。 API には、API エクスプローラー・ビューで API を実行するためのボタンが含まれています。 API のリンクを要求するには、以下のステップを実行します。

1. 「{{site.data.keyword.Bluemix_notm}} 組織の外部での共有 (Sharing Outside of Bluemix Organization)」セクションで、**「API キーの作成」**をクリックします。 「API キーの作成」ダイアログ・ボックスが表示されます。
     ユーザーの秘密は、制御できないことに注意してください。
2. API キーの固有の名前を指定します。
3. **「キーの作成 (Create key)」**を選択します。 
4. API ポータル・リンクを、{{site.data.keyword.Bluemix_notm}} アカウントを持たない利用者に送信します。 API キーおよび秘密 (使用されている場合) がリンクに含まれているため、どのキーがそのリンクを生成したかを判別できます。
  
API 資料のリンクにより**「API エクスプローラー (API Explorer)」**タブで API が開きます。

キーおよび秘密の処理について詳しくは、『[キーおよび秘密の管理](keys_secrets.html)』を参照してください。

## API エクスプローラーを使用した表示およびテスト
{: #explore_api}

「API エクスプローラー (API Explorer)」タブを選択して、Swagger 文書から生成された html を表示します。 

API エクスプローラーに、API に適用される API アクションおよび資料がすべて表示されます。 操作とアクションおよびそれらの説明を表示し、UI から API をテストすることができます。 Swagger 文書をダウンロードして、その内容を再利用することもできます。

API をテストするには、以下のステップを実行します。
1. デフォルトでは、*「例」*が選択されています。 これにより、選択した API のコードの例が表示されます。
2. 必要に応じて、指定した言語の横にあるメニューから言語を選択して、例のフォーマットを変更します。 
3. **「試行する (Try it)」**を選択します。
4. **「操作の呼び出し (Call operation)」**を選択します。 

要求への応答が表示されます。 

## カスタム・ドメイン
{: #custom_domains}

場合によっては、API ゲートウェイのデフォルト・ドメインの代わりにカスタム (「バニティー」) ドメインを使用する必要があることがあります。 API Management 機能は、選択したドメイン・ネームで、API の前に配置する操作がサポートされます。

初めてカスタム・ドメインをセットアップするには、以下のステップを実行します。 ドメインをセットアップするステップを以前に完了している場合は、『[API でのカスタム・ドメインの使用](manage_apis.html#custom_domains_bind)』を参照してください。

カスタム・ドメインは単一の API には分離されませんが、以下によって定義される API のグループにスコープされます。
- 発信元の {{site.data.keyword.Bluemix_notm}} サービス (例えば、{{site.data.keyword.openwhisk_short}})
- Cloud Foundry スペース

例えば、カスタム・ドメインは、「開発」Cloud Foundry スペースで作成されたすべての {{site.data.keyword.openwhisk_short}} API にスコープされます。

### セットアップ

はじめに、統合 API 管理機能をサポートする {{site.data.keyword.Bluemix_notm}} サービスで新しい API を作成するか、{{site.data.keyword.Bluemix_notm}} API コンソールを使用して API プロキシーを作成します。

#### 証明書の準備

カスタム・ドメインを登録するためには、セットアップ中に有効な TLS 証明書を提供する必要があります。[Certificate Manager](../services/certificate-manager) サービスを使用して、証明書と秘密鍵をアップロードします。

*注意: API 呼び出しは、TLS (ポート 443) を使用してのみ使用できます。単純な HTTP はサポートされていません。*

### API でのカスタム・ドメインの使用
{: #custom_domains_bind}

初期セットアップの完了後に、以下のステップを実行して、{{site.data.keyword.Bluemix_notm}} API コンソールの**「カスタム・ドメイン」**セクションから、登録済みのドメインに 1 つ以上の API をバインドします。

1. 使用可能なターゲットのリストで、カスタム・ドメインをアタッチするサービスまたはカスタム・ドメインを見つけます。
2. 別のブラウザー・ウィンドウまたはタブで、DNS プロバイダーの「設定」ページに移動し、目的のドメインの CNAME レコードを作成します。{{site.data.keyword.Bluemix_notm}} カスタム・ドメイン管理ページの**「デフォルト・ドメイン / 別名」**列の値を CNAME ターゲットとして使用して、DNS 設定を保存します。
  
    *注: DNS の変更は伝搬に最大 48 時間かかることがありますが、変更はそれよりも迅速に行われます。*
  
3. 「カスタム・ドメイン」ページで、ターゲットの「デフォルト・ドメイン」を含む 行の 3 つのドットをクリックし、メニューから**「編集」**を選択します。
4. 表示されるダイアログで、**「カスタム・ドメインの割り当て (Assign a custom domain)」**チェック・ボックスを選択します。
5. **「ドメイン・ネーム (Domain name)」**フィールドに目的のカスタム・ドメインを指定します (例えば、*api.mycompany.com*)。
6. 初期セットアップ時にアップロードされた証明書の Certificate Manager から、クラウド・リソース名 (CRN) をコピーします。
7. コピーした CRN を**「証明書 CRN (Certificate CRN)」**フィールドに貼り付けます。
8. **「保存」**をクリックします。 指定されたドメイン・ネームがデフォルト・ドメインの次の行に表示され、正常に適用されたことが示されます。

*注: カスタム・ドメインが適用される前に、カスタム・ドメインの CNAME が API に関連付けられているデフォルト・ドメインを指していることを確認することで、DNS ポインターが検証されます。DNS セットアップが完了していない場合や、ステップ 2 の DNS の変更がまだ反映されていない場合は、エラーが発生し、ドメインの設定は保存されません。これが発生した場合は、DNS 設定を変更した後、最大 48 時間まで、定期的に再試行してください。エラーが 48 時間を超えて続く場合は、DNS 設定を確認するか、{{site.data.keyword.Bluemix_notm}} サポートに問い合わせてください。*
