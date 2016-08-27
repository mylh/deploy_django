# deploy_django

Ansible role to deploy django based web application (my style). Python wsgi application is served with uwsgi and nginx. Uwsgi server is ran by supervisor. Optional feature - download and install GeoIP database and a cronjob to update this db.

Code deploymnent is possible in two ways:
 - from remote GIT repo
 - from local machine with sync command

Default mode is local sync from ../src direcotry relative to the ansible script root.

if `requirements.pip` is present in src directory then requirements are installed into app venv

if `setup.py` is present in src directory then package is installed locally into app venv

Assumptions: You have read through the role source and understand what you are doing :) Python3. Ansible 2.0 and higher. If deployment is made from a GIT repo django project is placed into `src` subdirectory within repo. If not then you need to set `app_root_path` and `app_uwsgi_executable` variables. Uwsgi and nginx located at the same machine, we use unix sockets.

## Usage

inlude this role as dependency role into app customized role.

When `--tags=deploy` command line option is used then only code update, syncdb and collectstatic is made with uwsgi app reload. Use to save your time.