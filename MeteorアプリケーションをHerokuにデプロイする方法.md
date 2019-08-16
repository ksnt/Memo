# MeteorアプリケーションをHerokuにデプロイする方法2019

190816

以前やった方法とは違った方法でやってみて出来たのでメモ。

### 方法

まず、Herokuでアプリを作成する。

```
$ heroku create
```

もしアプリケーションの名前を指定したければ

```
$ heroku create myapp
```

とする。次に、Meteor Buildpack Horseを設定する。

```
$ heroku buildpacks:set https://github.com/AdmitHub/meteor-buildpack-horse.git
```

アプリケーションの名前を指定していた場合は次のようにする。

```
$ heroku buildpacks:set https://github.com/AdmitHub/meteor-buildpack-horse.git --app myapp

```

MeteorはMongoDBを使うため、そのためのアドオンを追加する必要がある。

```
$ heroku addons:create mongolab
```

最後に、環境変数`ROOT_URL`を設定する。
```
$ heroku config:set ROOT_URL=https://myapp.herokuapp.com
```

URLの中身は適切に変える必要があることに注意。

あとはgit pushすればよい。

```
$ git push heroku master
```

### 参考

http://meteor-fan.axlight.com/deploy-meteor-on-heroku/

