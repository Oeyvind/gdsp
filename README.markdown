# gDSP – an online course in DSP ear training

## South database migrations

This project uses [South](http://south.aeracode.org/) migrations for database
management. South allows you to make changes to the database without dealing
with raw SQL. The workflow is as follows:

1. Make some change to a model which affects the database, e.g. add a field.
2. Create a migration for this change. If the change was made to a model in the
   `core` application, this is achieved by running:

        ./manage.py schemamigration core --auto

   If it's the first migration for an app, replace `--auto` with `--initial`.
3. Run the migration. In the case of the `core` application, this means
   running:

        ./manage.py migrate core

## SASS and Compass for stylesheets

The CSS for this project is generated from stylesheets written in
[SASS](http://sass-lang.com/) using the [Compass](http://compass-style.org/)
framework. Compass is a Ruby application which can be installed using
[RubyGems](http://rubygems.org/) by running:

        [sudo] gem install compass

(At the time of writing, this will install `compass-0.12.2` and its dependencies
`sass`, `chunky_png` and `fssm`.)

To have Compass pick up on changes to SASS files when they're saved, `cd` into the
`compass` directory and run:

        compass watch

For a one-off compilation, run:

        compass compile

from the same directory. Both will generate CSS from the files present in
`compass/sass` and write to files in `static/css` in accordance with the
settings in `compass/config.rb`.

## Python packages

The Python packages required by this project are listed in the file
`requirements.txt`. Assuming [pip](http://www.pip-installer.org/) is present,
these packages can be installed with:

        pip install -r requirements.txt

Using a [virtualenv](http://www.virtualenv.org/) environment is a
good idea, both in development and production, as it allows you to
maintain several different Python environments on one system, as well
as install packages without root privileges. When using virtualenv
with Apache and mod\_wsgi, remember to set the WSGIPythonPath ([see
this](https://docs.djangoproject.com/en/dev/howto/deployment/wsgi/modwsgi/)).

## Configuration in a production environment

For security reasons, the database configuration and SECRET\_KEY of the
project are kept out of Git. This information, along with other configuration
variables which differ from development to production, is set in the file
`gdsp/settings_prod.py`. In production, this file is expected to be present and
the environment variable `DJANGO_PRODUCTION` is expected to be set.
