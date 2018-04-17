================================================================
SIFに必要なソフトウェアのインストール
================================================================
Sitecore Install Framework を使用するために必要なソフトウェアをインストールします。

PowerShell のバージョン確認
================================================================

PowerShell は5.0 以降のバージョンが必要です。 Windows Server 2016の場合特に問題ないと思いますが、念のため確認します。

PowerShellを起動して、``$PSVersionTable`` と入力して実行します。

.. figure:: /images/prerequisites/pre-sif01.png

Web Deploy 3.6 for Hosting Servers のインストール
================================================================
Web PI(Platform Installer) 5.0 を使ってインストールします。

`Microsoft Web Platform Installer <https://www.microsoft.com/web/downloads/platform.aspx>`__ のページから、インストーラーをダウンロードします。ドキュメント作成時点の最新版が Web PI 5.0 です。
ダウンロードしたファイル wpilauncher.exe を右クリック > プロパティ を選択します。 **ブロックの解除** をクリックして、**適用** ボタンを押します。

wpilauncher.exe をダブルクリックして、インストーラーを起動します。右上の検索ボックスから、 *Web Deploy* というキーワードを入力して検索します。一覧から、 でWeb Deploy 3.6 for Hosting Servers を見つけて、右横にある **追加ボタン** をクリックして選択した後、 **インストール** をクリックしてインストールします。

.. figure:: /images/prerequisites/pre-sif02.png

URL Rewrite 2.1のインストール
================================================================
Web PI で、 URL Rewrite を検索すれば 2.1 のバージョンのURL Rewrite モジュールを見つけて、Web Deploy 3.6 for Hosting Servers と同様にインストールできます。

日本語UIのOSで検索すると、 URL Rewrite 2.0 が見つかりますが、こちらで問題ありません。インストール後に、 ``C:\Windows\System32\inetsrv\rewrite.dll`` のバージョンを確認すると 7.1.1980 になっているので、バージョン 2.1であることを確認できます。

.. figure:: /images/prerequisites/pre-sif04.png

.. note:: 次のURLから x64用の日本語のURL Rewrite 2.1 を明示的にダウンロードしてインストールすることもできます。`<https://www.iis.net/downloads/microsoft/url-rewrite>`__


データ層アプリケーション フレームワーク (17.01 DacFx)のインストール
====================================================================
`このページ <https://www.microsoft.com/ja-jp/download/details.aspx?id=55114>`__  からx86版のMicrosoft® SQL Server® データ層アプリケーション フレームワーク (17.0.1 DacFx)を明示的にダウンロードしてインストールするできます。

ただし、 :doc:`sql-server` のページで、最新の SQL Server Management Studio をインストールしている場合は、すでに最新のソフトウェアがインストールされているというメッセージが表示されます。この場合は、インストールする必要はありません。

SQL DOM のインストール
================================================================
`Microsoft® SQL Server® 2016 Service Pack 1 Feature Pack <https://www.microsoft.com/ja-JP/download/details.aspx?id=54279>`__ のページにアクセスして、 x86版の SqlDom.msi をダウンロードして インストールします。

.. figure:: /images/prerequisites/pre-sif03.png

これで必要なソフトウェアのインストールは完了です。