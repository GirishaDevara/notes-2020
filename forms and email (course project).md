# Forms
  - Normal Forms
  - Model Forms

```python
django-admin startproject training
python manage.py startapp course_app
```

register app in settings.py file 

Create urls.py in app and create path in main urls file
***main urls***
```pythonfrom django.contrib import admin
from django.urls import path, include


urlpatterns = [
    path('admin/', admin.site.urls),
    path('course/',include('course_app.urls')),
    path('user/',include('user.urls')),
]
```
***app urls***
```python
from django.urls import path
from . import views


urlpatterns = [
    path('student/register', views.student_register, name='student_register'),
    path('faculty/register', views.faculty_register, name='faculty_register'),
    path('student/login', views.student_login, name='student_login'),
]
```


***views.py***

```python
from django.shortcuts import render
from django.http import HttpResponse
from .forms import StudentRegisterForm, FacultyRegisterForm, StudentLoginForm
from .models import StudentRegister, FacultyRegister



def student_register(request):
    form = StudentRegisterForm(request.POST)
    # if request.method == 'POST':
    if form.is_valid():
        student = StudentRegister(firstName=request.POST.get('firstName'), lastName=request.POST.get('lastName'),
                                  emailId=request.POST.get('emailId'), phoneNo=request.POST.get('phoneNo'),
                                  age=request.POST.get('age'), gender=request.POST.get('gender'),
                                  date_of_birth=request.POST.get('date_of_birth'))
        student.save()
        return HttpResponse('Student added')
    return render(request, 'user/student_registration.html', {'form': form})


def faculty_register(request):
    form = FacultyRegisterForm(request.POST)
    if request.method == 'POST':
        if form.is_valid():
            form.save()
            return HttpResponse('faculty_register done')
    return render(request, 'user/faculty_register.html', {'form':form})

```


create templates and add path in setings.py ``` os.path.join(BASE_DIR, 'templates') ```

***add_course.html***

```html<html>
<head>
    <title>Faculty Registration</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>
</head>
<body>
	<div class="container">
		<div class="row justify-content-center">
			<div class="card">
			<div class="card-header bg-info">Faculty Registration Page</div>
			<div class="card-body">
				<form method="POST" >
					{% csrf_token %}
					<table>
						{{ form.as_table }}
					</table>
					<div class="card-footer">
					<input class="btn btn-info" type="submit" name="submit" value="Submit">
					</div>
				</form>
			</div>
		</div>
		</div>
	</div>
</body>
</html>
```

and then start with models create course model

***models.py***
```python 
from django.db import models


class StudentRegister(models.Model):
    gender_vals = [('Male', 'Male'), ('FeMale', 'FeMale')]
    firstName = models.CharField(max_length=100)
    lastName = models.CharField(max_length=100)
    emailId = models.EmailField(null=True)
    phoneNo = models.CharField(max_length=10)
    age = models.IntegerField(null=True)
    gender = models.CharField(max_length=10, choices=gender_vals)
    date_of_birth = models.DateField(null=True)

    def __str__(self):
        return self.firstName


class FacultyRegister(models.Model):
    gender_vals = [('Male', 'Male'), ('FeMale', 'FeMale')]
    firstName = models.CharField(max_length=100)
    lastName = models.CharField(max_length=100)
    emailId = models.EmailField(null=True)
    phoneNo = models.CharField(max_length=10)
    age = models.IntegerField(null=True)
    gender = models.CharField(max_length=10, choices=gender_vals)
    date_of_birth = models.DateField(null=True)

    def __str__(self):
        return self.firstName
```
make migrations & migrate

***forms.py*** create forms.py file 
```python
from django import forms
from django.forms import ModelForm
from .models import FacultyRegister, StudentRegister



class StudentRegisterForm(forms.Form):
    firstName = forms.CharField(label='Your name',max_length=100)
    lastName = forms.CharField(max_length=100)
    emailId = forms.EmailField(required=False)
    phoneNo = forms.CharField(max_length=10)
    age = forms.IntegerField(required=False)
    gender = forms.ChoiceField(choices=[('f','Female'),('m','male')])
    date_of_birth = forms.DateField(required=False)


class FacultyRegisterForm(forms.ModelForm):
    class Meta:
        model = FacultyRegister
        fields = "__all__"

 ```

# Email sending

***settings.py***
```python
EMAIL_USE_TLS = True
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_HOST_USER = 'gireesha.d@apssdc.in'
EMAIL_HOST_PASSWORD = 'satya147'
```

### Form.cleaned_data
Each field in a Form class is responsible not only for validating data, but also for “cleaning” it – normalizing it to a consistent format. This is a nice feature, because it allows data for a particular field to be input in a variety of ways, always resulting in consistent output.
### form.data
***views.py***
```python 
from django.shortcuts import render
from django.http import HttpResponse
from .forms import StudentRegisterForm, FacultyRegisterForm
from .models import StudentRegister, FacultyRegister
from django.core.mail import EmailMessage
from course import settings


def student_register(request):
    form = StudentRegisterForm(request.POST)
    # if request.method == 'POST':
    if form.is_valid():
        student = StudentRegister(firstName=request.POST.get('firstName'), lastName=request.POST.get('lastName'),
                                  emailId=request.POST.get('emailId'), phoneNo=request.POST.get('phoneNo'),
                                  age=request.POST.get('age'), gender=request.POST.get('gender'),
                                  date_of_birth=request.POST.get('date_of_birth'))
        student.save()
        name = form.data['firstName']
        sub = 'registration'
        body = 'Hey ' + name.title() + ' Congratulations your certificate is ready!!'
        receiver = form.data['emailId']
        sender = settings.EMAIL_HOST_USER
        email_mgs = EmailMessage(sub, body, sender, [receiver])
        # file attaching
        email_mgs.send()

        return HttpResponse('Student added')
    return render(request, 'user/student_registration.html', {'form': form})


def faculty_register(request):
    form = FacultyRegisterForm(request.POST)
    if request.method == 'POST':
        if form.is_valid():
            form.save()
            name = form.data['firstName']
            sub = 'registration'
            body = 'Hey ' + name.title() + ' Congratulations your certificate is ready!!'
            receiver = form.data['emailId']
            sender = settings.EMAIL_HOST_USER
            email_mgs = EmailMessage(sub, body, sender, [receiver])
            return HttpResponse('faculty_register done')
    return render(request, 'user/faculty_register.html', {'form':form})
```
