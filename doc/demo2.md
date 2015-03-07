# Tiwtorial 2

Lawrlwytho ffeiliau mp3 neu wav gyda'r API Festival

Cewch lawrlwytho'r ffeiliau .mp3 neu .wav trwy defnyddio unrhyw sgript lawrlwytho (fel curl, wget, python urllib a.y.b)

Dyma rhai enghreifftiau o lawrlwytho ffeil o'r enw 'llais' yn y ddau fformat .mp3 a .wav gyda sawl ddull gwahanol

**Sylwer: Mae'n rhaid mewnbynnu eich allwedd API yn lle `ALLWEDD_API`

## Curl

```
$ curl  https://api.techiaith.org/festival/v1?api_key=ALLWEDD_API&text=mae%20hen%20wlad%20fy%20nhadau > llais.mp3

$ # ffeil wav
$ curl  https://api.techiaith.org/festival/v1?api_key=ALLWEDD_API&text=mae%20hen%20wlad%20fy%20nhadau&format=wav > llais.wav
```

## Wget


```
$ wget -O llais.mp3  https://api.techiaith.org/festival/v1?api_key=ALLWEDD_API&text=mae%20hen%20wlad%20fy%20nhadau

$ # ffeil wav
$ wget -O llais.wav https://api.techiaith.org/festival/v1?api_key=ALLWEDD_API&text=mae%20hen%20wlad%20fy%20nhadau&format=wav
```

## Python 2

```
>>> import urllib
>>> with open('llais.mp3', 'wb') as f:
...     f.write(urllib.urlopen("https://api.techiaith.org/festival/v1?api_key=ALLWEDD_API&text=mae%20hen%20wlad%20fy%20nhadau").read())
... 
>>>
>>> # ffeil wav
... 
>>> with open('llais.wav', 'wb') as f:
...     f.write(urllib.urlopen("https://api.techiaith.org/festival/v1?api_key=ALLWEDD_API&text=mae%20hen%20wlad%20fy%20nhadau&format=wav").read())
...
```

## Python 3

Mae Python 3 yn defnyddio `urllib.request.urlopen` yn lle `urllib.urlopen`.