## Superuser and Role of superuser

Giving all permissions to particular user(admin).

Generating admin sites for your staff or clients to add, change, and delete content is tedious work that doesn’t require
much creativity. For that reason, Django entirely automates creation of admin interfaces for models

> **_Note:_**  The admin isn’t intended to be used by site visitors. It’s for site managers.


**step-6**

open the command prompt from the location of project's **manage.py**

First we’ll need to create a user who can login to the admin site. Run the following command:

```
python manage.py createsuperuser
```

Enter your desired username and press enter

```
Username: admin
```

You will then be prompted for your desired email address:

```
Email address: admin@example.com
```

The final step is to enter your password. You will be asked to enter your password twice, the second time as a
confirmation of the first

```
Password: **********
Password (again): *********
```

**end-step-6**

finally you will get **Superuser created successfully** message.

**Start the development server**

```
python manage.py runserver
```

Now, open a Web browser and go to “/admin/” on your local domain – e.g., http://127.0.0.1:8000/admin/


#### If you want to manage app from admin do step-7

**step-7** do this in YOUR_PROJECT_NAME/YOUR_APP_NAME/admin.py

```
from django.contrib import admin

# Register your models here.

from YOUR_APP_NAME.models import Register


admin.site.register(Register)
```
