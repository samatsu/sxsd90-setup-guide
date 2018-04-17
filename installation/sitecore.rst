================================================================
Sitecoreのセットアップ
================================================================
Sitecore Experience Platform 環境をセットアップしていきます。

リソースのダウンロード
================================================================
`<https://dev.sitecore.net/>`__ にアクセスして、 最新の Sitecore 9 の構成ファイルをダウンロードします。今回は、Sitecore Experience Platform 9.0 rev. 171002 (9.0 Initial Release) をインストール前提で、手順を記載していきます。

Sitecore 9.0 の Initial Release は `こちら <https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/90/Sitecore_Experience_Platform_90_Initial_Release.aspx>`__ からダウンロードできます。

.. note:: Sitecore 本体や関連モジュールをダウンロードするには、 Sitecoreが提供する開発者向け認定試験に合格している必要があります。

ダウンロードページの **Download options for On Premises deployment** セクションの **Packages for XP Single** をダウンロードします。Packages for XP Single にはオンプレミス環境の一つのマシン上にSitecore Experience Platform をインストールするための構成ファイル一式が含まれています。

.. figure:: /images/installation/ins-sc01.png


ダウンロードしたファイル (今回の例では `Sitecore 9.0.0 rev. 171002 (WDP XP0 packages).zip` を右クリックしてプロパティ画面を表示し、 ブロックの解除 を行います。

.. note:: Azure用の構成ファイル一式は `Download options for Azure AppService` セクションからダウンロードできます。

ダウンロードした zip ファイルを展開します。今回は、  ``C:\resourcefiles`` フォルダーにzipファイルを展開した前提で説明を記載します。

`C:\resourcefiles` に展開された `XP0 Configuration files rev.171002.zip` を展開して、中身のファイルを `C:\resourcefiles` に移動します。最終的に次の図のようなファイル構成になります。

.. figure:: /images/installation/ins-sc03.png

同ページ上からインストールガイドもダウンロードできます。 インストールガイドをまだダウンロードしていない場合は、 **Release information** セクションで **Installation guide**  をクリックしてダウンロードしておきます。

.. figure:: /images/installation/ins-sc02.png


Install スクリプトの準備
================================================================
Sitecore のインストールは、 インストール用のPowerShell スクリプトを使用します。
ダウンロードしたInstallation Guide の `Edit and Run the Installation Script` に従って、インストール用のPowerShell スクリプト
を作成し、``C:\resourcefiles`` に ``install.ps1`` という名前で保存します。

Installation Guide の PDFからスクリプトをコピーして作成するのが面倒な場合は、 Sitecore 9.0 の Initial Release の場合は、 :download:`Installスクリプトのひな形 <../download/install.ps1>` をダウンロードして利用することもできます。

今回は、あらかじめ用意しておいたインストールスクリプトのひな形をダウンロードし、#define parameters セクションにパラメーターを次の表のように変更しました。

.. csv-table:: インストールスクリプトのパラメーター例
 :header: "パラメーター", "値"

 $prefix , \\"xp0\\"
 $PSScriptRoot , \\"C:\resourcefiles\\"
 $XConnectCollectionService , \\"$prefix.xconnect\\" 
 $sitecoreSiteName , \\"$prefix.sc\\"
 $SolrUrl , \\"\https://localhost:8983/solr\\" 
 $SolrRoot , \\"C:\Solr-6.6.1\\"
 $SolrService , \\"Solr-6.6.1\\" 
 $SqlServer , \\".\\"
 $SqlAdminUser , \\"sa\\" 
 $SqlAdminPassword , saユーザーのパスワード

.. note:: SqlAdminPassword は SQL Server をインストール時に指定したsaユーザーのパスワードを設定してください。

.. note:: 設定するパラメーターは環境に合わせて適宜変更してください。

ライセンスファイルの準備
================================================================
Installation Guide に従って install.ps1 を準備した場合は、 $PSScriptRoot 配下にライセンスファイルを配置しておく必要があるので、配置します。

最終的には次の図のようなファイルは一になります。

.. figure:: /images/installation/ins-sc04.png


Install スクリプトの実行
================================================================
PowerShellを管理者モードで起動して、作成した Install.ps1 を実行します。このとき、文字化けが発生する場合は、最初に ``[Console]::OutputEncoding = [Text.Encoding]::UTF8`` を実行します。

.. code-block:: ps1

 [Console]::OutputEncoding = [Text.Encoding]::UTF8
 .\install.ps1

.. figure:: /images/installation/ins-sc05.png

.. warning:: スクリプトを実行する前に Solr が 8983 ポートで動作していることを確認してください！

インストール時に、エラーが発生した場合は、エラー内容に従ってエラーを修正してから、インストールスクリプトを再度実行してください。

インストールに成功すると、IIS管理マネージャーから、Sitecore 本体および、 xConnect 用のサイトが作成されていることを確認できます。

.. figure:: /images/installation/ins-sc06.png

ブラウザーを起動して、 `http://xp0.sc` にアクセスします。デフォルトのトップページが表示されることを確認します。

また、`http://xp0.sc/sitecore` にアクセスして、デフォルトの admin の パスワード `admin/b` でラウンチパッドにログインできることを確認します。

.. note:: インストール用の設定ファイルで別のパスワードを指定している場合は、そのパスワードでログインして下さい。