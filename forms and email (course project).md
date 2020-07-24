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
```python
from django.contrib import admin
from django.urls import path, include


urlpatterns = [
    path('admin/', admin.site.urls),
    path('addcourse/',include('course_app.urls')),
```
***app urls***
```python
from django.urls import path
from . import views

urlpatterns = [
    path('add', views.add_course, name = 'add_course')
]
```

***views.py***

```python
def add_course(request):
    return render(request, 'course/add_course.html')

```
create templates and add path in setings.py ``` os.path.join(BASE_DIR, 'templates') ```

***add_course.html***

```html
<html>
<head>
<title>add a course</title>
</head>
<body>
<p>working fine</p>
</body>
</html>
```

and then start with models create course model

***models.py***
```python 
from django.db import models


class CourseModel(models.Model):
    course_name = models.CharField(max_length=250)
    image = models.CharField(max_length=2083)
    description = models.CharField(max_length=500)

    def __str__(self):
        return self.course_name
```
make migrations & migrate

***forms.py*** create forms.py file 
```python
from django import forms


class CourseForm(forms.Form):
    course_name = forms.CharField(max_length=5)
    image_url = forms.CharField(max_length=2083)
    course_description = forms.CharField(max_length=400)
 ```

again ***views.py***
```python 
from django.shortcuts import render
from .forms import CourseForm


# Create your views here.
def add_course(request):
    form = CourseForm()
    return render(request, 'course/add_course.html', {'form': form})
```
```html
<html>
<head>
<title>add a course</title>
</head>
<body>
<form action="" method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit" name="submit" value="Add Course">
</form>

</body>
</html>
```

***views.py***
```python 
from django.shortcuts import render
from django.http import HttpResponse
from .forms import CourseForm
from .models import CourseModel


# Create your views here.
def add_course(request):
    form = CourseForm()
    if request.method == 'POST':
        form = CourseForm(request.POST)
        if form.is_valid():
            course = CourseModel(course_name=request.POST.get('course_name'),
                                 image=request.POST.get('image_url'),
                                 description=request.POST.get('course_description'))
            course.save()
            return HttpResponse('Course added successfully !!')
    return render(request, 'course/add_course.html', {'form': form})
```
