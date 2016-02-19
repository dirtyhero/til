# バッチ処理を登録するときに、deployのたびにcronの設定が増えていってしまう。

opsworksでのデプロイの場合には、curentのディレクトリから、
releaseのpathへシンボリックリンクをしているために、デプロイのたびにwheneverの実行をすると、
crontabに追記がされて、同じcronのタスクが沢山実行されている状態になってしまう。

登録時のコマンドを下記の用に実行することで解決。


```
bundle exec whenever --update-cron #{app_name}
```

wheneverでは、実行しているディレクトリ名でcronの登録を管理しているようだが、
登録のコマンドの後ろに、アプリの名称を引数として渡すと、
ディレクトリではなく、アプリの名称で管理されるようになりました。

```
bundle exec whenever --clear-crontab
```

これでちゃんと削除出来るようになりました。

