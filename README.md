### How to Create a Wep App with Django in VisualStudioCode
https://www.youtube.com/watch?v=OTmQOjsl0eg&ab_channel=Telusko (TutorialVideo1.mp4)


---
**Step 1 - Tools/TestEnviroment**

- Windows 10 Pro 22H2
- Anaconda 24.1.2 (Python 3.11.7)
- VisualStudioCode 1.87.2
- Django 5.0.3

---
**Step 2 - Preparation**

Open VisualStudioCode and then PowerShellTerminal

Create project folder:
`PS C:\Users\WORKINGSTATION\Desktop> mkdir WebAppCakeCorner`

Navigate into project folder:
`PS C:\Users\WORKINGSTATION\Desktop> cd .\WebAppCakeCorner\`

Check python version:
`PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> python --version`
`
Python 3.11.7`

Check pip version:
`PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> pip3 --version`
`
pip 23.2.1 from G:\20_Meine_Projekte\WEBPAGE_(Django)\WebAppCakeCorner\.venv\Lib\site-packages\pip (python 3.11)`


---
**Step 3 - Virtual Enviroment**

Create an virtual enviromnt:
`PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> python -m venv .venv`

activate virtual enviroment
`PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> .\.venv\Scripts\activate`

If the following error occurs:
```
.\.venv\Scripts\activate : File C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner\.venv\Scripts\Activate.ps1 cannot be loaded because running scripts is disabled on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1
+ .\.venv\Scripts\activate
+ ~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

then try first: 
`PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> Set-ExecutionPolicy Unrestricted -Scope Process`

and then this again:
`PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> .\.venv\Scripts\activate`

install `requirements.txt` file
`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> pip install -r requirements.txt`

Info only: collecting all your needed python packages using in this project
`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> pip freeze > requirements.txt` 

---
**Step 4 - install django**

install django
`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> pip install django`

check django version
`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> django-admin --version`
`
5.0.3`

---
**Step 5 - first django project "WebAppCakeCornerV1"**

`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> mkdir Projects`

`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner> cd .\Projects\`

`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner\Projects> django-admin startproject WebAppCakeCornerV1`

`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner\Projects> cd .\WebAppCakeCornerV1\`

run server first time
`(.venv) PS C:\Users\WORKINGSTATION\Desktop\WebAppCakeCorner\Projects\WebAppCakeCornerV1> python manage.py runserver`


---
**Step 6 - first django app** 

`(.venv) PS C:\Users\WORKINGSTATION\Desktop\Zuhal\Projects\WebAppCakeCornerV1> python manage.py startapp CheesecakeShop`

---
**[24:23-31:57] Step 6 - "Hello World"** 

- [ ] Inside `...\Projects\WebAppCakeCornerV1\CheesecakeShop\` create a file `urls.py`

- [ ] Inside `...\Projects\WebAppCakeCornerV1\CheesecakeShop\urls.py` add the following code:
```
from django.urls import path
from . import views

urlpatterns = [path('',views.home, name='home')]
```

- [ ] Inside `...\Projects\WebAppCakeCornerV1\CheesecakeShop\views.py` add the following code:
```
from django.shortcuts import render
from django.http import HttpResponse

def home(request):
    return HttpResponse("<h1>Hello World</h1>")
```

- [ ] Inside `...\Projects\WebAppCakeCornerV1\WebAppCakeCornerV1\urls.py` in the list `urlpatterns` add ` path('',include('CakeShop.urls')),` and import also the `include` function:
```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('',include('CheesecakeShop.urls')),
    path('admin/', admin.site.urls),
]
```
- [ ] run the server and check the result


---
**[31:57-40:30] Step 7 - First Page using django template language Part 1**

- [ ] Inside `...\Projects\WebAppCakeCornerV1\` create a folder `templates`

- [ ] Inside `...\Projects\WebAppCakeCornerV1\templates` create a file `home.html`

- [ ] Inside `...\Projects\WebAppCakeCornerV1\templates\home.html` add te following code:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>my Title</title>
</head>
<body>

    <p>my Text</p>
    
</body>
</html>
```

- [ ] Inside `...\Projects\WebAppCakeCornerV1\WebAppCakeCornerV1\settings.py` in  `TEMPLATES` inside `DIRS` add `os.path.join(BASE_DIR,'templates')` and add `import os` at the top
```
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR,'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

- [ ] Inside `...\Projects\WebAppCakeCornerV1\CheesecakeShop\views.py` change the code:
```
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def home(request):
    return render(request, "home.html")
```

- [ ] run the server and check the result (Tipp: access from every device in local network: `python manage.py runserver 192.168.1.183:8000`, note you need to add your IP address inside `...\Projects\WebAppCakeCornerV1\WebAppCakeCornerV1\settings.py` the host: `ALLOWED_HOSTS = ['192.168.1.183', 'localhost', '127.0.0.1']`)


### How to Create a Weppage using html and css
https://www.youtube.com/watch?v=cLOT0APQzDs&ab_channel=Mr.WebDesigner (TutorialVideo2.mp4)


















