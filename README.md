# Heroku Multi Procfile buildpack

Imagine you have a single code base, which has a few different applications within it... or at least the ability to run a few different applications. Or, maybe you're Google with your mono repo?

In any case, how do you manage this on Heroku? You don't. Heroku applications assume one repo to one application. 

Enter the Multi Procfile buildpack, where every app gets a Procfile!

# Usage

1. Write a bunch of Procfiles and scatter them through out your code base.
2. Create a bunch of Heroku apps.
3. For each app, set `PROCFILE=relative/path/to/Procfile/in/your/codebase/Procfile`, and of course:
   `heroku buildpacks:add -a <app> https://github.com/heroku/heroku-buildpack-multi-procfile`
4. For each app, `git push git@heroku.com:<app> master`

# Authors

Andrew Gwozdziewycz <apg@heroku.com> and Cyril David <cyx@heroku.com>
