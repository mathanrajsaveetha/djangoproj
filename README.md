# Design a Website for Server Side Processing

## AIM:
To design a website to perform mathematical calculations in server side.

## DESIGN STEPS:

### Step 1:
Open up a terminal in your preffered location, and start a django project using ```djang-admin startproject serversideprocessing```
Next setup an app inside the project folder using ```django-admin startapp calculator``` 

### Step 2:
Once Created ,link your app to the project by adding it in the list of apps in settings.py file located inside the project folder.
Add access to your host in allowed host setting and add static folders path to your settings.py file. 

### Step 3:
Create a static folder and template folder and add all your required files for the project - Images .etc in 
your static folder. In the Template folder add your html files required for the pages. 

### Step 4:
The html file can be made reactive by using the templating feature availible in django. Using the templating feature add the required
variables in the html file. Make sure your HTML file contain html forms so it can return values from the html template to views.py file.

### Step 5:
Head to the views.py in your app folder and create required functions to render a particular page or template when requested by the client.
In the views.py file add functions and code to manage the required server side calculation. Connect the code to the render function to return the 
calculated values to the html template. 

### Step 6: 
Next start the server from the projects main directory using ```python3 manage.py runserver 0:<portnumber>```.
Now the pages can be accessed from all the routed addresses in urls.py. Now you can perform the serverside calculations.

Publish the website in the given URL.

## PROGRAM :
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MathanRaj's Calculator</title>
    <link rel="stylesheet" href="{% static 'index.css' %}">
</head>
<body>
    <h1 class="bg">Volume of a Cube</h1>
    <h1>Input A value below for calculation</h1>
    <form method="post">
        <inputs>
        {% csrf_token %}
        <input class="valin" type="number" name="num1">
        </inputs>

        <br>
        <inputs>
        
        <button type="submit" name="pow"> Calculate</button>
        </inputs>
        <input type="reset" type="submit" name="Reset Values" class="maxw">
    </form>
    <br>
    <br>
    <br>
    <br>
    <h1 class="bg1">Volume of the Cube =</h1>
    <h2 class="out">{{result}}</h2>
</body>
</html>
### File: index.html
```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Basic Calculator</title>
    <link rel="stylesheet" href="{% static 'index.css' %}">
</head>
<body>
    <h1 class="bg">Basic Calculator</h1>
    <h1>Input two values below for calculation</h1>
    <form method="post">
        <inputs>
        {% csrf_token %}
        <input class="valin" type="number" name="num1">
        <input class="valin" type="number" name="num2">
        </inputs>
        <br>
        <inputs>
        <button type="submit" name="add"> Add </button>
        <button type="submit" name="sub"> Subtract </button>
        <button type="submit" name="mul"> Multiply </button>
        <button type="submit" name="div"> Divide </button>
        <button type="submit" name="pow"> Power </button>
        </inputs>
        <input type="reset" type="submit" name="Reset Values" class="maxw">
    </form>
    <br>
    <br>
    <br>
    <br>
    <h1 class="bg1">Result of the calculation =</h1>
    <h2 class="out">{{result}}</h2>
</body>
</html>
```

### File: index.css
```css
* {
    margin: 0%;
    font-family: monospace;
}
h1{
    text-align: center;
}

.bg{
    padding: 1%;
    text-align: center;
    background-color: rgb(230, 122, 0);
    font-size: 48px;
}

.valin{
    font-size: 48px;
    border: 5px;
    border-style:ridge;
    border-color: coral;
    padding-left: 8%;
    padding-right: 8%;
}

inputs{
    display: flex;   
    flex-direction: row;
    justify-content: space-between;
}

button{
    background-color:rgb(230, 122, 0);
    font-size: 32px;
    padding-left: 6.5%;
    padding-right: 6.5%;
}

.maxw{
    width: 100%;
    font-size: 30px;
}

.bg1{
    float: left;
    text-align: center;
    background-color: rgb(230, 122, 0);
    font-size: 38px;
    width: 60%;
}

.out{
    float: right;
    text-align: center;
    border: 2px;
    border-style: double;
    border-color: blue;
    font-family: 'Courier New';
    font-size: 38px;
    width: 39%;
}
```

### File: views.py
```python
from django.shortcuts import render
# Create your views here.

def index(request):
    if request.method == 'POST':
        try:
            num1 = int(request.POST['num1'])
            num2 = int(request.POST['num2'])
        except ValueError:
            return render(request,'index.html',{'result':'Enter a valid number!'})
        if 'add' in request.POST:
            return render(request,'index.html',{'result':num1+num2})
        elif 'mul' in request.POST:
            return render(request,'index.html',{'result':num1*num2})
        elif 'sub' in request.POST:
            return render(request,'index.html',{'result':num1-num2})
        elif 'div' in request.POST:
            try:
                return render(request,'index.html',{'result':num1/num2})
            except ZeroDivisionError:
                return render(request,'index.html',{'result':'Cannot divide by zero!'})
        elif 'pow' in request.POST:
            return render(request,'index.html',{'result':num1**num2})
    return render(request,"index.html")
```

### File: Urls.py
```python
from django.contrib import admin
from django.urls import path
from calculator import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.index, name="mainpage")
]
```

## OUTPUT:



## Result:
Hence a website has been designed to perform mathematical calculations in server side.

