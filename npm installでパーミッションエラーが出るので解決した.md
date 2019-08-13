# npm installでパーミッションエラーが出るので解決した

```
$ npm install
npm WARN checkPermissions Missing write access to /path/to/node_modules
....
```

となっていた。`sudo`をつければコマンドは実行可能だが面倒なので`/path/to/node_modules`の所有者を自身に変更して解決した。

```
$ sudo chown -R $(whoami) /path/to/node_modules
```
