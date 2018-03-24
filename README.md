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

Before add frontend subtree (wich is actually created) we create
a simple app to serve the home page from a template. We do this in develop
branch and make a commit.

It's time to add our stules from the frontend repo.

Sample frontend repo has now two releases: 1.0 and 1.1.
While on branch develop we add subtree from frontend repo.

For now we add subtree from frontend develop branch. To make commands easier
we will add a custom remote for frontend

```
git remote add frontend git@github.com:tonybolanyo/subtree-frontend.git
git subtree add --prefix=frontend/ frontend develop
```

Now we can recreate frontend files.

```
cd frontend
npm install
gulp build
```

Now the frontend optimized files are in frontend/dist so we need to configure
Django to use that folder as static folder. We only need a couple of lines in
the settings file:

```
STATICFILES_DIRS = [
    os.path.join(os.path.dirname(BASE_DIR), 'frontend', 'dist')
]
```

We can test everything is running as expected:

```
python manage.py runserver
```

And that's it.