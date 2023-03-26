# WeatherApp NodeJS

* Create an empty directory named weather-app.
* Open up your console, navigate to our new directory and run npm init.
* Fill out the required information to initialize our project.
* Within our weather-app directory, create a file named index.js — this file will house the code for our application.
* npm install --save express
* install in index.js

```
const express = require('express')
const app = express()

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(3000, function () {
  console.log('Example app listening on port 3000!')
})
```

* Run: node index.js
* Now open your browser and visit: http://localhost:3000
* Install template system: npm install ejs --save
* Edit index.js: app.set('view engine', 'ejs')
* Create directory/file: views\index.ejs
* Edit into index.ejs file basic boilerplate for front end:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Test</title>
    <link rel="stylesheet" type="text/css" href="/css/style.css">
    <link href='https://fonts.googleapis.com/css?family=Open+Sans:300' rel='stylesheet' type='text/css'>
  </head>
  <body>
    <div class="container">
      <fieldset>
        <form action="/" method="post">
          <input name="city" type="text" class="ghost-input" placeholder="Enter a City" required>
          <input type="submit" class="ghost-button" value="Get Weather">
        </form>
      </fieldset>
    </div>
  </body>
</html>
```

* In index.js, connect the template by replaceing Hello World line res.render('index');
* Run again: node index.js
* Set up POST route:

```
app.post('/', function (req, res) {
  res.render('index');
})
```

* install Middleware: npm install body-parser --save
* Edit index.js to add middleware:

```
const bodyParser = require('body-parser');
// ...
app.use(bodyParser.urlencoded({ extended: true }));
```

* In index.js - log city to the console (add to existing post):

```
app.post('/', function (req, res) {
  res.render('index');
  console.log(req.body.city);
})
```

* Test it (to make sure city shows in console): node index.js
* http://localhost:3000/
* Setting up our URL - Include at top of index.js:

```
const request = require('request');
const apiKey = '*****************';
```

* Setting up our URL - In index.js POST section add:

```
let city = req.body.city;
let url = `http://api.openweathermap.org/data/2.5/weather?q=${city}&units=imperial&appid=${apiKey}`
```

* Make our API call (inside POST request)

```
request(url, function (err, response, body) {
    if(err){
      res.render('index', {weather: null, error: 'Error, please try again'});
```

* Display the weather

```
} else {
  let weather = JSON.parse(body)
  if(weather.main == undefined){
    res.render('index', {weather: null, error: 'Error, please try again'});
  } else {
    let weatherText = `It's ${weather.main.temp} degrees in ${weather.name}!`;
    res.render('index', {weather: weatherText, error: null});
  }
}
```

* Install request module npm install request --save
* Update ejs template code to reflect the what we get back from the api

```
<% if(weather !== null){ %>
  <p><%= weather %></p>
<% } %>
<% if(error !== null){ %>
  <p><%= error %></p>
<% } %>
```

* add more text:
```
let weatherTextExpanded = `It's ${weather.main.temp} degrees, with
  ${weather.main.humidity}% humidity in ${weather.name}!`;
```
