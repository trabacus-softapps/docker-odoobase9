A *production-ready* image for Odoo 9 
=====================================

This image weighs just over 1Gb. Keep in mind that Odoo is a very extensive suite of business applications written in Python. We designed this image with built-in external dependencies and almost nothing useless. It is used from development to production on version 9.0 with various community addons.

Odoo version
============

This docker builds with a tested version of Odoo (formerly OpenERP) AND related dependencies. We do not intend to follow the git. The packed versions of Odoo have always been tested against our CI chain and are considered as production grade. We update the revision pretty often, though :)

This is important to do in this way (as opposed to a latest nightly build) because we want to ensure reliability and keep control of external dependencies.

You may use your own sources simply by binding your local Odoo folder to /opt/odoo/sources/odoo/

Here are the current revisions from http://nightly.odoo.com/9.0/nightly/src/ for each docker tag

    # production grade
    docker/odoobase:9.0c 07-FEB-2016

Start Odoo
----------

`Usage: docker run [OPTIONS] xyz/odoo[:TAG] [COMMAND ...]`

Run odoo in a docker container.

Positional arguments:
  COMMAND          The command to run. (default: help)

Commands:
  help             Show this help message
  start            Run odoo server in the background (accept additional arguments passed to odoo command)
  login            Run in shell mode as odoo user

Examples:
----------
  
  Run odoo V8 in the background as `xyz.odoo` on localhost:8069 and use /your/local/etc/ to load odoo.conf

	$ docker run --name="xyz.odoo" -v /your/local/etc:/opt/odoo/etc -p 8069:8069 -d xyz/odoo:9.0 start

  Run the V9 image with an interactive shell and remove the container on logout

  	$ docker run -ti --rm xyz/odoo:9.0 login

  Run the v8 image and enforce a database `mydb` update, then remove the container

	$ docker run -ti --rm  xyz/odoo:9.0 start --update=all --workers=0 --max-cron-threads=0 --no-xmlrpc --database=mydb --stop-after-init
