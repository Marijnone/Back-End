# Backend cheat-sheet 


### server in node.js

Dit is hoe een server wordt gemaakt zonder express.js
```
 var http = require('http')

http.createServer(onrequest).listen(8000)

function onrequest(req, res) {
  res.statusCode = 200
  res.setHeader('Content-Type', 'text/html')
  res.end('<h1>Hello World!</h1>\n')
} 
```
Lezen van een text file als je bijvoorbeeld "echo Hallo allemaal > in.txt" zou uitvoeren, dan kan node dit uitlezen met de volgende code.

```
var fs = require('fs')
var read = fs.createReadStream

read('in.txt')
  .pipe(process.stdout)
  ```
  De directory van een specefiek path krijgen 
  
  ```
  var path = require('path')
path.dirname('~/backend/index.js')
//=> '~/backend' 
```
Lezen van een file zonder stream
```
var fs = require('fs')
fs.readFile('/etc/passwd', onreadfile)
function onreadfile(err, data) {
  if (err) throw err
  console.log('Data: ', data)
}
```
Package maken 

 ```
 npm-init --yes
  
```
![](https://imgur.com/a/mxDpv)


http status codes: [link](https://httpstatuses.com/)

server maken in express
 ```
 var express = require('express')

express()
  .get('/', onhome)
  .listen(1900)

function onhome(req, res) {
  res.send('<h1>Hello World</h1>\n')
}
```

#### Callbacks
>In computer programming, a callback is a piece of executable code that is passed as an argument to other code, which is expected to call back (execute) the argument at some convenient time. The invocation may be immediate as in a synchronous callback or it might happen at later time, as in an asynchronous callback.>



#### Events
Using events is much simpler. It’s like callbacks with a name!
```
var client = require('my-chat-client')

client.on('connect', onconnect)
client.on('connectionerror', onconnectionerror)
client.on('disconnect', ondisconnect)
client.on('message', onmessage)
client.connect('http://mychatserver.com')


```



```
app.get('/',calback)
 ```
 #### Templates
 
 syntax:  ```<h1> <% data.title %> </h1> ```
 
 Gebruik van een template en het renderen hiervan
 
 ```
 express()
  .use(express.static('static'))
  .set('view engine', 'ejs')
  .set('views', 'view')
  …

function movies(req, res) {
  res.render('list.ejs', {data: data})
}

function movie(req, res, next) {
  …
  res.render('detail.ejs', {data: movie})
}

function notFound(req, res) {
  res.status(404).render('not-found.ejs')
}
```

#### Formulieren

[Slides week 4](https://docs.google.com/presentation/d/1PfEaV-jQdqKWByca9txp38yD8LWIDEWZzldNYBMwUNI/edit#slide=id.g3230fb1b6e_0_395)
``` <title>Add a movie - My movie website</title>
<h1>Add a new movie</h1>
<form action=/ method=post>
  <label>Title <input name=title></label>
  <label>
    Plot (short)
    <input name=plot>
  </label>
  <label>
    Description (long)
    <textarea
      name=description
      rows=5
    ></textarea>
  </label>
  <button>Add</button>
</form>




```


#### Error Handling Express

```
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})

```
