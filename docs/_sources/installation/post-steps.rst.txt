================================================================
インストール後の処理
================================================================
Sitecoreをインストールしたら、 Installation Guide の内容に従って、インストレーションの後処理を実施します。Sitecore 9.0 Initial Release用の Installation Guideの6章の手順に従って、後処理を実施していきます。バージョンによって作業が異なる可能性があるので、利用するSitecoreのバージョンのInstalltion GuideのSitecore XP Post-Installation Stepsを参照するようにしてください。

xDBシャードデータベース用のデータベースユーザーの作成
================================================================
シャード構成されたコレクションデータベースにアクセスするSQLユーザー(デフォルトでcollectionuser)をSQLサーバー上に作成します。

SQL Server Management Studio を起動して、SQL データベースサーバーに接続します。

ツールバーの **新しいクエリ** をクリックします。

.. figure:: /images/installation/ins-post01.png

Installation Guideの `Add a Recognized User to the xDB Shard Databases` セクションのサンプルスクリプトをベースにして、 `SETVAR` のパラメーターを適宜変更します。
デフォルト構成で xConnect をセットアップしている場合は、サンプルスクリプトのまま実行できるはずです。Sitecore 9.0 Initail Release が対象で、デフォルト構成のままインストールし、インストレーションガイドのPDFからサンプルスクリプトを準備するのが面倒な場合は、 :download:`こちら <../download/postinstall.sql>` からsqlファイルをダウンロードできます。

Management Studioの **クエリ > SQL CMDモード** をクリックします。

.. figure:: /images/installation/ins-post02.png

``F5`` キーもしくは、ツールバーの **実行ボタン** をクリックします。

.. figure:: /images/installation/ins-post03.png

エラーが発生しなければ成功です。

インデックスのリビルド
================================================================
Sitecoreの編集環境にログインします。デフォルトのままインストールしている場合は、``http://xp0.sc/sitecore`` です。

**コントロールパネル** にアクセスし、 **INDEXING** セクションの **Indexing manager** をクリックします。

.. figure:: /images/installation/ins-post04.png

Indexing Manager ダイアログで、 Select all をクリックして、 **Rebuild** をクリックします。


リンクデータベースのリビルド
================================================================
アイテム間の参照関係を管理しているリンクデータベースをリビルドします。コントロールパネル内の **DATABASE** セクションの **Rebuild link databases** をクリックします。

.. figure:: /images/installation/ins-post05.png

core, master を選択して、**Rebuild** をクリックします。

.. figure:: /images/installation/ins-post06.png


マーケティング定義の配置
================================================================
xDBにマーケティング定義を配置します。コントロールパネル内の **ANALYTICS** セクションの **Deploy marketing definitions** をクリックします。

.. figure:: /images/installation/ins-post07.png

定義の種類がすべて選択されていることを確認してから、 **Deploy** をクリックします。

.. figure:: /images/installation/ins-post08.png

.. note:: Deployの処理は時間がかかります。

静的コンテンツに対する Expires ヘッダーの設定
================================================================
パフォーマンスを改善するために、静的コンテンツに対して7日間キャッシュを有効かする設定をIISのサイトに設定します。

IIS管理マネージャーを起動して、 Sitecoreのサイト(今回の例は xp0.sc) を選択して、 **HTTP 応答ヘッダー** をダブルクリックします。 

.. figure:: /images/installation/ins-post09.png

右側操作ペインの **共通ヘッダー** の設定 をクリックします。

.. figure:: /images/installation/ins-post10.png

ダイアログの中の **期限切れのWebコンテンツ** を選択し、 失効までの期間に 7日間を指定して **OK** ボタンをクリックします。

.. figure:: /images/installation/ins-post11.png

IPジオロケーションルックアップ処理の無効化
================================================================
IPアドレスから、ロケーション情報をルックアップするサービスを利用していない場合は、ルックアップ処理を無効化できます。 Installation Guideの Tracking Configuration セクションに従って、無効化してください。有効のままでも特に問題はありません。


IISの再起動
================================================================
最後に、コマンドプロンプトから ``iisreset`` を実行してIISを再起動します。

これでセットアップ完了です。