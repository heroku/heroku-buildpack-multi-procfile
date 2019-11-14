# Heroku Multi Node buildpack

Built as an extension to [Heroku Multi Procfile buildpack](https://github.com/heroku/heroku-buildpack-multi-procfile) and a more suitable alternative to another [Heorku Multi Node buildpack](https://github.com/busbud/heroku-buildpack-multi-node).

Relies on APP_DIR config variable being set. Copies Procfile from APP_DIR to root and writes into root a package.json that installs the APP_DIR node app.
