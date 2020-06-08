# Basic Course Django

This course is created for backend developer begining, which they to learn the basic django structure. In its we will create a simple CRUD project to reforce the learned

## Previous Knowledge 📋

Django is a framework on python to develomentp web application in backend, and to work with its (in this course) is required this previous knowlodge:

* SO GNU/Linux based on Debian.
* Programming languaje: Python 3.
* SQL languaje (We will use PostgreSQL).
* HTML, CSS and JS.

## Installations and configurations to start 🔧

### Update package list

```bash
sudo apt-get update
sudo apt-get safe-upgrade
```

### Install dependency package

```bash
sudo apt-get install git-core libjpeg-dev libfreetype6 libfreetype6-dev zlib1g-dev libxml2-dev libxslt1-dev python3-dev libssl-dev python3-pip libwv-dev wv libpq-dev gettext python3-psycopg2
```

### Install PostgreSQL

```bash
sudo apt-get install curl ca-certificates gnupg
curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
sudo apt-get update && sudo apt-get install postgresql-11
```

### Update pip

```bash
sudo pip3 install pip --upgrade
```

### Install virtualenv

virtualenv is a package that allows us to create an enviroment to python projects. It is a good practice create a virtual enviroment to each python project

```bash
sudo pip3 install virtualenv
```

### Create the virtualenv

We create the virtualen with python3 structure

```bash
virtualenv env --python=python3
```

### Activate the virtualenv

```bash
source env/bin/activate
```
**PD:** This step we need do each time that work in the project

### Configure PostgreSQL

```bash
sudo su - postgres
psql

postgres=# CREATE DATABASE django_basic_coursedb;
postgres=# CREATE USER devuser WITH PASSWORD 'devpass';
postgres=# ALTER ROLE devuser SET client_encoding TO 'utf8';
postgres=# ALTER ROLE devuser  SET default_transaction_isolation TO 'read committed';
postgres=# ALTER ROLE devuser  SET timezone TO 'UTC';
postgres=# GRANT ALL PRIVILEGES ON DATABASE django_basic_coursedb TO devuser;
postgres=# \q
```

**PD:** django_basic_coursedb, devuser and devpass are values that you can set however you want

### Install Django and postgresql module

```bash
pip3 install Django psycopg2
```

### Create project

```bash
django-admin startproject basic_course
```

### Apply migrations
First we need change the variable settings DATABASES

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'django_basic_coursedb',                      
        'USER': 'devuser',
        'PASSWORD': 'devpass',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

Now apply migrations

```bash
cd basic_course
python manage.py migrate
```

## Test installation 🔩

### Create admin user

```bash
python manage.py createsuperuser
```

Set the value to admin user

**PD:** You need take note of this values for future uses

### Run local server

```bash
python manage.py runserver 0.0.0.0:8000
```

And open this url: http://localhost:8000. To admin dashboard access: http://localhost:8000/admin