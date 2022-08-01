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

**angular ui**

- create angular project `ng --version` and `ng new angular10`

  - test run `ng serve --open`

- generate components and services

  - create component department by `ng generate component department`

    - create the child component for showing data or deleting `ng generate component department/show-dep`
    - create the child component for add and edit `ng generate component department/add-edit-dep`

  - create component employee by `ng generate component employee`

    - create the child component for showing data or deleting `ng generate component employee/show-emp`
    - create the child component for add and edit `ng generate component employee/add-edit-emp`

  - create service file `ng generate service shared`

  - import service `import { SharedService } from './shared.service'` in file app.module.ts
    - pass SharedService to providers

- add service methods

  - import module infile app.module.ts `import {HttpClientModule} from '@angular/common/http'` and `import {FormsModule, ReactiveFormsModule} from '@angular/forms'`
  - pass `HttpClientModule`, `FormsModule`, `ReactiveFormsModule` to imports section
  - navigate to shared.service.ts and import `import {HttpClient} from '@angular/common/http'`, `import {Observable} from 'rxjs'`
  - defind readonly variable APIUrl and PhotoUrl within class SharedService

  - assign instant private http: HttpClient to constructor

  - service of department and employee

    - create get method using `Observable` is a feature that provides support for delivering messages between different parts of your single-page application.
    - create post, put, delete method

  - service of photo `UploadPhoto`
  - service get all department name `getAllDepartmentNames`

- add routing to navigate

  - navigate to file app-routing.module.ts and import `import { EmployeeComponent } from './employee/employee.component'`, `import { DepartmentComponent } from './department/department.component'`
  - map path with component in routes section
  - add `<router-outlet></router-outlet>` in file app.component.html
  - test by `http://localhost:4200/employee`

- instll bootstrap

  - install bootstrap by `ng add @ng-bootstrap/ng-bootstrap`
  - add stylesheet link to index.html and add js script within tag body

- add bootstrap and add navbar within file app.component.html

- show departments screen

  - add DepartmentList empty array in file show-dep.component.ts
  - import service `import {SharedService} from 'src/app/shared.service'`
  - assign instant `private service:SharedService` to constructor of class ShowDepComponent
  - create method refreshDepList and using asynchronous operation `this.DepartmentList = data`
  - add refreshDepList in method ngOnInit it is the first that gets executed when this component is in scope
  - navigate to file show-dep.component.html and create table add button edit delete from bootstrap
  - put `selector: 'app-show-dep'` => `<app-show-dep></app-show-dep>` to department.component.html

  - model pop-up window form `https://getbootstrap.com/docs/4.3/components/modal/` copy to file show-dep.components.html
  - custom method to on button click and add `<app-add-edit-dep [dep]="dep" *ngIf="ActivateAddEditDepComp"></app-add-edit-dep>`
  - create addClick and closeClick function in file show-dep.components.ts

- department screen : add / edit

  - add function editClick and pass dataItem to function within file show-dep.component.html
  - create function editClick within class ShowDepComponent in file show-dep.component.ts
  - add @Input within class AddEditDepComponent in file add-edit-dep.component.ts and initialze departmentId in ngOnInit
  - add function addDepartment and updateDepartment within file add-edit-dep.component.html
  - import service `import {SharedService} from 'src/app/shared.service'`
  - create method addDepartment and updateDepartment within class AddEditDepComponent in file add-edit-dep.component.ts

- department screen : delete

  - add function deleteClick and pass dataItem to function within show-dep.component.html
  - create function deleteClick within class ShowDepComponent in file show-dep.component.ts

- show employee screen

  - copy code html form file show-dep.component.html to show-emp.component.html
  - copy code ts form file show-dep.component.ts to show-emp.component.ts and modify variable & method
  - add `<app-show-emp></app-show-emp>` to file employee.component.html

- upload photo, add/update employee screen

  - copy code html form file add-edit-dep.component.html to add-edit-emp.component.html
  - copy code ts form file add-edit-dep.component.ts to add-edit.component.ts and modify variable & method
  - create method loadDepartmentList and pass to method ngOnInit
  - create method uploadPhoto for upload photo and create function show img and upload image within file add-edit-emp.component.html

- sorting and filtering
  - navigate to file show-dep.component.ts and initialize variable `DepartmentIdFilter`, `DepartmentNameFilter`,`DepartmentListWithoutFilter`
  - add DepartmentListWithoutFilter to method refreshDepList()
  - create function FilterFn() and add to html in file show-dep.component.html
  - create button sorting in file show-dep.component.html and create function sortResult in file show-dep.component.ts
