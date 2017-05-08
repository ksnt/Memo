# How to deploy Meteor application through Heroku
# Author: ksnt

## create git repository, then add and commit file
```
$ cd MOVE_TO_THE_DIRECTORY_FOR_YOUR_APP
$ git init
$ git add .
$ git commit -m "first commit"
```

## Login your Heroku account (or create your account if you don't have it)
## Create new application from "Dashboard" or Create new application on the terminal


## Create scaffold using Buildpack
```
$ heroku create --stack cedar --buildpack https://github.com/AdmitHub/meteor-buildpack-horse.git
```

## Choose ROOT_URL
```
$ heroku config:add ROOT_URL=https://YOUR_APP_NAME.com
```

## Create package.josn on the top directory of the applization
```
$cat package.json # example of package.json
{
  "name": "blog",
  "version": "1.0.0",
  "description": "",
  "scripts": {
  "start": "node server.js"
}
}
```

## Add a addon: mongolab
```
$ heroku addons:create mongolab:sandbox
```

## Remark
## If you want to use mongolab, you have to register your credit card. The fee is free.


## Setting of mongolam
```
$ heroku config:get MONGODB_URI
$ heroku addons:open mongolab
```

## Choose which language you use.
## Now I am using MeteorJs, therefore I choose nodejs.
```
$ heroku buildpacks:set heroku/nodejs
```

## Deploy
```
$ heroku git:remote -a YOUR_APP_NAME
$ git push heroku master
```