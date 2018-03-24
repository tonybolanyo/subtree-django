# subtree-django
Root repo to try git subtree

## steps

Create new repo on Github.

Clone repo to local machine

`git clone git@github.com:tonybolanyo/subtree-django.git`

Create virtual environment and install basic django site.

```
virtualenv .env
source .env/bin/activate
pip install django
```

Create minimal django project

```
django-admin startproject subtree
mv subtree/ src
cd src
python manage.py migrate
```

Test it runs

```
python manage.py runserver
```

Push to origin/master

