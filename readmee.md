**django api**

- pipenv --python 3.8.9

- pipenv install django

- pipenv shell check by pip list

- install django and djangorestframework

  - `pip install django`
  - `pip install djangorestframework`

- create django project

  - `django-admin startproject DjangoAPI`
  - start project `python manage.py runserver`

- exploring sqlite db file

- enable cors `pip install django-cors-headers`

  - open setting.py and register INSTALL_APPS section add "corsheaders"
  - add "corsheaders.middleware.CorsMiddleware" to MIDDLEWARE section
  - add CORS_ORIGIN_ALLOW_ALL = True if want domain spacify CORS_ORIGIN_WHITELIST = ("http://google.com")

- create django app and models

  - `python manage.py startapp EmployeeApp`
  - open setting.py and add 'EmployeeApp.apps.EmployeeappConfig' in INSTALL_APPS section and add 'rest_framework'
  - create model Employee in models.py
  - create table in sqlite `python manage.py makemigrations EmployeeApp`
  - and change to database file `python manage.py migrate EmployeeApp`

- add serializers
  - create file serializers in EmployeeApp
  - import `from rest_framework import serializers`
  - import `EmployeeApp.models import Departments, Employees`
  - create class DepartmentSerializer and EmployeeSerializer
