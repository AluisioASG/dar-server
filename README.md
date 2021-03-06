# Dar Server

Node.js based filesystem backend for document archives ([Dar](http://github.com/substance/dar)). You can find examples [here](https://github.com/substance/dar/tree/master/examples).

## Install

```
$ git clone https://github.com/substance/dar-server.git
$ cd dar-server
$ npm install
```

## Integration into a custom Express application

```
let express = require('express')
let darServer = require('dar-server')
let path = require('path')

const port = 4000
const rootDir = path.resolve(path.join(__dirname, 'archives'))

let app = express()
darServer.serve(app, {
  port,
  serverUrl: 'http://localhost:' + port,
  rootDir
})

app.listen(port, () => {
  console.log(`Running dar-server on port ${port}`)
})
```

To avoid name clashes with your own express end-points you can provide an `apiUrl`

```
darServer.serve(app, {
  port,
  serverUrl: 'http://localhost:' + port,
  rootDir,
  apiUrl: '/archives'
})
```

## Command-line tool

This module comes with a command-line tool that starts `dar-server` in a new express instance.

```
$ npm install -g dar-server
$ dar-server ./my-archives
DAR server is running on http://localhost:4100
```

To start you could take the examples from the [DAR repository](https://github.com/substance/dar):
```
git clone https://github.com/substance/dar.git
```
and then start the dar-server using
```
dar-server ./dar/examples
```
After that you should be able to open
```
http://localhost:4100/!list
```
in the browser and see a listing of found archives.
Notice, that `dar-server` is just a backend for serving archives.
To be able to read and edit the context you need to use [Texture](https://github.com/substance/texture).