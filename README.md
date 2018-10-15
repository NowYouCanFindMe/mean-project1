
# Project 1
 ## Appendix
 **app.set**
 ```
  app.set('views', __dirname + '/views')
  app.set('view engine', 'jade')
```
We want express to use Jade and to find the files to render inside the `/views  ` folder.

**app.use()**
```
app.use(express.logger('dev'))
app.use(stylus.middleware(
  { src: __dirname + '/public'
  , compile: compile
  }
  ```
  This is a middleware function that have access to the request object(req), and the response object (res).
  
  **nodemon** - nodemon is a tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected.
## Steps
Let us first create a folder: 
```
cd ~/Documents
mkdir project1
cd project11
```
Or you can always right click, within a folder directory...

Next,
Create `package.json`

```javascript
{
  "name": "Project1",
  "version": "0.0.1",
  "private": "true",
  "dependencies": {
    "express": "^3.0.0-alpha4",
    "jade": "^1.0.4",
    "nib": "^1.0.4",
    "stylus": "^0.54.5"
  }
}

```

install dependencies: 
`npm install`

create `app.js`

Let us require the modules that we installed under dependencies in `package.json`

```
/*
 * Module dependencies
 */
var express = require('express')
  , stylus = require('stylus')
  , nib = require('nib')
```

Let us add some functionality to `app.js`

```javascript
var app = express()
function compile(str, path) {
  return stylus(str)
    .set('filename', path)
    .use(nib())
}
app.set('views', __dirname + '/views')
app.set('view engine', 'jade')
app.use(express.logger('dev'))
app.use(stylus.middleware(
  { src: __dirname + '/public'
  , compile: compile
  }
))
app.use(express.static(__dirname + '/public'))

app.get('/', function (req, res) {
  res.end('It is working!!!')
})
app.listen(3000)
```
## Halftime Break
Half Time Break

Let us see if everything is working
Open up a terminal window, cd into the folder you are working on 

Then type: `node app.js`

Confirm things are working by going to 

`http://localhost:3000/`
If you see the words: `‘It is working!!!’`, things are a-okay. 

Play around with `res.end('It is working!!!')`

And see if you can change the words
(Refresh the page to see changes)

But one second, if the page does not change we have to ***start node again***. 

Close the terminal window, or end the process by pressing `control+c`

Type `node app.js` again

This is kinda annoying. I will later so you an easier way for it to update by itself. 

## End of Half Time Break

Create a folder called `views`
Inside of the views folder, create a layout called `layout.jade`
Which will act as our template
```javascript
doctype
html
  head
    title #{title} - My Site
    link(rel='stylesheet', href='/stylesheets/style.css')
  body
    header
      h1 My Site
    .container
      .main-content
        block content
      .sidebar
        block sidebar
    footer
      p Running on node with Express, Jade and Stylus
```

Next we are going to create a file called `index.jade`, to fill in the layout we just created.
This will also be in the `views/`folder.

```javascript 
extend layout
block content
  p
    | Vivamus hendrerit arcu sed erat molestie
    | vehicula. Sed auctor neque eu tellus
    | rhoncus ut eleifend nibh porttitor. Ut in.
  p
    | Donec congue lacinia dui, a porttitor
    | lectus condimentum laoreet. Nunc eu
    | ullamcorper orci. Quisque eget odio ac
    | lectus vestibulum faucibus eget in metus.
    | In pellentesque faucibus vestibulum. Nulla
    | at nulla justo, eget luctus tortor.
block sidebar
  .widget
    h1 Widget
    p
      | Sed auctor neque eu tellus rhoncus ut
      | eleifend nibh porttitor. Ut in nulla enim.
    p
      | Vivamus hendrerit arcu sed erat molestie
      | vehicula.
```

## Let us add some styling
Create a folder called `public`
Within `public` create another folder called `stylesheets`
Next create an external stylesheet file, called `style.styl`
Within this file we will create css ids and classes to style contents in both layout and views files

Remember the `res.end('It is working!!!')`

Let us change that so it can render our changes we just made. 

Replace `app.get(‘/’,…)` to 
```javascript 
app.get('/', function (req, res) {
  res.render('index',
  { title : 'Home' }
  )
})
```
Now it is going to render the `index.jade` file that we created in the `views` folder

Only to see the changes. We have to **start node again…**

Input `node app.js` into a new terminal window.

But wait a second, there is an easier way. 

Let us install a tool call `

`
In a new terminal instance run
`npm install -g nodemon`

Once installed, let us run it again, but with nodemon

`nodemon app.js`


Feel free to customize the, index.jade file to make it your own. 






