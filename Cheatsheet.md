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
