================================================================
レジストリ キー へのアクセスが拒否されました。エラーの回避
================================================================
SitecoreのWebサイトが既定の ApplicationPoolIdentity ユーザーで実行されている場合、Sitecoreのログファイルに次のような警告メッセージが記録されます。

::

 レジストリ キー 'Global' へのアクセスが拒否されました。

これはSitecore の パフォーマンスログを有効化している状態でかつ、アプリケーションプールの実行ユーザーが ``Performance Log Users`` グループのメンバーになっていない場合に発生します。

そのため、この問題を回避するには、 アプリケーションプールの実行ユーザーをデフォルトの ApplicationPoolIdentity から Network Service に変更します。

.. figure:: /images/misc/misc-regerr01.png

もしくは、アプリケーションプールの実行ユーザーを ``Performance Log Users`` グループのメンバーにします。 デフォルトのApplicationPoolIdentity が実行ユーザーに指定されている場合は、実際にApplicationPoolIdentityというユーザーがいるわけではありません。例えば xp0.sc というサイトのApplicationPoolIdentityの実際のアカウントは、次の図のように ``IIS AppPool\xp0.sc`` になります。

.. figure:: /images/misc/misc-regerr02.png

