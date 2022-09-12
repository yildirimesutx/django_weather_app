#### API 
```
from django.shortcuts import render
from decouple import config
import requests

# Create your views here.

def home(request):
    API_key = config('API_KEY')
    city = "Bursa"
    url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_key}"

    response= requests.get(url)
    content = response.json()

    print(content)
```
API env file içine ekledik, requests kurduk ve import ettik,

pip install requests

requests.get(url) ile veri yakaladık

response değişkenine atadık

response.json()  json ile dic haline getirdik


gelen veriyi terminalde görüntülemek için 

from pprint import pprint

import ederek 

pprint(response.json())  terminalde daha sade halde görüntüledik

veriyi templatede göstermek için dic methodundan verileri aldık

context = {
        'city':content['name'],
        'temp':content['main']['temp'],
        'icon' : contentcontent['weather'][0]['icon'],
        'desc' : content['weather'][0]['description']

    }

kullanıcıdan sorgu yapabilmesi için get methodu ile 
form tanımladık, form tetiklendiğinde url aşağıdaki gibi değişmektedir.

içi dolu sorgu yapıldığında da aşağıdaki gibi gözükmektedir

http://127.0.0.1:8000/?name=
http://127.0.0.1:8000/?name=ankara

<form action="" method="get">

    <input type="text" name="name">
    <input type="submit" value="Add">
</form>


bu sebeple formdan gelen veriyi yakalamak için 

views.py da request.GET methodunu,  sonrs ki get  dic veri çekmek için

  city = request.GET.get('name')
    print(city)  

get('name') ile input içindeki name aynı olmak zorunda    
