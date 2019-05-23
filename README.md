# My Project Consumer Web

The folder structure will look like this:
```
~/environment/myproject-consumer-web
├── build/
├── config/
├── index.html
├── node_modules
├── package-lock.json
├── package.json
├── src
    ├── App.vue
    ├── assets/
        └── logo.png
    ├── components/
    ├── main.js
    └── router/
        └── index.js    
├── static
├── test
├── README.md
└── .gitignore
```

## Prerequsites
- Git
```
$ git --version
$ git config --global user.name "REPLACE_ME_WITH_YOUR_NAME"
$ git config --global user.email REPLACE_ME_WITH_YOUR_EMAIL@example.com
$ git config --global credential.helper '!aws codecommit credential-helper $@'
$ git config --global credential.UseHttpPath true
```

- npm
```
$ npm -v
6.7.0
```

- vue-cli
```
$ npm install -global vue-cli eslint
$ vue --version 
2.9.6
```

## Step 1: Create Frontend using VueJS, HTML, CSS and Bootstrap 4 
- Provides basic CRUD functionality for products
- The Service will be triggered by consumers via a web app
```
| WEBPAGE      | URI                                     | ACTION                      |
|--------------|-----------------------------------------|-----------------------------|
| HOME         | http://[hostname]/index                 | Landing Page                |
| INDEX        | http://[hostname]/products              | Gets all products           |
| DETAIL       | http://[hostname]/products/<product_id> | Gets one product            |
| SIGNIN       | http://[hostname]/login                 | Logs the user in            |
| SIGNUP       | http://[hostname]/signup                | Signs up the user           |
| BOOK-1       | http://[hostname]/user-booking-1.html   | Booking Step 1              |
| BOOK-2       | http://[hostname]/user-booking-2.html   | Booking Step 2              |
| PAYMENT      | http://[hostname]/payment.html          | Payment                     |
| CONFIRMATION | http://[hostname]/confirmation.html     | Confirmation                |
```

### Step 1.1: Initialize Vue Project
```
$ cd ~/environment/
$ vue init webpack myproject-consumer-web
$ cd myproject-consumer-web
$ npm run dev
```

### Step 1.2: Create a CodeCommit Repository
```bash
$ aws codecommit create-repository --repository-name myproject-consumer-web
```

### Step 1.3: Set up .gitignore
- Automatically created by vue init

### Step 1.4: Import Existing Project Folder to CodeCommit Repo
```bash
$ cd ~/environment/myproject-consumer-web
$ git init
$ git add .
$ git commit -m "Initial Commit"
$ git remote add origin https://git-codecommit.us-east-1.amazonaws.com/v1/repos/myproject-consumer-web
$ git remote -v
$ git push origin master
```

### Step 1.5: Test Vue Application Locally
```
$ cd ~/environment/myproject-consumer-web
$ npm run dev
```

### Step 1.6: Add Bootstrap 4
```bash
$ npm install bootstrap jquery popper.js webpack-cli --save 
$ npm install sass-loader node-sass webpack --save-dev
```

- in ~/environment/myproject-consumer-web/package.json you must see the ff dependencies:
```json
  "dependencies": {
    "bootstrap": "^4.3.1",
    "jquery": "^3.4.1",
    "popper.js": "^1.15.0"
  },
```

### Step 1.7: Require bootstrap in main.js

In `myproject-consumer-web/src/main.js`

Add the following line 
```js

import Vue from 'vue'
import App from './App'
import router from './router'

-------------------------------------------------------------
//Add this below
import 'bootstrap'
-------------------------------------------------------------
....
```

### Step 2.2: Require bootstrap in css files

In `myproject-consumer-web/assets/`
create file: `app.scss`

```scss
@import '~/bootstrap/scss/bootstrap'
```

We need to require `app.scss` in  `main.js` for it to be able to render the bootstrap css files. 

In `myproject-vuejs-web/src/main.js`
Add the following line 
```js
import Vue from 'vue'
import App from './App'
import router from './router'

import 'bootstrap'

-------------------------------------------------------------
// Add this below
import './assets/app.scss'
-------------------------------------------------------------

//more code below
....

```

### Step 2.3: Require require jQuery and popper.js

In `myproject-consumer-web/src/main.js`
Add the following line:
```js
import Vue from 'vue'
import App from './App'
import router from './router'
import 'bootstrap'
import './assets/app.scss'

-------------------------------------------------------------
// Add this below
// Assign `$` to the jQuery variable in the window element
import jQuery from 'jquery'
window.$ = window.jQuery = jQuery
import 'popper.js'
-------------------------------------------------------------
....

```

Final Version of `main.js`:

```js
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router'
import 'bootstrap'
import './assets/app.scss'

// Assign `$` to the jQuery variable in the window element
import jQuery from 'jquery'
window.$ = window.jQuery = jQuery
import 'popper.js'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```

## Step 3: Setup Basic U/I

### Step 3.1 Add a basic Bootstrap Navbar
In `myproject-consumer-web/src/`
replace code in `App.vue` with the following snippet:

Adding this code snippet will allow the navbar to be displayed in multiple views without needed to copy and paste code repetitively.

```html
<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              Dropdown
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="#">Action</a>
              <a class="dropdown-item" href="#">Another action</a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>
    <div class="container">
      <img src="./assets/logo.png">
      <router-view/>      
    </div>

  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  text-align: center;

}
</style>

```

### Step 3.1: Modify Router
In `myproject-consumer-web/src/router`
replace code in  `index.js` with the following snippet:

```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from '@/components/home'

Vue.use(Router)

let router = new Router({
  routes: [
    {
      path: '/',
      name: 'Home',
      component: Home
    }
  ]
})

export default router
```

### Step 3.2:  Setup a Basic Home Page
In `myproject-consumer-web/src/components`
add file: `home.vue`

```html
<template>
  <div>
    <h1>Home</h1>
    <div>
      <router-link to="/#"></router-link>
    </div>
  </div>
</template>
```


### Step 3.3: Test home page

In your browser, go to:  
```
http://localhost:8080
```
You should see the ff:
![](home.png)


## Step 4: Set up Axios to Consume Data

### Step 4.1: Install Axios
In the terminal run, inside your project folder, the following command: 
```bash
$ npm install axios --save
```

in `myproject-consumer-web/package.json` you must see the following dependencies:
```json
  "dependencies": {
    "bootstrap": "^4.3.1",
    "jquery": "^3.4.1",
    "popper.js": "^1.15.0",
    "axios": "^0.18.0"
  },
```

### Step 4.2: Modify Home Page to Include Axios

In `myproject-consumer-web/src/App.vue` remove the following line:

App.vue
```html
<img src="./assets/logo.png">
```

In `myproject-consumer-web/src/main.js`
Add the following lines:

```js
import axios from 'axios'
Vue.prototype.$http = axios;
```

### (Optional) Clean up
```
$ aws codecommit delete-repository --repository-name myproject-consumer-web
$ rm -rf ~/environment/myproject-consumer-web
```
