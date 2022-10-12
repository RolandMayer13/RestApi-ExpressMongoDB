# Build A REST API With Node.js, Express, & MongoDB - Quick
This project was created from a tutorial by Web Dev Simplified.  
Watch YouTube video [Build A REST API With Node.js, Express, & MongoDB - Quick](https://www.youtube.com/watch?v=fgTGADljAeg) by [Web Dev Simplified](https://www.youtube.com/c/WebDevSimplified).

## Tools used in this project
- [VSCode](https://code.visualstudio.com/)
  - [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) extension by Huachao Mao
- [Docker](https://www.docker.com/)

## Step-by-step instructions to create project
- Create project folder
- Navigate inside project folder
- Open terminal
```Terminal
> npm init
```
- Install dependencies
  - [Mongoose](https://mongoosejs.com/) (elegant mongodb object modeling for node.js)
```Terminal
> npm i express mongoose
```
- Install development dependencies
  - [dotenv](https://github.com/motdotla/dotenv#readme) (Dotenv is a zero-dependency module that loads environment variables from a .env file into process.env.)
  - [nodemon](https://nodemon.io/) (Nodemon is a utility that will monitor for any changes in your source and automatically restart your server.)
```Terminal
> npm i --save-dev dotenv nodemon
```
- Open package.json
- Create "devStart" script
```json
"scripts": {
  "devStart": "nodemon server.js"
}
```
- Create .env file
- Create .gitignore file
```
.env
node_modules
```
- Create server.js file
```js
// server.js
const express = require('express')
const app = express()

app.listen(3000, () => console.log('Server Started'))
```
- Start server (press ctrl-c to stop server)
```Terminal
> npm run devStart
```
- Run MongoDB in docker container (`docker stop mongodb` stops the container)
```Terminal
> docker pull mongo
> docker run --name mongodb -d -p 27017:27017 mongo
```
- Connect server to MongoDB
```js
// server.js
const express = require('express')
const app = express()
// new code starts here...
const mongoose = require('mongoose')

mongoose.connect('mongodb://localhost/subscribers', { useNewUrlParser: true })
const db = mongoose.connection
db.on('error', (error) => console.error(error))
db.once('open', () => console.log('Connected to Database'))
// new code ends here

app.listen(3000, () => console.log('Server Started'))
```
- Create environment variable for connection string
```
// .env
DATABASE_URL=mongodb://localhost/subscribers
```
- Replace connection string with environment variable
```js
// server.js
require('dotenv').config()

...
mongoose.connect(process.env.DATABASE_URL, { useNewUrlParser: true })
...
```
- Setup routes
```js
// server.js
...
db.once('open', () => console.log('Connected to Database'))

// new code starts here
app.use(express.json())

const subscribersRouter = require('./routes/subscribers')
// localhost:3000/subscribers
app.use('/subscribers', subscribersRouter)
// new code ends here

...
```
- Create `routes` folder
- Create `subscribers.js` file in `routes` folder
```js
// subscribers.js
const express = require('express')
const router = express.Router()

// Getting all
router.get('/', (req, res) => {
  res.send('Hello World')
})

// Getting one
router.get('/:id', (req, res) => {
  res.send(req.params.id)
})

// Creating one
router.post('/', (req, res) => {

})

// Updating one
router.patch('/:id', (req, res) => {

})

// Deleting one
router.delete('/:id', (req, res) => {

})

module.exports = router
```
- Install [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) extension in [VSCode](https://code.visualstudio.com/)
- Create `route.rest` file in `routes` folder
```js
// routes.rest
GET http://localhost:3000/subscribers

###

GET http://localhost:3000/subscribers/12
```
