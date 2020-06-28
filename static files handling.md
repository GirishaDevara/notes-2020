###  static files
To handle static files we need to maintan them in main project folder


```settings.py```

```
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]
```


```templets```

```
<!DOCTYPE html>
<html>
<head>
	{% load static %}
	<title>Register page</title>
	<link rel="stylesheet" type="text/css" href="{% static 'css/bootstrap.min.css' %}">
	<script type="text/javascript" src="{% static 'js/bootstrap.min.js' %}"></script>
</head>
<body>
	<div class="container">
		<div class="row justify-content-center">
			<div class="card">
			<div class="card-header bg-info">Registration Page</div>
			<div class="card-body">
				<form method="POST">
					{% csrf_token %}
					<table>
						{{ form.as_table }}
					</table>
					<div class="card-footer">
					<input class="btn btn-info" type="submit" name="submit" value="Submit">
				</form>
			</div>
		</div>
		</div>
	</div>
</body>
</html>```


```staticeExampleCss.css```

```
.layout{
            width:40%;
		    margin:10vh auto 0 auto;
		    background-color:#a8e0b66e;
		    color: #6f062a;
		    font-family: cursive;
        }
.layout_login{
    width:40%;
    margin:10vh auto 0 auto;
    background-color:#9ca8ab30;
    color: #6f062a;
    font-family: cursive;
}
/*input{
        margin-left: -10%;
        margin-bottom: 1%;
        }*/
lable{
           float: left;
           margin-right : 10%;
           width: 150px;
           display: block;
  		   overflow: hidden;
        }

input[type = submit]{
            align-items: center;
        }
h1,#sub{
        text-align : center;
        }
h5{
        color:white;
        }
p{
        text-align:center;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 300px;
  margin: auto;
  text-align: center;
  font-family: arial;
}

.price {
  color: grey;
  font-size: 22px;
}

.card button {
  border: none;
  outline: 0;
  padding: 12px;
  color: white;
  background-color: #000;
  text-align: center;
  cursor: pointer;
  width: 100%;
  font-size: 18px;
}

.card button:hover {
  opacity: 0.7;
}
.card-img-top {
    width: 100%;
    height: 15vw;
    object-fit: cover;
}
```
