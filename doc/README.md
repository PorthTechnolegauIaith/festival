[scroll down for english](#festival-api)

# API Festival

Mae'r API yn gweithio dros HTTPS GET, felly gellir defnyddio unrhyw iaith/meddalwedd HTTP er mwyn cysylltu at yr API.

## Tiwtorialau

Mae [Tiwtorial 1](demo1.md) yn enghraifft o sut i ddefnyddio'r API o fewn tudalen HTML gyda'r tag 'audio' HTML5.

Mae [Tiwtorial 2](demo2.md) yn dangos sut y gellir llwytho ffeiliau mp3 o'r API i lawr er mwyn eu storio'n lleol.

## Fersiwn Cyfredol

Mae un fersiwn o API Festival ar gael: v1 neu 'fersiwn un'.
Bydd yr URL yn newid gyda phob fersiwn newydd o'r API. Ar hyn o bryd, dylid defnyddio `/v1` ar gyfer fersiwn un.

## Schema

Mae cysylltiad â'r API yn gweithio dros HTTPS yn unig, gan ddefnyddio'r parth `api.techiaith.org/festival`. Mae'r API yn anfon ffeiliau mp3 yn unig, mewn ffrwd sain.

## Paramedrau

| Paramedr     | Disgrifiad | Sylwadau |
|--------------|------------|----------|
| `api_key`    | Eich allwedd API, ar gael o'r Canolfan APIs (https://api.techiaith.org) | angenrheidiol |
| `text`       | Y testun i'w lleferu. Wedi'i fformatio yn ôl RFC 3986 yn ôl RFC 3986 (percent-encoded) | angenrheidiol |
| `stretch`    | Rhif (float) rhwng 0 a 5 sy'n newid cyflymder y llais. Mae rhif <1 yn cyflymu'r llais, a rhif >1 yn arafu'r llais. Rhagosodiad: `1.2` | dewisol |
|  `pitch`     | Rhif (float) rhwng 1 a 9 sy'n newid traw y llais. Mae rhif isel yn cynhyrchu traw isel, ac mae rhif uchel yn cynhyrchu traw uchel. Rhagosodiad: `5` | dewisol |
| `format`     | Fformat y ffeil allbwn. Gallwch ddewis rhwng `mp3` a `wav`. Rhagosodiad: `mp3` | dewisol |    
| `lang`       | Yr iaith ar gyfer unrhyw destun fydd yn cael ei ddychwelyd (e.e. negeseuon gwall). Dewis o `en` neu `cy`. Rhagosodiad: `cy` | dewisol |

### Enghraifft

```
$ curl https://api.techiaith.org/festival/v1?api_key=123&text==mae%20hen%20wlad%20fy%20nhadau > allan.mp3
$ file allan.mp3
allan.mp3: MPEG ADTS, layer III, v2,  56 kbps, 16 kHz, Monaural
```

## Cyfyngu nifer yr alwadau yr awr

Mae gan yr API gyfyngiad ar y nifer o alwadau y gellir eu gwneud mewn awr.

Mae'r cyfyngiad yn un hael iawn, ac rydym yn ystyried y bydd hyn yn ddigon ar gyfer y rhan fwyaf o'n defnyddwyr. Os ydych eisiau cynyddu nifer y galwadau at yr API sydd gennych, cysylltwch â ni.

Gellir gweld cyfanswm nifer eich galwadau ar unrhyw adeg drwy edrych ar 'HTTP headers' yn eich galwad API:

```
$ curl -D headers.txt https://api.techiaith.org/festival/v1?api_key=123&text==mae%20hen%20wlad%20fy%20nhadau > /dev/null
$ cat headers.txtq                                                            

HTTP/1.1 200 OK
Date: Wed, 17 Dec 2014 13:57:52 GMT
Content-Type: audio/mpeg
Transfer-Encoding: chunked
Connection: keep-alive
X-RATELIMIT-REMAINING: 293
X-RATELIMIT-RESET: 1418828048
X-RATELIMIT-LIMIT: 300
```

Mae'r headers yn cynnwys yr holl wybodaeth sydd ei hangen:

| Enw'r Header | Disgrifiad |
|--------------|------------|
| X-RateLimit-Limit | Y nifer mwyaf o alwadau allwch chi eu gwneud mewn awr |
| X-RateLimit-Remaining | Y nifer o alwadau sydd gennych ar ôl yn y 'blwch' cyfyngu presennol |
| X-RateLimit-Reset | Yr amser y bydd y 'blwch' cyfyngu presennol yn cael ei ail-osod, mewn [eiliadau epoch UTC](http://en.wikipedia.org/wiki/Unix_time) |

Os oes arnoch angen yr amser mewn fformat gwahanol, gellir gwneud hyn gydag unrhyw iaith raglennu fodern. Er enghraifft, gellir gwneud hyn trwy gonsol eich porwr (gyda Javascript) a dychwelyd gwrthrych 'Javascript Date'.


```javascript
new Date(1416237399 * 1000)
Date 2014-11-17T15:16:39.000Z
```

Ar ôl i chi fynd dros eich nifer mwyaf o alwadau yr awr, byddwch yn derbyn gwall gan y gweinydd (403 Forbidden):

```
curl -i https://api.techiaith.org/festival/v1?api_key=65f7ef45-fe56-4aac-a787-9a64fa065af4&text=mae%20hen%20wlad%20fy%20nhadau

HTTP/1.1 403 Forbidden
Server: nginx/1.4.6 (Ubuntu)
Date: Wed, 17 Dec 2014 16:39:55 GMT
Content-Type: text/html
Content-Length: 257
Connection: keep-alive
X-RATELIMIT-REMAINING: 0
X-RATELIMIT-LIMIT: 300
X-RATELIMIT-RESET: 1418836717

ERROR 403 Forbidden: Rydych chi wedi mynd dros eich cyfyngiad nifer yr alwadau yr awr
```

------

## Festival API

The API works using HTTPS GET, meaning you can use it with any programming language/software package of your choice which works over HTTP

## Current Version

Currently, there is only one version of the Festival API available: v1 or 'version 1'.

## Schema

The connection to the API is over HTTPS only, from the domain `api.techiaith.org/festival`. The API sends mp3 files as audio streams to the receiver.

## API Parameters

| Parameter   | Description | Notes |
|------------|------------|----------|
| `api_key`  | Your API key, from the API Centre (https://api.techiaith.org) | required |
| `text`     | The text to speak. Formatted according to RFC 3986 (percent-encoded) | required |
| `stretch`  | Number (float) between 0 and 5 which alters the speed of the voice. A number <1 speeds up the voice, and a number >1 slows down the voice. Default: `1.2` | optional |
| `pitch`    | Number (float) between 1 and 9 which alters the pitch of the voice. A low number gives a low pitch, and a high number a high pitch. Default: `5` | optional |
| `format`   | Format of the output audio file. Can be either `mp3` or `wav`. Default: `mp3` | optional |
| `lang`     | The language for any text returned by the API (e.e. grammar suggestion sentences, error messages). Choices: `en` or `cy`. Default: `cy` | optional |

### Example


```
$ curl https://api.techiaith.org/festival/v1?api_key=123&text==mae%20hen%20wlad%20fy%20nhadau > out.mp3
$ file out.mp3
out.mp3: MPEG ADTS, layer III, v2,  56 kbps, 16 kHz, Monaural
```

## Rate Limiting

The API has a limit on the number of requests you can make per hour, linked to your API key.

You are initially given a high number of requests per hour, which we believe will be enough for most of our users.
If you would like to increase the number of requests you can make to the API per hour, use the form within the 'API Centre'.

You can view the number of requests you have made/have remaining at any time by looking at the 'HTTP headers' of any response to the API:

```
$ curl -i https://api.techiaith.org/festival/v1?api_key=rhywbeth&text=un%20dau%20tri                                                            

HTTP/1.1 200 OK
Date: Mon, 17 Nov 2014 14:41:21 GMT
Content-Type: application/json
Content-Language: cy
X-Ratelimit-Remaining: 276
X-Ratelimit-Limit: 300
X-Ratelimit-Reset: 1416237399
```

The headers contain all information you may require:

| Header Name | Description |
|--------------|------------|
| X-RateLimit-Limit | Maximum number of requests you can make per hour (rate limit) |
| X-RateLimit-Remaining | The number of requests remaining in the current rate limit window |
| X-RateLimit-Reset | The time at which the current rate limit window resets in [UTC epoch seconds](http://en.wikipedia.org/wiki/Unix_time) |


If you need the time in a different format, any modern programming language can get the job done. For example, if you open up the console on your web browser, you can easily get the reset time as a JavaScript Date object.

```javascript
new Date(1416237399 * 1000)
Date 2014-11-17T15:16:39.000Z
```

Once you go over the rate limit you will receive an error response:

```
curl -i https://api.techiaith.org/festival/v1?api_key=65f7ef45-fe56-4aac-a787-9a64fa065af4&text=mae%20hen%20wlad%20fy%20nhadau&lang=en

HTTP/1.1 403 Forbidden
Server: nginx/1.4.6 (Ubuntu)
Date: Wed, 17 Dec 2014 16:40:16 GMT
Content-Type: text/html
Content-Length: 257
Connection: keep-alive
X-RATELIMIT-REMAINING: 0
X-RATELIMIT-LIMIT: 300
X-RATELIMIT-RESET: 1418836717

ERROR 403 Forbidden: You have exceeded your request limit
```
