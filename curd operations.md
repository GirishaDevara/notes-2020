## create 


***models.py***
```python
from django.db import models


class SignUp(models.Model):
    name = models.CharField(max_length=50)
    roll_num = models.CharField(max_length=15, null=True)
    gender_list = [('Male','Male'),('Female','Female')]
    gender = models.CharField(max_length=10,choices=gender_list)
    email = models.EmailField()
    age = models.IntegerField()

    def __str__(self):
        return self.name + self.roll_num
```

***views.py***

```python
from django.shortcuts import render
from .models import SignUp


def signup(request):
    return render(request,'testing/signup.html')
```
***signup.html***

```html
<!DOCTYPE html>
<html>
<head>
    {% load static %}
	<title>Sign Up Page</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
</head>
<body>
<div class="container">
		<div class="row justify-content-center">
			<div class="card">
	    		<div class="card-header bg-success">Registration Page</div>
                <div class="card-body">
                    <form method="POST">
                        {% csrf_token %}
                        <input type="text" name="name" placeholder="Name"><br>
                        <input type="text" name="role_num" placeholder="Roll number"><br>
                        <input type="email" name="email" placeholder="Email "><br>

                        <input type="text" name="age" placeholder="age"><br>
                        Male :<input type="radio" name="gender" value="Male"><br>
                        Female :<input type="radio" name="gender" value="Female"><br>
                        <div class="card-footer bg-success ">
                        <input type="submit" name="submit" value="SAVE"><br>
                        </div>
                    </form>
                </div>
            </div>
        </div>
</div>
</body>
</html>
```

after edit vies.py for post method
***views.py***
```python 
def signup(request):
    if request.method == 'POST':
        name = request.POST.get('name')
        roll_num = request.POST.get('rollnum')
        email = request.POST['email']
        age = request.POST.get('age')
        gender= request.POST['gender']
        obj = SignUp(name=name,roll_num=roll_num,email=email,
                     age=age, gender=gender)
        obj.save()
        return HttpResponse("signUp done successfully")
    return render(request,'testing/signup.html')
```

### for display  details
***urls.py***

```python
 path('display/',views.display, name='display'),
 ```
***views.py***
```
def display(request):
    data = SignUp.objects.all()
    return render(request,'testing/display.html',{'data':data})
```

***dispaly.html***
```html
<!DOCTYPE html>
<html>
<head>
	<title>Display Details</title>
</head>
<body>
	<table border="1">
		<thead>
			<th>name</th>
			<th>age</th>
        <th>gender</th>
        <th>rollnum</th>
        <th>email</th>
		</thead>
		<tbody>
			{% for i in data %}
				<tr>
                <td>{{ i.name }}</td>
                <td>{{ i.age }}</td>
                <td>{{ i.gender }}</td>
                <td>{{ i.roll_num }}</td>
                <td>{{ i.email }}</td>
				</tr>
			{% endfor %}
		</tbody>
	</table>
</body>
</html>
```
