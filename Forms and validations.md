# Model Forms
Before starting we need to create a new app with name course, and register app in settings.py

***urls.py***

```python
path('courses/',include('subjects.urls')),
```
complete entire url in app urls

***app urls.py***

```python 
 path('add', views.add_subject, name='add'),
```

***models.py***

```python 
from django.db import models


class Courses(models.Model):
    course_name = models.CharField(max_length=200)
    image_url = models.CharField(max_length=2083)
    details = models.CharField(max_length=500)
    
    def __str__(self):
        return self.course_name
```
make migrations & migrate

## create Form.py

***form.py***

```python 
from django.forms import ModelForm
from .models import Course

class Course_form(ModelForm):
    class Meta:
        model = Course
        fields = '__all__'

```

***views.py***
```python
from django.shortcuts import render
from .models import Course
from .forms import Course_form


def add_subject(request):
    form = Course_form()
    return render(request, 'course.html', {'form':form})
```
***html
<form action="" method="POST">
    {% csrf_token %}
    {{form.as_p}}
    <input type="submit" name="submit" value="submit">
</form>
```

***views.py***

```python 
def add_subject(request):
    if request.method == "POST":
        form = Course_form(request.POST)
        if form.is_valid():
            form.save()
            return HttpResponse('course added successfully')
    form = Course_form()
    return render(request, 'course.html', {'form': form})
```

