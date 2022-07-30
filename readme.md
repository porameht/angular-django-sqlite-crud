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

- APIs for Department screen : GET, PUT, POST and DELETE

  - navigate to EmployeeApp/views.py
  - import `from django.shortcuts import render`
  - import `from django.views.decorators.csrf import csrf_eempy`
  - import `from rest_framework.parsers import JSONParser`
  - import `from django.core.files.storage import default_storage`
    -import `from django.http.response import JsonResponse`

  - import data `from EmployeeApp.models import Departments, Employees`
  - import data `from EmployeeApp.serializers import DepartmentSerializer, EmployeeSerializer`

  - add @csrf_exempt is a CSRF cookie that is based on a random secret value, which other sites will not have access to

  - create function departmentApi and add condition request method GET, POST, PUT, DELETE

  - create file EmployeeApp/urls.py and prepare routi ng url for access API
    - import `from django.conf.urls import urls`
    - import api method `from EmployeeApp import views` and create urlpatterns
    - add api of EmployeeApp to main/urls.py and import `from django.urls import re_path` then add url from EmployeeApp to urlpatterns
    - test api by post man `http://127.0.0.1:8000/department/`

- APIs for Employee screen : GET, PUT, POST and DELETE

  - navigate to EmployeeApp/views.py and add function employeeApi
    - navigate to EmployeeApp/urls.py and prepare routing url for access API function employeeApi
  - test api by postman result are "ok"

- API method yo Upload Photo
  - import `import os` in file DjangoAPI/setting.py and add `MEDIA_URL = '/media/', MEDIA_ROOT = os.path.join(BASE_DIR,"media")`
  - import `from django.core.files.storage import default_storage` in file EmployeeApp/views.py and create function SaveFile
  - set routing url in file EmployeeApp/urls.py and add static route
  - test file by using post method setting to uploadedFile and type is file
