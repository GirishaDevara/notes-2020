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
		
