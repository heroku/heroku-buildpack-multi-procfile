# Heroku Multi Procfile buildpack

_tl;dr_ -- The idea here is that you have a single git repository, but multiple Heroku apps. In other words, you want to share a single git repository to power multiple Heroku apps. So, for each app you need this buildpack, and for each app, you need to set a config variable named PROCFILE to the location where the procfile is for that app. As an example:

```
$ heroku create -a example-1
$ heroku create -a example-2
$ heroku buildpacks:add -a example-1 https://github.com/heroku/heroku-buildpack-multi-procfile
$ heroku buildpacks:add -a example-2 https://github.com/heroku/heroku-buildpack-multi-procfile
$ heroku config:set -a example-1 PROCFILE=Procfile
$ heroku config:set -a example-2 PROCFILE=backend/Procfile
$ git push https://git.heroku.com/example-1.git HEAD:master
$ git push https://git.heroku.com/example-2.git HEAD:master
```

When example-1 builds, it'll copy Procfile into /app/Procfile, and when example-2 builds, it'll copy backend/Procfile to /app/Procfile. For example-2, the process types available for you to scale up will be the ones referenced (originally) in backend/Procfile.

# Heroku Pipelines

**This buildpack will not work** for using a different Procfile in staging and production. You must use the same Procfile in these two environments because the slug will be compiled when your app is deployed to staging. When the compiled slug is promoted to production, the production environment will be ignored because the app won't be compiled again to copy over a different Procfile.

This buildpack does work well for review apps though because they are compiled each time you deploy a new review app.

# Authors

Andrew Gwozdziewycz <apg@heroku.com> and Cyril David <cyx@heroku.com>
