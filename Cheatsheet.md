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

[Streams lecture](https://docs.google.com/presentation/d/16uT5GMOcTcs2xcbqvlCb3RetpFATil5nmXyZK7uvEdc/edit#slide=id.g32b61634d9_0_77)
Voorbeeld van een stream
```
var fs = require('fs')
var read = fs.createReadStream

read('in.txt')
  .pipe(process.stdout)
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
De directory van een specefiek path krijgen 

  
  ```
  var path = require('path')
path.dirname('~/backend/index.js')
//=> '~/backend' 
```
Package maken 

 ```
 npm-init --yes
  
```
#### Require van een path

Meer over require en node modules 
[Lecture Require](https://docs.google.com/presentation/d/16uT5GMOcTcs2xcbqvlCb3RetpFATil5nmXyZK7uvEdc/edit#slide=id.g32b61634d9_0_400)

```
var sum = require('../sum')
```

![URL eplained](https://imgur.com/a/mxDpv)


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

```
app.get('/',calback)
 ```


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
#### Body-parser

```
var slug = require('slug')
var bodyParser = require('body-parser')


…

express()
  .use(express.static('static'))
  .use(bodyParser.urlencoded({extended: true}))
  .set('view engine', 'ejs')
  .set('views', 'view')
  .get('/', movies)
  .post('/', add)
  .get('/add', form)
  .get('/:id', movie)
  .use(notFound)
  .listen(8000)

```
#### The function to grab the data from lecture 4
[Lecture 4](https://docs.google.com/presentation/d/1PfEaV-jQdqKWByca9txp38yD8LWIDEWZzldNYBMwUNI/edit#slide=id.g3230fb1b6e_0_355)
```
function form(req, res) {
  res.render('add.ejs')
}

function add(req, res) {
  var id = slug(req.body.title).toLowerCase()

  data.push({
    id: id,
    title: req.body.title,
    plot: req.body.plot,
    description: req.body.description
  })

  res.redirect('/' + id)
}
```
#### Serve static files
In je index.js
Om bijvoorbeeld afbeeldingen te hosten kan je in express zeggen
Zorg er wel voor dat je afbeeldingen ook echt in die map zitten 
```.use(express.static('public/images'));```

#### Error Handling Express

```
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})

```
#### Middelware

```
app.use()=req, res, next> {

```

Wat doet next? Next maakt het mogelijk om express (middelware/ app) te vertellen wanneer hij naar de vogende functie mag gaan.
Stel je hebt onderstaande code dit is een lege functie
```
app.use()=req, res, next> {

```
Als je nu je pagina zou vernieuwen toont hij de pagina maar chrome blijft laden.
Door de code te wijzigen naar:
```
app.use()=req, res, next> {
next()
```
Gaat de code netjes verder na deze functie.



#### Link naar Lynda en Udemy 
[Lynda express](https://www.lynda.com/Node-js-tutorials/Initial-server-files-folders/633869/671247-4.html?srchtrk=index%3a2%0alinktypeid%3a2%0aq%3aexpress.js%0apage%3a1%0as%3arelevance%0asa%3atrue%0aproducttypeid%3a2)

[Udemy Express ](https://www.udemy.com/the-complete-nodejs-developer-course-2/learn/v4/t/lecture/5525322?start=0)

