# How to deploy Meteor application through Heroku 
## Author: ksnt

:satisfied: enjoy!

# Setting of git

create git repository, then add and commit file
```
$ cd MOVE_TO_THE_DIRECTORY_FOR_YOUR_APP
$ git init
$ git add .
$ git commit -m "first commit"
```

# Setting of Heroku

1. Login your Heroku account (or create your account if you don't have it) <br>
2. Create new application from "Dashboard" or Create new application on the terminal

3. Create scaffold using Buildpack
```
$ heroku create --stack cedar --buildpack https://github.com/YOUR_ACCOUNT_NAME/YOUR_REPOSITORY_NAME.git
```

4. Choose ROOT_URL
```
$ heroku config:add ROOT_URL=https://YOUR_APP_NAME.com
```

5. Create package.json on the top directory of the application
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

6. Add an addon: mongolab
```
$ heroku addons:create mongolab:sandbox
```

<em>Remark</em><br>
<em>If you want to use mongolab, you have to register your credit card. The fee is free.</em>


7. Setting of mongolam
```
$ heroku config:get MONGODB_URI
$ heroku addons:open mongolab
```

8. Choose which language you use.
Now I am using MeteorJs, therefore I choose nodejs.
```
$ heroku buildpacks:set heroku/nodejs
```

9. Deploy
```
$ heroku git:remote -a YOUR_APP_NAME
$ git push heroku master
```
