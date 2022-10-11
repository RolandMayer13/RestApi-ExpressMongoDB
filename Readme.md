# Build A REST API With Node.js, Express, & MongoDB - Quick
https://www.youtube.com/watch?v=fgTGADljAeg

- Create project folder
- Navigate inside project folder
- Open terminal
```Terminal
npm init
```
- Install dependencies
  - [Mongoose](https://mongoosejs.com/) (elegant mongodb object modeling for node.js)
```Terminal
npm i express mongoose
```
- Install development dependencies
  - [dotenv](https://github.com/motdotla/dotenv#readme) (Dotenv is a zero-dependency module that loads environment variables from a .env file into process.env.)
  - [nodemon](https://nodemon.io/) (Nodemon is a utility that will monitor for any changes in your source and automatically restart your server.)
```Terminal
npm i --save-dev dotenv nodemon
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
const express = require('express')
const app = express()

app.listen(3000, () => console.log('Server Started'))
```
- Start server
```Terminal
npm run devStart
```
- Stop server
```Terminal
CTRL + C
```
