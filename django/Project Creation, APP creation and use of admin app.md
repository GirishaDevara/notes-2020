# Project Creation, APP creation and use of admin app
## Contents
1. [Project Creation](#Project-Creation)
2. [App Creation in Project](#App-Creation-in-Project)

****************************
## Project Creation

* Now, to create a Project in spcefied folder where to do and now open cmd in same path :
	```
			   path		                   creating project
	    D:\----\MyPractice>django-admin startproject College(projectname)
	    D:\---\MyPractice>cd College
	    D:\---\MyPractice\College
	    
	    
<img src='https://github.com/GirishaDevara/notes-2020/blob/master/django/Django-introduction/project.PNG' alt='project' />
	    
<img src='https://github.com/GirishaDevara/notes-2020/blob/master/django/Django-introduction/folder11.PNG' alt='folder1' />	    
	    
* Present we are in our Django Project(College) path.
* Check in browser wheather its working or not
  	```
	    D:\---\MyPractice\College>python manage.py runserver
	    localhost:8000/
	    it is localhost address --> http://127.0.0.1:8000/
	    it worked..!
	    
<img src='https://github.com/GirishaDevara/notes-2020/blob/master/django/Django-introduction/view.PNG' alt='view' />
  
## App Creation in Project
* Create a new App in Project
	```
	D:\~~~Girisha~~~\MyPractice\College>python manage.py startapp appname(Students)
	D:\~~~Girisha~~~\MyPractice\College>python manage.py runserver
	localhost:8000/
	it is localhost address --> http://127.0.0.1:8000/
<img src='https://github.com/GirishaDevara/notes-2020/blob/master/django/Django-introduction/app.PNG' alt='app' />	
<img src='https://github.com/GirishaDevara/notes-2020/blob/master/django/Django-introduction/folder11.PNG' alt='folder11' />
		
## **urls.py :**
* we have defaultly urls.py in  our created project(College) but we dont have urls.py in our own app so we should create new file with name urls.py in our own App(Students).
* Now we find the Students App in our project(College).
* Now goto Students app folder and create "urls.py" file and add like this

  	```
	from django.urls import path
	from Students import views
	urlpatterns=[
		path('index/',views.index,name="index"),

	]

> _NOTE:_ here i am importing views from Students app and mentioned one path because,if we browse localhost:8000/Students/index then it goes to views part index function and gives return template as a output. 

* goto (Students/views.py file) Students folder open views.py file and add like this.
	```
		
	from django.shortcuts import render
	from django.http import HttpResponse
	def index(request):
			return HttpResponse("<h2>Hello World</h2>")
			
* **HttpResponse  :** is a response class with string data. While HttpRequest is created by Django, HttpResponse is created by programmer.
* Create a function index in the views.py file. This function will be mapped from the Students/urls.py file.

> **_NOTE:_** import HttpResponse from http package and defining the function index.

* goto (College/urls.py file) College folder open urls.py file and add like this.
	
* Django already has mentioned a URL here for the admin. The path function takes the first argument as a route of string or regex type.The view argument is a view function which is used to return a response (template) to the user.


	
		from django.contrib import admin
		from django.urls import path,include
		from appname(Students) import views
		urlpatterns = [
	   		path('admin/', admin.site.urls),
			path('Students/',include('Students.urls'))
			]

* here we are importing the include because all the app urls are need to include in project urls.py file,so we are import include and giving path for browser.
* check in browser. localhost:8000/Students/index


	<img src='https://github.com/GirishaDevara/notes-2020/blob/master/django/Django-introduction/output.PNG' width="50%" height="30%" alt='output' />

* In anothe rway to represent url is without creating urls.py file in app Students add path in project urls.py file and import the Students app views in project urls.py file follow like this...
	```
		from django.contrib import admin
		from django.urls import path
		from appname(Students) import views
		urlpatterns = [
	   		path('admin/', admin.site.urls),
			path('index/',views.index,name='index'),
			]
		

* check in browser. localhost:8000/index

<img src='https://github.com/GirishaDevara/notes-2020/blob/master/django/Django-introduction/output.PNG' width="50%" height="30%" alt='output' />


* **You will get Hello World message**
