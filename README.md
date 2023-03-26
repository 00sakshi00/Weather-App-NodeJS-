# WeatherApp NodeJS

* Create an empty directory named weather-app.
* Open up your console, navigate to our new directory and run npm init.
* Fill out the required information to initialize our project.
* Within our weather-app directory, create a file named index.js — this file will house the code for our application.
* npm install --save express
* install in index.js

* Run: node index.js
* Now open your browser and visit: http://localhost:3000
* Install template system: npm install ejs --save
* Edit index.js: app.set('view engine', 'ejs')
* Create directory/file: views\index.ejs
* Edit into index.ejs file basic boilerplate for front end:

* In index.js, connect the template by replaceing Hello World line res.render('index');
* Run again: node index.js
* Set up POST route:

* install Middleware: npm install body-parser --save
* Edit index.js to add middleware:

* In index.js - log city to the console (add to existing post):

* Test it (to make sure city shows in console): node index.js
* http://localhost:3000/
* Setting up our URL - Include at top of index.js:

* Setting up our URL - In index.js POST section add:

* Make our API call (inside POST request)

* Display the weather

* Install request module npm install request --save
* Update ejs template code to reflect the what we get back from the api

* add more text:
