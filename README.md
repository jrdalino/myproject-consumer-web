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
$ npm install -g @vue/cli
$ vue --version 
3.7.0
```

## Step 1: Create Frontend using VueJS, HTML, CSS and Bootstrap 4 
- Provides basic CRUD functionality for products
- The Service will be triggered by consumers via a web app
```
| WEBPAGE      | URI                                     | ACTION                      |
|--------------|-----------------------------------------|-----------------------------|
| HOME         | http://[hostname]/                      | Landing Page                |
| INDEX        | http://[hostname]/products              | Gets all products           |
| DETAIL       | http://[hostname]/products/<product_id> | Gets one product            |
| SIGNIN       | http://[hostname]/login                 | Logs the user in            |
| SIGNUP       | http://[hostname]/signup                | Signs up the user           |
| BOOK-1       | http://[hostname]/booking/step1         | Booking Step 1              |
| BOOK-2       | http://[hostname]/booking/step1         | Booking Step 2              |
| PAYMENT      | http://[hostname]/booking/payment       | Payment and Confirmation    |
| CONFIRMATION | http://[hostname]/booking/confirmed     | Confirmed                   |
```

### Step 1.1: Initialize Vue Project
```
$ cd ~/environment/
$ vue init webpack myproject-consumer-web
$ cd myproject-consumer-web
$ npm run serve
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
$ git remote add origin https://git-codecommit.ap-southeast-1.amazonaws.com/v1/repos/myproject-consumer-web
$ git remote -v
$ git push origin master
```

## Step 2: Setup Web Template (Bootstrap 4 - Directory Template)

### Step 2.1:  Install theme dependencies and node modules
Install dependencies:
In `myproject-consumer-web` add the following dependencies into `package.json`

```json
  "dependencies": {
    "bootstrap": "^4.3.1",
    "bootstrap-select": "^1.13.5",
    "jquery": "^3.3.1",
    "popper.js": "^1.15.0",
  },
```
Install module: vue-awesome-swiper
In the terminal run the following: 
```
$ npm install vue-awesome-swiper --save
```
after, run:
```
$ npm install
```

### Step 2.2: Import CSS and javascript dependencies to `main.js`

In `myproject-vuejs-web/src/main.js` add the following lines of code: 

```js
/* eslint-disable */

import VueAwesomeSwiper from 'vue-awesome-swiper'
import 'swiper/dist/css/swiper.css'
Vue.use(VueAwesomeSwiper)

// jQuery
require("@/assets/vendor/jquery/jquery.min.js")

// bootstrap
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';

// css
require('@/assets/vendor/nouislider/nouislider.css')
require('@/assets/vendor/magnific-popup/magnific-popup.css')
require('@/assets/css/style.default.css')
require('@/assets/css/custom.css')
require('@/assets/img/favicon.png')

// As a global method
require("@/assets/vendor/object-fit-images/ofi.min.js")
require("@/assets/vendor/bootstrap/js/bootstrap.bundle.min.js")
require("@/assets/vendor/magnific-popup/jquery.magnific-popup.min.js")
require("@/assets/vendor/smooth-scroll/smooth-scroll.polyfills.min.js")
require("@/assets/vendor/bootstrap-select/js/bootstrap-select.min.js")
```

Final Version of `main.js`:

```js
import Vue from 'vue'
import App from './App.vue'
import VueAwesomeSwiper from 'vue-awesome-swiper'
import 'swiper/dist/css/swiper.css'
Vue.use(VueAwesomeSwiper)

// jQuery
require("@/assets/vendor/jquery/jquery.min.js")

// bootstrap
import 'bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';

// css
require('@/assets/vendor/nouislider/nouislider.css')
require('@/assets/vendor/magnific-popup/magnific-popup.css')
require('@/assets/css/style.default.css')
require('@/assets/css/custom.css')
require('@/assets/img/favicon.png')

// As a global method
require("@/assets/vendor/object-fit-images/ofi.min.js")
require("@/assets/vendor/bootstrap/js/bootstrap.bundle.min.js")
require("@/assets/vendor/magnific-popup/jquery.magnific-popup.min.js")
require("@/assets/vendor/smooth-scroll/smooth-scroll.polyfills.min.js")
require("@/assets/vendor/bootstrap-select/js/bootstrap-select.min.js")

import router from './router'

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')

```

### Step 2.3: Import CSS dependencies to `App.vue`

Add the following stylesheet imports inside the `<style>` tag of `App.vue`
```css
 /*extra css*/
 @import "https://fonts.googleapis.com/css?family=Playfair+Display:400,400i,700";
 @import "https://fonts.googleapis.com/css?family=Poppins:300,400,400i,700";
 @import "https://cdnjs.cloudflare.com/ajax/libs/Swiper/4.4.1/css/swiper.min.css";
 @import "https://use.fontawesome.com/releases/v5.8.1/css/all.css";

```

Final version of `App.vue`:

```html
<template>
  <div id="app">
    <div class="navbar-margin"></div>
    <router-view/>
  </div>
</template>

<script type="text/javascript">
  // @ is an alias to /src
export default {
  name: 'home',
  components: {
  }
}

</script>
<style type="text/css">
  .navbar-margin {
    margin-bottom: 70px;
  }

  /*extra css*/
  @import "https://fonts.googleapis.com/css?family=Playfair+Display:400,400i,700";
  @import "https://fonts.googleapis.com/css?family=Poppins:300,400,400i,700";
  @import "https://use.fontawesome.com/releases/v5.8.1/css/all.css";

</style>

```

## Step 3: Set up Router Plugin

### Step 3.1: Add a router plugin
```bash
$ vue add router
```
Output:

```bash
? Use history mode for router? (Requires proper server setup for index fa
llback in production) Yes

🚀  Invoking generator for core:router...
📦  Installing additional dependencies...

added 1 package from 1 contributor and audited 24981 packages in 6.458s
found 0 vulnerabilities

✔  Successfully invoked generator for plugin: core:router
   The following files have been updated / added:

     .gitignore
     README.md
     babel.config.js
     package-lock.json
     package.json
     public/favicon.ico
     public/index.html
     src/App.vue
     src/assets/logo.png
     src/components/HelloWorld.vue
     src/main.js
     src/router.js
     src/views/About.vue
     src/views/Home.vue

   You should review these changes with git diff and commit them.

```
## Step 4: Set up Global Navbar and Footer

### Step 4.1: Set up Global Navigation Bar Component
In `myproject-consumer-web/src/components/`
create a file called : `Navigation.vue`

Add the following code in `Navigation.vue`:

```html
<template>
   <nav class="navbar navbar-expand-lg fixed-top shadow navbar-light bg-white">
      <div class="container-fluid">
        <div class="d-flex align-items-center"><a href="/" class="navbar-brand py-1"><img src="../assets/img/logo.svg" alt="Directory logo"></a>
          <form action="#" id="search" class="form-inline d-none d-sm-flex">
            <div class="input-label-absolute input-label-absolute-left input-reset input-expand ml-lg-2 ml-xl-3"> 
              <label for="search_search" class="label-absolute"><i class="fa fa-search"></i><span class="sr-only">What are you looking for?</span></label>
              <input id="search_search" placeholder="Search" aria-label="Search" class="form-control form-control-sm border-0 shadow-0 bg-gray-200">
              <button type="reset" class="btn btn-reset btn-sm"><i class="fa-times fas"></i></button>
            </div>
          </form>
        </div>
        <button type="button" data-toggle="collapse" data-target="#navbarCollapse" aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation" class="navbar-toggler navbar-toggler-right"><i class="fa fa-bars"></i></button>
        <!-- Navbar Collapse -->
        <div id="navbarCollapse" class="collapse navbar-collapse">
          <form action="#" id="searchcollapsed" class="form-inline mt-4 mb-2 d-sm-none">
            <div class="input-label-absolute input-label-absolute-left input-reset w-100">
              <label for="searchcollapsed_search" class="label-absolute"><i class="fa fa-search"></i><span class="sr-only">What are you looking for?</span></label>
              <input id="searchcollapsed_search" placeholder="Search" aria-label="Search" class="form-control form-control-sm border-0 shadow-0 bg-gray-200">
              <button type="reset" class="btn btn-reset btn-sm"><i class="fa-times fas">           </i></button>
            </div>
          </form>
          <ul class="navbar-nav ml-auto">
            <li class="nav-item dropdown"><a id="homeDropdownMenuLink" href="/" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" class="nav-link dropdown-toggle active">
                 
                Home</a>
              <div aria-labelledby="homeDropdownMenuLink" class="dropdown-menu"><a href="index.html" class="dropdown-item">Rooms</a><a href="index-2.html" class="dropdown-item">Restaurants</a></div>
            </li>
            <!-- Megamenu-->
            <li class="nav-item dropdown position-static"><a href="#" data-toggle="dropdown" class="nav-link dropdown-toggle">Template</a>
              <div class="dropdown-menu megamenu py-lg-0">
                <div class="row">
                  <div class="col-lg-9">
                    <div class="row p-3 pr-lg-0 pl-lg-5 pt-lg-5">
                      <div class="col-lg-3">
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase">Homepage</h6>
                        <ul class="megamenu-list list-unstyled">
                          <li class="megamenu-list-item"><a href="index.html" class="megamenu-list-link">Rooms   </a></li>
                          <li class="megamenu-list-item"><a href="index-2.html" class="megamenu-list-link">Restaurants   </a></li>
                        </ul>
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase">Restaurants</h6>
                        <ul class="megamenu-list list-unstyled">
                          <li class="megamenu-list-item"><a href="category.html" class="megamenu-list-link">Category - Map on the top   </a></li>
                          <li class="megamenu-list-item"><a href="category-2.html" class="megamenu-list-link">Category - Map on the right   </a></li>
                          <li class="megamenu-list-item"><a href="category-3.html" class="megamenu-list-link">Category - no map   </a></li>
                          <li class="megamenu-list-item"><a href="detail.html" class="megamenu-list-link">Restaurant detail   </a></li>
                        </ul>
                      </div>
                      <div class="col-lg-3">
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase">Rooms</h6>
                        <ul class="megamenu-list list-unstyled">
                          <li class="megamenu-list-item"><a href="category-rooms.html" class="megamenu-list-link">Category - Map on the top   </a></li>
                          <li class="megamenu-list-item"><a href="category-2-rooms.html" class="megamenu-list-link">Category - Map on the right   </a></li>
                          <li class="megamenu-list-item"><a href="category-3-rooms.html" class="megamenu-list-link">Category - no map   </a></li>
                          <li class="megamenu-list-item"><a href="detail-rooms.html" class="megamenu-list-link">Room detail   </a></li>
                        </ul>
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase">Blog</h6>
                        <ul class="megamenu-list list-unstyled">
                          <li class="megamenu-list-item"><a href="blog.html" class="megamenu-list-link">Blog   </a></li>
                          <li class="megamenu-list-item"><a href="post.html" class="megamenu-list-link">Post   </a></li>
                        </ul>
                      </div>
                      <div class="col-lg-3">
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase">Pages</h6>
                        <ul class="megamenu-list list-unstyled">
                          <li class="megamenu-list-item"><a href="contact.html" class="megamenu-list-link">Contact   </a></li>
                          <li class="megamenu-list-item"><a href="pricing.html" class="megamenu-list-link">Pricing   </a></li>
                          <li class="megamenu-list-item"><a href="text.html" class="megamenu-list-link">Text page   </a></li>
                          <li class="megamenu-list-item"><a href="faq.html" class="megamenu-list-link">F.A.Q.s  <span class="badge badge-info ml-1">New</span>   </a></li>
                          <li class="megamenu-list-item"><a href="coming-soon.html" class="megamenu-list-link">Coming soon   </a></li>
                        </ul>
                      </div>
                      <div class="col-lg-3">
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase">User</h6>
                        <ul class="megamenu-list list-unstyled">
                          <li class="megamenu-list-item"><a href="/login" class="megamenu-list-link">Sign in   </a></li>
                          <li class="megamenu-list-item"><a href="/signup" class="megamenu-list-link">Sign up   </a></li>
                          <li class="megamenu-list-item"><a href="user-booking-1.html" class="megamenu-list-link">Booking process - 4 pages <span class="badge badge-warning ml-1">New</span>   </a></li>
                          <li class="megamenu-list-item"><a href="user-grid.html" class="megamenu-list-link">Bookings &mdash; grid view <span class="badge badge-warning ml-1">New</span>   </a></li>
                          <li class="megamenu-list-item"><a href="user-booking-detail.html" class="megamenu-list-link">Booking detail <span class="badge badge-warning ml-1">New</span>   </a></li>
                        </ul>
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase">Host</h6>
                        <ul class="megamenu-list list-unstyled">
                          <li class="megamenu-list-item"><a href="user-add-0.html" class="megamenu-list-link">Add new listing - 6 pages   </a></li>
                          <li class="megamenu-list-item"><a href="user-list.html" class="megamenu-list-link">Bookings &mdash; list view <span class="badge badge-warning ml-1">New</span>   </a></li>
                        </ul>
                      </div>
                    </div>
                    <div class="row megamenu-services d-none d-lg-flex pl-lg-5">
                      <div class="col-xl-3 col-lg-6 d-flex">
                        <div class="megamenu-services-item">
                          <svg class="svg-icon megamenu-services-icon">
                            <use xlink:href="#destination-map-1"> </use>
                          </svg>
                          <div>
                            <h6 class="text-uppercase">Best rentals</h6>
                            <p class="mb-0 text-muted text-sm">Find the perfect place</p>
                          </div>
                        </div>
                      </div>
                      <div class="col-xl-3 col-lg-6 d-flex">
                        <div class="megamenu-services-item">
                          <svg class="svg-icon megamenu-services-icon">
                            <use xlink:href="#money-box-1"> </use>
                          </svg>
                          <div>
                            <h6 class="text-uppercase">Earn points</h6>
                            <p class="mb-0 text-muted text-sm">And get great rewards</p>
                          </div>
                        </div>
                      </div>
                      <div class="col-xl-3 col-lg-6 d-flex">
                        <div class="megamenu-services-item">
                          <svg class="svg-icon megamenu-services-icon">
                            <use xlink:href="#customer-support-1"> </use>
                          </svg>
                          <div>
                            <h6 class="text-uppercase">020-800-456-747</h6>
                            <p class="mb-0 text-muted text-sm">24/7 Available Support</p>
                          </div>
                        </div>
                      </div>
                      <div class="col-xl-3 col-lg-6 d-flex">
                        <div class="megamenu-services-item">
                          <svg class="svg-icon megamenu-services-icon">
                            <use xlink:href="#secure-payment-1"> </use>
                          </svg>
                          <div>
                            <h6 class="text-uppercase">Secure Payment</h6>
                            <p class="mb-0 text-muted text-sm">Secure Payment</p>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="col-lg-3 d-none d-lg-block"><img src="img/photo/photo-1521170665346-3f21e2291d8b.jpg" alt="" class="bg-image"></div>
                </div>
              </div>
            </li>
            <!-- /Megamenu end-->
            <li class="nav-item"><a href="contact.html" class="nav-link">Contact</a>
            </li>
            <li class="nav-item dropdown"><a id="docsDropdownMenuLink" href="index.html" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" class="nav-link dropdown-toggle ">
                 
                Docs</a>
              <div aria-labelledby="docsDropdownMenuLink" class="dropdown-menu dropdown-menu-right">
                <h6 class="dropdown-header font-weight-normal">Documentation</h6><a href="docs/docs-introduction.html" class="dropdown-item">Introduction </a><a href="docs/docs-directory-structure.html" class="dropdown-item">Directory structure </a><a href="docs/docs-gulp.html" class="dropdown-item">Gulp </a><a href="docs/docs-customizing-css.html" class="dropdown-item">Customizing CSS </a><a href="docs/docs-credits.html" class="dropdown-item">Credits </a><a href="docs/docs-changelog.html" class="dropdown-item">Changelog </a>
                <div class="dropdown-divider"></div>
                <h6 class="dropdown-header font-weight-normal">Components</h6><a href="docs/components-bootstrap.html" class="dropdown-item">Bootstrap </a><a href="docs/components-directory.html" class="dropdown-item">Theme </a>
              </div>
            </li>
            <li class="nav-item"><a href="/login" class="nav-link">Sign in</a></li>
            <li class="nav-item"><a href="/signup" class="nav-link">Sign up</a></li>
            <li class="nav-item mt-3 mt-lg-0 ml-lg-3 d-lg-none d-xl-inline-block"><a href="user-add-0.html" class="btn btn-primary">Add a listing</a></li>
          </ul>
        </div>
      </div>
    </nav>  
</template>
```

Add the following code into the `<template>` tag of `App.vue`
```html
...
<Navigation/>
<router-view/>
...
```

In the `<script>` tag of `App.vue` add the following code: 

```js
import Navigation from '@/components/Navigation.vue' <--- We import the footer from our components

export default {
  name: 'home',
  components: {
    Navigation <--- We add footer as a component
  }
}
```

Add the following under `<Navigation>` tag in  `App.vue`
```html
<div class="navbar-margin"></div>
```
Add the following code inside the `<style>` tag of `App.vue`
```css
 .navbar-margin {
     margin-bottom: 70px;
 }
```

### Step 4.2 : Set up Global Footer Component
In `myproject-consumer-web/src/components/`
create a file called : `Footer.vue`

Add the following code in `Footer.vue`:
```html
<template>
   <footer class="position-relative z-index-10 d-print-none">
      <!-- Main block - menus, subscribe form-->
      <div class="py-6 bg-gray-200 text-muted"> 
        <div class="container">
          <div class="row">
            <div class="col-lg-4 mb-5 mb-lg-0">
              <div class="font-weight-bold text-uppercase text-dark mb-3">Directory</div>
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing.</p>
              <ul class="list-inline">
                <li class="list-inline-item"><a href="#" target="_blank" title="twitter" class="text-muted text-hover-primary"><i class="fab fa-twitter"></i></a></li>
                <li class="list-inline-item"><a href="#" target="_blank" title="facebook" class="text-muted text-hover-primary"><i class="fab fa-facebook"></i></a></li>
                <li class="list-inline-item"><a href="#" target="_blank" title="instagram" class="text-muted text-hover-primary"><i class="fab fa-instagram"></i></a></li>
                <li class="list-inline-item"><a href="#" target="_blank" title="pinterest" class="text-muted text-hover-primary"><i class="fab fa-pinterest"></i></a></li>
                <li class="list-inline-item"><a href="#" target="_blank" title="vimeo" class="text-muted text-hover-primary"><i class="fab fa-vimeo"></i></a></li>
              </ul>
            </div>
            <div class="col-lg-2 col-md-6 mb-5 mb-lg-0">
              <h6 class="text-uppercase text-dark mb-3">Rentals</h6>
              <ul class="list-unstyled">
                <li><a href="index.html" class="text-muted">Rooms     </a></li>
                <li><a href="category-rooms.html" class="text-muted">Map on top     </a></li>
                <li><a href="category-2-rooms.html" class="text-muted">Side map     </a></li>
                <li><a href="category-3-rooms.html" class="text-muted">No map     </a></li>
                <li><a href="detail-rooms.html" class="text-muted">Room detail     </a></li>
              </ul>
            </div>
            <div class="col-lg-2 col-md-6 mb-5 mb-lg-0">
              <h6 class="text-uppercase text-dark mb-3">Pages</h6>
              <ul class="list-unstyled">
                <li><a href="contact.html" class="text-muted">Contact                                   </a></li>
                <li><a href="pricing.html" class="text-muted">Pricing                                   </a></li>
                <li><a href="text.html" class="text-muted">Text page                                   </a></li>
                <li><a href="faq.html" class="text-muted">F.A.Q.s  <span class="badge badge-info ml-1">New</span>                                   </a></li>
                <li><a href="coming-soon.html" class="text-muted">Coming soon                                   </a></li>
              </ul>
            </div>
            <div class="col-lg-4">
              <h6 class="text-uppercase text-dark mb-3">Daily Offers & Discounts</h6>
              <p class="mb-3"> Lorem ipsum dolor sit amet, consectetur adipisicing elit. At itaque temporibus.</p>
              <form action="#" id="newsletter-form">
                <div class="input-group mb-3">
                  <input type="email" placeholder="Your Email Address" aria-label="Your Email Address" class="form-control bg-transparent border-dark border-right-0">
                  <div class="input-group-append">
                    <button type="submit" class="btn btn-outline-dark border-left-0"> <i class="fa fa-paper-plane text-lg"></i></button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
      <!-- Copyright section of the footer-->
      <div class="py-4 font-weight-light bg-gray-800 text-gray-300">
        <div class="container">
          <div class="row align-items-center">
            <div class="col-md-6 text-center text-md-left">
              <p class="text-sm mb-md-0">&copy; 2019 Your company.  All rights reserved.</p>
            </div>
            <div class="col-md-6">
              <ul class="list-inline mb-0 mt-2 mt-md-0 text-center text-md-right">
                <li class="list-inline-item"><img src="../assets/img/visa.svg" alt="..." class="w-2rem"></li>
                <li class="list-inline-item"><img src="../assets/img/mastercard.svg" alt="..." class="w-2rem"></li>
                <li class="list-inline-item"><img src="../assets/img/paypal.svg" alt="..." class="w-2rem"></li>
                <li class="list-inline-item"><img src="../assets/img/western-union.svg" alt="..." class="w-2rem"></li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </footer>
</template>
```

Add the following code into the `<template>` tag of `App.vue`
```html
...
<router-view/>
<Footer/>
...
```
In the `<script>` tag of `App.vue` add the following code: 

```js
import Footer from '@/components/Footer.vue' <--- We import the footer from our components

export default {
  name: 'home',
  components: {
    Navigation,
    Footer <--- We add footer as a component
  }
}
```

Final Version of `App.vue`
```html
<template>
  <div id="app">
    <Navigation/>
    <div class="navbar-margin"></div>
    <router-view/>
    <Footer/>

  </div>
</template>

<script type="text/javascript">
  // @ is an alias to /src
import Navigation from '@/components/Navigation.vue'
import Footer from '@/components/Footer.vue'

export default {
  name: 'home',
  components: {
    Navigation,
    Footer
  }
}
</script>
<style type="text/css">
  .navbar-margin {
    margin-bottom: 50px;
  }

  /*extra css*/
  @import "https://fonts.googleapis.com/css?family=Playfair+Display:400,400i,700";
  @import "https://fonts.googleapis.com/css?family=Poppins:300,400,400i,700";
  @import "https://use.fontawesome.com/releases/v5.8.1/css/all.css";
</style>
```

## Step 5: Set up Home Page

### Step 5.1: Set up Search Bar Component
In `myproject-consumer-web/src/components/`
create a file called : `SearchBar.vue`
Add the following code:
```html
<template>
  <div class="searchbar">
    <section class="hero-home">
      <swiper :options="swiperOption" class="hero-slider">
        <div class="swiper-wrapper dark-overlay">
          <swiper-slide class="swiper-slide pic_1"></swiper-slide>
          <swiper-slide class="swiper-slide pic_2"></swiper-slide>
          <swiper-slide class="swiper-slide pic_3"></swiper-slide>
          <swiper-slide class="swiper-slide pic_4"></swiper-slide>
        </div>
      </swiper>
      <div class="container py-6 py-md-7 text-white z-index-20">
        <div class="row">
          <div class="col-xl-10">
            <div class="text-center text-lg-left">
              <p class="subtitle letter-spacing-4 mb-2 text-secondary text-shadow">The best holiday experience</p>
              <h1 class="display-3 font-weight-bold text-shadow">Stay like a local</h1>
            </div>
            <div class="search-bar mt-5 p-3 p-lg-1 pl-lg-4">
              <form action="#">
                <div class="row">
                  <div class="col-lg-4 d-flex align-items-center form-group">
                    <input type="text" name="search" placeholder="What are you searching for?" class="form-control border-0 shadow-0">
                  </div>
                  <div class="col-lg-3 d-flex align-items-center form-group">
                    <div class="input-label-absolute input-label-absolute-right w-100">
                      <label for="location" class="label-absolute"><i class="fa fa-crosshairs"></i><span class="sr-only">City</span></label>
                      <input type="text" name="location" placeholder="Location" id="location" class="form-control border-0 shadow-0">
                    </div>
                  </div>
                  <div class="col-lg-3 d-flex align-items-center form-group no-divider">
                    <select title="Categories" data-style="btn-form-control" class="selectpicker">
                      <option value="small">Restaurants</option>
                      <option value="medium">Hotels</option>
                      <option value="large">Cafes</option>
                      <option value="x-large">Garages</option>
                    </select>
                  </div>
                  <div class="col-lg-2">
                    <button type="submit" class="btn btn-primary btn-block rounded-xl h-100">Search </button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .pic_1 {
    background: url('../assets/img/photo/photo-1501621965065-c6e1cf6b53e2.jpg') center;
    background-size: cover
  }
  .pic_2 {
    background: url('../assets/img/photo/photo-1519974719765-e6559eac2575.jpg') center;
    background-size: cover
  }
  .pic_3 {
    background: url('../assets/img/photo/photo-1490578474895-699cd4e2cf59.jpg') center;
    background-size: cover
  }
  .pic_4 {
    background: url('../assets/img/photo/photo-1534850336045-c6c6d287f89e.jpg') center;
    background-size: cover
  }

</style>


<script>
  export default {
    data() {
      return {
        swiperOption: {
          el: '.hero-slider',
          effect: 'fade',
          speed: 2000,
          allowTouchMove: false,
          autoplay: {
              delay: 2000,
          },
        }
      }
    }
  }
</script>
```
### Step 5.2: Set up AboutProduct Component
In `myproject-consumer-web/src/components/`
create a file called : `AboutProduct.vue`
Add the following code:
```html
<template>
    <div class="about-product">
     <section class="py-6 bg-gray-100">
      <div class="container">
        <div class="text-center pb-lg-4">
          <p class="subtitle text-secondary">One-of-a-kind vacation rentals </p>
          <h2 class="mb-5">Booking with us is easy</h2>
        </div>
        <div class="row">
          <div class="col-lg-4 mb-3 mb-lg-0 text-center">
            <div class="px-0 px-lg-3">
              <div class="icon-rounded bg-primary-light mb-3">
                <svg class="svg-icon text-primary w-2rem h-2rem">
                  <use xlink:href="#destination-map-1"> </use>
                </svg>
              </div>
              <h3 class="h5">Find the perfect rental</h3>
              <p class="text-muted">One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed in his bed in</p>
            </div>
          </div>
          <div class="col-lg-4 mb-3 mb-lg-0 text-center">
            <div class="px-0 px-lg-3">
              <div class="icon-rounded bg-primary-light mb-3">
                <svg class="svg-icon text-primary w-2rem h-2rem">
                  <use xlink:href="#pay-by-card-1"> </use>
                </svg>
              </div>
              <h3 class="h5">Book with confidence</h3>
              <p class="text-muted">The bedding was hardly able to cover it and seemed ready to slide off any moment. His many legs, pit</p>
            </div>
          </div>
          <div class="col-lg-4 mb-3 mb-lg-0 text-center">
            <div class="px-0 px-lg-3">
              <div class="icon-rounded bg-primary-light mb-3">
                <svg class="svg-icon text-primary w-2rem h-2rem">
                  <use xlink:href="#heart-1"> </use>
                </svg>
              </div>
              <h3 class="h5">Enjoy your vacation</h3>
              <p class="text-muted">His room, a proper human room although a little too small, lay peacefully between its four familiar </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
```

### Step 5.3: Set up DisplayCatalog1 Component
In `myproject-consumer-web/src/components/`
create a file called : `DisplayCatalog1.vue`
Add the following code:
```html
<template>
  <div class="display-catalog-1">
    <section class="py-6 bg-white">
      <div class="container">
        <div class="row mb-5">
          <div class="col-md-8">
            <p class="subtitle text-primary">Stay and eat like a local</p>
            <h2>Our guides</h2>
          </div>
          <div class="col-md-4 d-lg-flex align-items-center justify-content-end"><a href="category.html" class="text-muted text-sm">
               
              See all guides<i class="fas fa-angle-double-right ml-2"></i></a></div>
        </div>
        <div class="row">
          <swiper :options="swiperOption" class="guides-slider">
              <swiper-slide class="h-auto px-2">
                <div class="card card-poster gradient-overlay mb-4 mb-lg-0"><a href="category.html" class="tile-link"></a><img src="../assets/img/photo/new-york.jpg" alt="Card image" class="bg-image">
                  <div class="card-body overlay-content">
                    <h6 class="card-title text-shadow text-uppercase">New York</h6>
                    <p class="card-text text-sm">The big apple</p>
                  </div>
                </div>
              </swiper-slide>
              <swiper-slide class="h-auto px-2">
                <div class="card card-poster gradient-overlay mb-4 mb-lg-0"><a href="category.html" class="tile-link"></a><img src="../assets/img/photo/paris.jpg" alt="Card image" class="bg-image">
                  <div class="card-body overlay-content">
                    <h6 class="card-title text-shadow text-uppercase">Paris</h6>
                    <p class="card-text text-sm">Artist capital of Europe</p>
                  </div>
                </div>
              </swiper-slide>
              <swiper-slide class="h-auto px-2">
                <div class="card card-poster gradient-overlay mb-4 mb-lg-0"><a href="category.html" class="tile-link"></a><img src="../assets/img/photo/barcelona.jpg" alt="Card image" class="bg-image">
                  <div class="card-body overlay-content">
                    <h6 class="card-title text-shadow text-uppercase">Barcelona</h6>
                    <p class="card-text text-sm">Dalí, Gaudí, Barrio Gotico</p>
                  </div>
                </div>
              </swiper-slide >
              <swiper-slide class="h-auto px-2">
                <div class="card card-poster gradient-overlay mb-4 mb-lg-0"><a href="category.html" class="tile-link"></a><img src="../assets/img/photo/prague.jpg" alt="Card image" class="bg-image">
                  <div class="card-body overlay-content">
                    <h6 class="card-title text-shadow text-uppercase">Prague</h6>
                    <p class="card-text text-sm">City of hundred towers</p>
                  </div>
                </div>
              </swiper-slide >
          </swiper>
        </div>
      </div>
    </section>
  </div>
</template>

<script scoped>
  export default {
    data() {
      return {
        swiperOption: {
          slidesPerView: 7,
          spaceBetween: 20,
          loop: true
        }
      }
    }
  }
</script>
```

### Step 5.4: Set up DisplayCatalog2 Component
In `myproject-consumer-web/src/components/`
create a file called : `DisplayCatalog2.vue`
Add the following code:
```html
<template>
  <div class="display-catalog-2">
  <section class="py-6 bg-gray-100"> 
      <div class="container">
        <div class="row mb-5">
          <div class="col-md-8">
            <p class="subtitle text-secondary">Hurry up, these are expiring soon.        </p>
            <h2>Last minute deals</h2>
          </div>
          <div class="col-md-4 d-lg-flex align-items-center justify-content-end"><a href="category.html" class="text-muted text-sm">
               
              See all deals<i class="fas fa-angle-double-right ml-2"></i></a></div>
        </div>
        <!-- Slider main container-->
        <swiper :options="swiperOption">
            <!-- Slides-->
            <swiper-slide class="h-auto px-2">
              <!-- place item-->
              <div data-marker-id="59c0c8e33b1527bfe2abaf92" class="w-100 h-100">
                <div class="card h-100 border-0 shadow">
                  <div class="card-img-top overflow-hidden gradient-overlay"> <img src="../assets/img/photo/photo-1484154218962-a197022b5858.jpg" alt="Modern, Well-Appointed Room" class="img-fluid"/><a href="detail-rooms.html" class="tile-link"></a>
                    <div class="card-img-overlay-bottom z-index-20">
                      <div class="media text-white text-sm align-items-center"><img src="../assets/img/avatar/avatar-0.jpg" alt="Pamela" class="avatar avatar-border-white mr-2"/>
                        <div class="media-body">Pamela</div>
                      </div>
                    </div>
                    <div class="card-img-overlay-top text-right"><a href="javascript: void();" class="card-fav-icon position-relative z-index-40"> 
                        <svg class="svg-icon text-white">
                          <use xlink:href="#heart-1"> </use>
                        </svg></a></div>
                  </div>
                  <div class="card-body d-flex align-items-center">
                    <div class="w-100">
                      <h6 class="card-title"><a href="detail-rooms.html" class="text-decoration-none text-dark">Modern, Well-Appointed Room</a></h6>
                      <div class="d-flex card-subtitle mb-3">
                        <p class="flex-grow-1 mb-0 text-muted text-sm">Private room</p>
                        <p class="flex-shrink-1 mb-0 card-stars text-xs text-right"><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i>
                        </p>
                      </div>
                      <p class="card-text text-muted"><span class="h4 text-primary">$80</span> per night</p>
                    </div>
                  </div>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="h-auto px-2">
              <!-- place item-->
              <div data-marker-id="59c0c8e322f3375db4d89128" class="w-100 h-100">
                <div class="card h-100 border-0 shadow">
                  <div class="card-img-top overflow-hidden gradient-overlay"> <img src="../assets/img/photo/photo-1426122402199-be02db90eb90.jpg" alt="Cute Quirky Garden apt, NYC adjacent" class="img-fluid"/><a href="detail-rooms.html" class="tile-link"></a>
                    <div class="card-img-overlay-bottom z-index-20">
                      <div class="media text-white text-sm align-items-center"><img src="../assets/img/avatar/avatar-7.jpg" alt="John" class="avatar avatar-border-white mr-2"/>
                        <div class="media-body">John</div>
                      </div>
                    </div>
                    <div class="card-img-overlay-top text-right"><a href="javascript: void();" class="card-fav-icon position-relative z-index-40"> 
                        <svg class="svg-icon text-white">
                          <use xlink:href="#heart-1"> </use>
                        </svg></a></div>
                  </div>
                  <div class="card-body d-flex align-items-center">
                    <div class="w-100">
                      <h6 class="card-title"><a href="detail-rooms.html" class="text-decoration-none text-dark">Cute Quirky Garden apt, NYC adjacent</a></h6>
                      <div class="d-flex card-subtitle mb-3">
                        <p class="flex-grow-1 mb-0 text-muted text-sm">Entire apartment</p>
                        <p class="flex-shrink-1 mb-0 card-stars text-xs text-right"><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-gray-300">                                  </i>
                        </p>
                      </div>
                      <p class="card-text text-muted"><span class="h4 text-primary">$121</span> per night</p>
                    </div>
                  </div>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="h-auto px-2">
              <!-- place item-->
              <div data-marker-id="59c0c8e3a31e62979bf147c9" class="w-100 h-100">
                <div class="card h-100 border-0 shadow">
                  <div class="card-img-top overflow-hidden gradient-overlay"> <img src="../assets/img/photo/photo-1512917774080-9991f1c4c750.jpg" alt="Modern Apt - Vibrant Neighborhood!" class="img-fluid"/><a href="detail-rooms.html" class="tile-link"></a>
                    <div class="card-img-overlay-bottom z-index-20">
                      <div class="media text-white text-sm align-items-center"><img src="../assets/img/avatar/avatar-8.jpg" alt="Julie" class="avatar avatar-border-white mr-2"/>
                        <div class="media-body">Julie</div>
                      </div>
                    </div>
                    <div class="card-img-overlay-top text-right"><a href="javascript: void();" class="card-fav-icon position-relative z-index-40"> 
                        <svg class="svg-icon text-white">
                          <use xlink:href="#heart-1"> </use>
                        </svg></a></div>
                  </div>
                  <div class="card-body d-flex align-items-center">
                    <div class="w-100">
                      <h6 class="card-title"><a href="detail-rooms.html" class="text-decoration-none text-dark">Modern Apt - Vibrant Neighborhood!</a></h6>
                      <div class="d-flex card-subtitle mb-3">
                        <p class="flex-grow-1 mb-0 text-muted text-sm">Entire apartment</p>
                        <p class="flex-shrink-1 mb-0 card-stars text-xs text-right"><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-gray-300">                                  </i><i class="fa fa-star text-gray-300">                                  </i>
                        </p>
                      </div>
                      <p class="card-text text-muted"><span class="h4 text-primary">$75</span> per night</p>
                    </div>
                  </div>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="h-auto px-2">
              <!-- place item-->
              <div data-marker-id="59c0c8e3503eb77d487e8082" class="w-100 h-100">
                <div class="card h-100 border-0 shadow">
                  <div class="card-img-top overflow-hidden gradient-overlay"> <img src="../assets/img/photo/photo-1494526585095-c41746248156.jpg" alt="Sunny Private Studio-Apartment" class="img-fluid"/><a href="detail-rooms.html" class="tile-link"></a>
                    <div class="card-img-overlay-bottom z-index-20">
                      <div class="media text-white text-sm align-items-center"><img src="../assets/img/avatar/avatar-9.jpg" alt="Barbora" class="avatar avatar-border-white mr-2"/>
                        <div class="media-body">Barbora</div>
                      </div>
                    </div>
                    <div class="card-img-overlay-top text-right"><a href="javascript: void();" class="card-fav-icon position-relative z-index-40"> 
                        <svg class="svg-icon text-white">
                          <use xlink:href="#heart-1"> </use>
                        </svg></a></div>
                  </div>
                  <div class="card-body d-flex align-items-center">
                    <div class="w-100">
                      <h6 class="card-title"><a href="detail-rooms.html" class="text-decoration-none text-dark">Sunny Private Studio-Apartment</a></h6>
                      <div class="d-flex card-subtitle mb-3">
                        <p class="flex-grow-1 mb-0 text-muted text-sm">Shared room</p>
                        <p class="flex-shrink-1 mb-0 card-stars text-xs text-right"><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-gray-300">                                  </i>
                        </p>
                      </div>
                      <p class="card-text text-muted"><span class="h4 text-primary">$93</span> per night</p>
                    </div>
                  </div>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="h-auto px-2">
              <!-- place item-->
              <div data-marker-id="59c0c8e39aa2eed0626e485d" class="w-100 h-100">
                <div class="card h-100 border-0 shadow">
                  <div class="card-img-top overflow-hidden gradient-overlay"> <img src="../assets/img/photo/photo-1522771739844-6a9f6d5f14af.jpg" alt="Mid-Century Modern Garden Paradise" class="img-fluid"/><a href="detail-rooms.html" class="tile-link"></a>
                    <div class="card-img-overlay-bottom z-index-20">
                      <div class="media text-white text-sm align-items-center"><img src="../assets/img/avatar/avatar-10.jpg" alt="Jack" class="avatar avatar-border-white mr-2"/>
                        <div class="media-body">Jack</div>
                      </div>
                    </div>
                    <div class="card-img-overlay-top text-right"><a href="javascript: void();" class="card-fav-icon position-relative z-index-40"> 
                        <svg class="svg-icon text-white">
                          <use xlink:href="#heart-1"> </use>
                        </svg></a></div>
                  </div>
                  <div class="card-body d-flex align-items-center">
                    <div class="w-100">
                      <h6 class="card-title"><a href="detail-rooms.html" class="text-decoration-none text-dark">Mid-Century Modern Garden Paradise</a></h6>
                      <div class="d-flex card-subtitle mb-3">
                        <p class="flex-grow-1 mb-0 text-muted text-sm">Entire house</p>
                        <p class="flex-shrink-1 mb-0 card-stars text-xs text-right"><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i>
                        </p>
                      </div>
                      <p class="card-text text-muted"><span class="h4 text-primary">$115</span> per night</p>
                    </div>
                  </div>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="h-auto px-2">
              <!-- place item-->
              <div data-marker-id="59c0c8e39aa2edasd626e485d" class="w-100 h-100">
                <div class="card h-100 border-0 shadow">
                  <div class="card-img-top overflow-hidden gradient-overlay"> <img src="../assets/img/photo/photo-1488805990569-3c9e1d76d51c.jpg" alt="Brooklyn Life, Easy to Manhattan" class="img-fluid"/><a href="detail-rooms.html" class="tile-link"></a>
                    <div class="card-img-overlay-bottom z-index-20">
                      <div class="media text-white text-sm align-items-center"><img src="../assets/img/avatar/avatar-11.jpg" alt="Stuart" class="avatar avatar-border-white mr-2"/>
                        <div class="media-body">Stuart</div>
                      </div>
                    </div>
                    <div class="card-img-overlay-top text-right"><a href="javascript: void();" class="card-fav-icon position-relative z-index-40"> 
                        <svg class="svg-icon text-white">
                          <use xlink:href="#heart-1"> </use>
                        </svg></a></div>
                  </div>
                  <div class="card-body d-flex align-items-center">
                    <div class="w-100">
                      <h6 class="card-title"><a href="detail-rooms.html" class="text-decoration-none text-dark">Brooklyn Life, Easy to Manhattan</a></h6>
                      <div class="d-flex card-subtitle mb-3">
                        <p class="flex-grow-1 mb-0 text-muted text-sm">Private room</p>
                        <p class="flex-shrink-1 mb-0 card-stars text-xs text-right"><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-warning"></i><i class="fa fa-star text-gray-300">                                  </i>
                        </p>
                      </div>
                      <p class="card-text text-muted"><span class="h4 text-primary">$123</span> per night</p>
                    </div>
                  </div>
                </div>
              </div>
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
        </swiper>

      </div>
    </section>    
  </div>
</template>

<script>
  export default {
    data() {
      return {
        swiperOption: {
          slidesPerView: 4,
          spaceBetween: 20,
          roundLengths :true,
          pagination: {
            el: '.swiper-pagination',
            clickable: true,
            dynamicBullets: true
          },
          loop: true,
          breakpoints: {  
             1200 :{  
               slidesPerView: 3
            },
             991 :{  
              slidesPerView : 2
            },
             565 :{  
              slidesPerView :1
            }
         },
        }
      }
    }
  }
</script>
```

### Step 5.4: Set up DisplayCatalog3 Component
In `myproject-consumer-web/src/components/`
create a file called : `DisplayCatalog3.vue`
Add the following code:
```html
<template>
    <section class="py-6 bg-gray-100"> 
      <div class="container">
        <div class="row mb-5">
          <div class="col-md-8">
            <p class="subtitle text-secondary">Stories from around the globe</p>
            <h2>From our travel blog</h2>
          </div>
          <div class="col-md-4 d-md-flex align-items-center justify-content-end"><a href="blog.html" class="text-muted text-sm">
               
              See all articles<i class="fas fa-angle-double-right ml-2"></i></a></div>
        </div>
        <div class="row">
          <!-- blog item-->
          <div class="col-lg-4 col-sm-6 mb-4">
            <div class="card shadow border-0 h-100"><a href="post.html"><img src="../assets/img/photo/photo-1512917774080-9991f1c4c750.jpg" alt="..." class="img-fluid card-img-top"/></a>
              <div class="card-body"><a href="#" class="text-uppercase text-muted text-sm letter-spacing-2">Travel </a>
                <h5 class="my-2"><a href="post.html" class="text-dark">Autumn fashion tips and tricks          </a></h5>
                <p class="text-gray-500 text-sm my-3"><i class="far fa-clock mr-2"></i>January 16, 2016</p>
                <p class="my-2 text-muted text-sm">Pellentesque habitant morbi tristique senectus. Vestibulum tortor quam, feugiat vitae, ultricies ege...</p><a href="post.html" class="btn btn-link pl-0">Read more<i class="fa fa-long-arrow-alt-right ml-2"></i></a>
              </div>
            </div>
          </div>
          <!-- blog item-->
          <div class="col-lg-4 col-sm-6 mb-4">
            <div class="card shadow border-0 h-100"><a href="post.html"><img src="../assets/img/photo/photo-1522771739844-6a9f6d5f14af.jpg" alt="..." class="img-fluid card-img-top"/></a>
              <div class="card-body"><a href="#" class="text-uppercase text-muted text-sm letter-spacing-2">Living </a>
                <h5 class="my-2"><a href="post.html" class="text-dark">Newest photo apps          </a></h5>
                <p class="text-gray-500 text-sm my-3"><i class="far fa-clock mr-2"></i>January 16, 2016</p>
                <p class="my-2 text-muted text-sm">ellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibu...</p><a href="post.html" class="btn btn-link pl-0">Read more<i class="fa fa-long-arrow-alt-right ml-2"></i></a>
              </div>
            </div>
          </div>
          <!-- blog item-->
          <div class="col-lg-4 col-sm-6 mb-4">
            <div class="card shadow border-0 h-100"><a href="post.html"><img src="../assets/img/photo/photo-1482463084673-98272196658a.jpg" alt="..." class="img-fluid card-img-top"/></a>
              <div class="card-body"><a href="#" class="text-uppercase text-muted text-sm letter-spacing-2">Travel </a>
                <h5 class="my-2"><a href="post.html" class="text-dark">Best books about Photography          </a></h5>
                <p class="text-gray-500 text-sm my-3"><i class="far fa-clock mr-2"></i>January 16, 2016</p>
                <p class="my-2 text-muted text-sm">Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante.  Mauris placerat eleif...</p><a href="post.html" class="btn btn-link pl-0">Read more<i class="fa fa-long-arrow-alt-right ml-2"></i></a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
</template>

```

### Step 5.5: Set up PhotoWheel Component
In `myproject-consumer-web/src/components/`
create a file called : `PhotoWheel.vue`
Add the following code:
```html
<template>
    <section>
      <div class="container-fluid px-0">
        <div class="instagram-slider">
        <swiper :options="swiperOption">
            <swiper-slide><img src="../assets/img/instagram/instagram-1.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-2.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-3.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-4.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-5.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-6.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-7.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-8.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-9.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-10.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-11.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-12.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-13.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
            <swiper-slide><img src="../assets/img/instagram/instagram-14.jpg" alt="" class="img-fluid hover-scale"></swiper-slide>
        </swiper>
        </div>
    </div>
    </section>
</template>

<script>
  export default {
    data() {
      return {
        swiperOption: {
          slidesPerView: 10,
          spaceBetween: 0,
        }
      }
    }
  }
</script>
```

### Step 5.6: Set up Testimonials Component
In `myproject-consumer-web/src/components/`
create a file called : `Testimonials.vue`
Add the following code:
```html
<template>
  <div class="testimonials">
    <section class="py-7">
      <div class="container">
        <div class="text-center">
          <p class="subtitle text-primary">Testimonials</p>
          <h2 class="mb-5">Our dear customers said about us</h2>
        </div>
        <!-- Slider main container-->
        <swiper :options="swiperOption" class="testimonials-slider testimonials">
          <!-- Additional required wrapper-->
            <!-- Slides-->
            <swiper-slide class="px-3">
              <div class="testimonial card rounded-lg shadow border-0">
                <div class="testimonial-avatar"><img src="../assets/img/avatar/avatar-3.jpg" alt="..." class="img-fluid"></div>
                <div class="text">
                  <div class="testimonial-quote"><i class="fas fa-quote-right"></i></div>
                  <p class="testimonial-text">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever</p><strong>Jessica Watson</strong>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="px-3">
              <div class="testimonial card rounded-lg shadow border-0">
                <div class="testimonial-avatar"><img src="../assets/img/avatar/avatar-3.jpg" alt="..." class="img-fluid"></div>
                <div class="text">
                  <div class="testimonial-quote"><i class="fas fa-quote-right"></i></div>
                  <p class="testimonial-text">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever</p><strong>Jessica Watson</strong>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="px-3">
              <div class="testimonial card rounded-lg shadow border-0">
                <div class="testimonial-avatar"><img src="../assets/img/avatar/avatar-3.jpg" alt="..." class="img-fluid"></div>
                <div class="text">
                  <div class="testimonial-quote"><i class="fas fa-quote-right"></i></div>
                  <p class="testimonial-text">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever</p><strong>Jessica Watson</strong>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="px-3">
              <div class="testimonial card rounded-lg shadow border-0">
                <div class="testimonial-avatar"><img src="../assets/img/avatar/avatar-3.jpg" alt="..." class="img-fluid"></div>
                <div class="text">
                  <div class="testimonial-quote"><i class="fas fa-quote-right"></i></div>
                  <p class="testimonial-text">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever</p><strong>Jessica Watson</strong>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="px-3">
              <div class="testimonial card rounded-lg shadow border-0">
                <div class="testimonial-avatar"><img src="../assets/img/avatar/avatar-3.jpg" alt="..." class="img-fluid"></div>
                <div class="text">
                  <div class="testimonial-quote"><i class="fas fa-quote-right"></i></div>
                  <p class="testimonial-text">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever</p><strong>Jessica Watson</strong>
                </div>
              </div>
            </swiper-slide>
            <swiper-slide class="px-3">
              <div class="testimonial card rounded-lg shadow border-0">
                <div class="testimonial-avatar"><img src="../assets/img/avatar/avatar-3.jpg" alt="..." class="img-fluid"></div>
                <div class="text">
                  <div class="testimonial-quote"><i class="fas fa-quote-right"></i></div>
                  <p class="testimonial-text">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever</p><strong>Jessica Watson</strong>
                </div>
              </div>
            </swiper-slide>
          <div class="swiper-pagination"></div>
        </swiper>
      </div>
    </section>
  </div>
</template>

<script scoped>
    export default {
    data() {
      return {
        swiperOption:  {
        slidesPerView: 2,
        spaceBetween: 20,
        loop: true,
        roundLengths: true,
        breakpoints: {
            1200: {
                slidesPerView: 3,
                spaceBetween: 0
            },
            991: {
                slidesPerView: 2,
                spaceBetween: 0
            },
            565: {
                slidesPerView: 1
            }
        },
          // If we need pagination
          pagination: {
              el: '.swiper-pagination',
              clickable: true,
              dynamicBullets: true
          },
      }
      }
    }
  }
</script>
```

### Step 5.7: Import Components into `Home.vue`
Import the individual components we made in steps `5.1` - `5.6`:
In `myproject-consumer-web/src/views`

In the `<template>` tag of `Home.vue` 
 Add the following code:
```html
<template>
  <div class="home">
    <SearchBar/>
    <AboutProduct/>
    <DisplayCatalog1/>
    <DisplayCatalog2/>
    <Testimonials/>
    <DisplayCatalog3/>
    <PhotoWheel/> 
  </div>
</template>
```

In the `<script>` tag of `Home.vue` 
 Add the following code:
```html
<script>
// @ is an alias to /src
import SearchBar from '@/components/SearchBar.vue'
import AboutProduct from '@/components/AboutProduct.vue'
import DisplayCatalog1 from '@/components/DisplayCatalog1.vue'
import DisplayCatalog2 from '@/components/DisplayCatalog2.vue'
import Testimonials from '@/components/Testimonials.vue'
import DisplayCatalog3 from '@/components/DisplayCatalog3.vue'
import PhotoWheel from '@/components/PhotoWheel.vue'

export default {
  name: 'home',
  components: {
    SearchBar, 
    AboutProduct,
    DisplayCatalog1,
    DisplayCatalog2,
    Testimonials,
    DisplayCatalog3,
    PhotoWheel
  }
}

</script>
```

Final Version of `Home.vue`
```html
<template>
  <div class="home">
    <SearchBar/>
    <AboutProduct/>
    <DisplayCatalog1/>
    <DisplayCatalog2/>
    <Testimonials/>
    <DisplayCatalog3/>
    <PhotoWheel/> 
  </div>
</template>

<script>
// @ is an alias to /src
import SearchBar from '@/components/SearchBar.vue'
import AboutProduct from '@/components/AboutProduct.vue'
import DisplayCatalog1 from '@/components/DisplayCatalog1.vue'
import DisplayCatalog2 from '@/components/DisplayCatalog2.vue'
import Testimonials from '@/components/Testimonials.vue'
import DisplayCatalog3 from '@/components/DisplayCatalog3.vue'
import PhotoWheel from '@/components/PhotoWheel.vue'

export default {
  name: 'home',
  components: {
    SearchBar, 
    AboutProduct,
    DisplayCatalog1,
    DisplayCatalog2,
    Testimonials,
    DisplayCatalog3,
    PhotoWheel
  }
}
</script>
```

Final Version of `router.js`
* Important to note that `router.js` takes care of routing to `Home.vue`
* Our home page is accessible via `localhost:8080/`

```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from './views/Home.vue'

Vue.use(Router)

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/about',
      name: 'about',
      component: () => import('./views/About.vue')
    }
  ]
})
```

## Step 6: Set up Login Page

In `myproject-consumer-web/src/views/`
create a file called : `Login.vue`

Add the following snippet
```html
<template>
    <div class="login">
        <div class="container-fluid px-3">
          <div class="row min-vh-100">
            <div class="col-md-8 col-lg-6 col-xl-5 d-flex align-items-center">
              <div class="w-100 py-5 px-md-5 px-xl-6 position-relative">
                <div class="mb-5"><img src="img/logo-square.svg" alt="..." style="max-width: 4rem;" class="img-fluid mb-3">
                  <h2>Welcome back</h2>
                </div>
                <form class="form-validate">
                  <div class="form-group">
                    <label for="loginUsername" class="form-label"> Email Address</label>
                    <input name="loginUsername" id="loginUsername" type="email" placeholder="name@address.com" autocomplete="off" required data-msg="Please enter your email" class="form-control">
                  </div>
                  <div class="form-group mb-4">
                    <div class="row">
                      <div class="col">
                        <label for="loginPassword" class="form-label"> Password</label>
                      </div>
                      <div class="col-auto"><a href="#" class="form-text small">Forgot password?</a></div>
                    </div>
                    <input name="loginPassword" id="loginPassword" placeholder="Password" type="password" required data-msg="Please enter your password" class="form-control">
                  </div>
                  <div class="form-group mb-4">
                    <div class="custom-control custom-checkbox">
                      <input id="loginRemember" type="checkbox" class="custom-control-input">
                      <label for="loginRemember" class="custom-control-label text-muted"> <span class="text-sm">Remember me for 30 days</span></label>
                    </div>
                  </div>
                  <!-- Submit-->
                  <button class="btn btn-lg btn-block btn-primary">Sign in</button>
                  <hr data-content="OR" class="my-3 hr-text letter-spacing-2">
                  <button class="btn btn btn-outline-primary btn-block btn-social mb-3"><i class="fa-2x fa-facebook-f fab btn-social-icon"> </i>Connect <span class="d-none d-sm-inline">with Facebook</span></button>
                  <button class="btn btn btn-outline-muted btn-block btn-social mb-3"><i class="fa-2x fa-google fab btn-social-icon"> </i>Connect <span class="d-none d-sm-inline">with Google</span></button>
                  <hr class="my-4">
                  <p class="text-center"><small class="text-muted text-center">Don't have an account yet? <a href="signup.html">Sign Up                </a></small></p>
                </form><a href="index.html" class="close-absolute mr-md-5 mr-xl-6 pt-5"> 
                  <svg class="svg-icon w-3rem h-3rem">
                    <use xlink:href="#close-1"> </use>
                  </svg></a>
              </div>
            </div>
            <div class="col-md-4 col-lg-6 col-xl-7 d-none d-md-block">
              <!-- Image-->
              <div style="background-image: url(img/photo/photo-1497436072909-60f360e1d4b1.jpg);" class="bg-cover h-100 mr-n3"></div>
            </div>
          </div>
        </div>
    </div>
</template>


<script>
export default {
  name: 'landing',
  props: {
    msg: String
  }
}
</script>

<style type="text/css">
    
    
</style>
```


In `myproject-consumer-web/src/`

Add the following snippet in `router.js`:

```js
{
   path: '/about',
   name: 'about',
   // route level code-splitting
   // this generates a separate chunk (about.[hash].js) for this route
   // which is lazy-loaded when the route is visited.
   component: () => import(/* webpackChunkName: "about" */ './views/About.vue')
},
{ 
   //Added a route for login
   path: '/login',
   name: 'login',
   component: () => import('./views/Login.vue')
}
```

## Step 7: Set up Signup Page

In `myproject-consumer-web/src/views/`
create a file called : `SignUp.vue`

Add the following snippet
```html
<template>
  <div class="signup">
        <div class="container-fluid px-3">
      <div class="row min-vh-100">
        <div class="col-md-8 col-lg-6 col-xl-5 d-flex align-items-center">
          <div class="w-100 py-5 px-md-5 px-xl-6 position-relative">
            <div class="mb-4"><img src="img/logo-square.svg" alt="..." style="max-width: 4rem;" class="img-fluid mb-4">
              <h2>Sign up</h2>
              <p class="text-muted">His room, a proper human room although a little too small, lay peacefully between its four familiar walls. A collection of textile samples lay spread out on the table.</p>
            </div>
            <form class="form-validate">
              <div class="form-group">
                <label for="loginUsername" class="form-label"> Email Address</label>
                <input name="loginUsername" id="loginUsername" type="email" placeholder="name@address.com" autocomplete="off" required data-msg="Please enter your email" class="form-control">
              </div>
              <div class="form-group">
                <label for="loginPassword" class="form-label"> Password</label>
                <input name="loginPassword" id="loginPassword" placeholder="Password" type="password" required data-msg="Please enter your password" class="form-control">
              </div>
              <div class="form-group mb-4">
                <label for="loginPassword2" class="form-label"> Confirm your password</label>
                <input name="loginPassword2" id="loginPassword2" placeholder="Password" type="password" required data-msg="Please enter your password" class="form-control">
              </div>
              <button type="submit" class="btn btn-lg btn-block btn-primary">Sign up</button>
              <hr data-content="OR" class="my-3 hr-text letter-spacing-2">
              <button class="btn btn btn-outline-primary btn-block btn-social mb-3"><i class="fa-2x fa-facebook-f fab btn-social-icon"> </i>Connect <span class="d-none d-sm-inline">with Facebook</span></button>
              <button class="btn btn btn-outline-muted btn-block btn-social mb-3"><i class="fa-2x fa-google fab btn-social-icon"> </i>Connect <span class="d-none d-sm-inline">with Google</span></button>
              <hr class="my-4">
              <p class="text-sm text-muted">By signing up you agree to Directory's <a href="#">Terms and Conditions</a> and <a href="#">Privacy Policy</a>.</p>
            </form><a href="index.html" class="close-absolute mr-md-5 mr-xl-6 pt-5"> 
              <svg class="svg-icon w-3rem h-3rem">
                <use xlink:href="#close-1"> </use>
              </svg></a>
          </div>
        </div>
        <div class="col-md-4 col-lg-6 col-xl-7 d-none d-md-block">
          <!-- Image-->
          <div style="background-image: url(img/photo/photo-1497436072909-60f360e1d4b1.jpg);" class="bg-cover h-100 mr-n3"></div>
        </div>
      </div>
    </div>
  </div>
</template>
```


In `myproject-consumer-web/src/`

Add the following snippet in `router.js`:

```js
{
  path: '/login',
  name: 'login',
  component: () => import('./views/Login.vue')
},
{
  //Add sign up into routes
  path: '/signup',
  name: 'sigup',
  component: () => import('./views/SignUp.vue')
}
```

## Step 8: Set up Product Page

### Step 8.1: Set up `Products.vue` Component
In  `src/views`  create a file called `Products.vue`
Add the following code:

```html
<template>
  <div class="product">
    <ProductIndex/>
        <router-view/>  
  </div>
</template>

<script type="text/javascript">
    import ProductIndex from '@/components/products'

    export default {
    name: 'products',
        components: {
            ProductIndex
        }
    }

</script>

```

### Step 8.2: Set up `products` Folder
In  `src/components`  folder create a folder called  `booking`

```bash
$ cd src/components
$ mkdir products
$ cd products
```

### Step 8.3: Product `index` Component
Create a product index page by re-using `<DisplayCatalog2/>` and `<DisplayCatalog3/>` 

In `myproject-consumer-web/src/views/product`
create a file called : `index.vue`

Add the following code:
```html
<template>
  <div class="products">
    <h1>Product Catalog</h1>
    <DisplayCatalog2/>
    <DisplayCatalog3/>
  </div>
</template>

<style scoped>
  h1 {
    margin-top: 100px;
    text-align: center;
  } 
</style>

<script type="text/javascript">
import DisplayCatalog2 from '@/components/DisplayCatalog2.vue'
import DisplayCatalog3 from '@/components/DisplayCatalog3.vue'


export default {
name: 'products',
  components: {
    DisplayCatalog2,
    DisplayCatalog3
  }
}

</script>
```


### Step 8.4: ProductDetail Component

In `myproject-consumer-web/src/views/product`
create a file called : `ProductDetail.vue`

Add the following code:
```html
<template>
  <div class="product-detail">
    <section>
        <!-- Additional required wrapper-->
        <swiper :options="swiperOption">
          <!-- Slides-->
          <swiper-slide>
            <a href="../../assets/img/photo/photo-1426122402199-be02db90eb90.jpg" data-toggle="gallery-top" title="Our street"><img src="../../assets/img/photo/photo-1426122402199-be02db90eb90.jpg" alt="Our street" class="img-fluid"></a>
          </swiper-slide>
          <swiper-slide>
            <a href="../../assets/img/photo/photo-1512917774080-9991f1c4c750.jpg" data-toggle="gallery-top" title="Outside"><img src="../../assets/img/photo/photo-1512917774080-9991f1c4c750.jpg" alt="Outside" class="img-fluid"></a>
          </swiper-slide>
          <swiper-slide>
            <a href="../../assets/img/photo/photo-1494526585095-c41746248156.jpg" data-toggle="gallery-top" title="Rear entrance"><img src="../../assets/img/photo/photo-1494526585095-c41746248156.jpg" alt="Rear entrance" class="img-fluid"></a>
          </swiper-slide>
          <swiper-slide>
            <a href="../../assets/img/photo/photo-1484154218962-a197022b5858.jpg" data-toggle="gallery-top" title="Kitchen"><img src="../../assets/img/photo/photo-1484154218962-a197022b5858.jpg" alt="Kitchen" class="img-fluid"></a>
          </swiper-slide>
          <swiper-slide>
            <a href="../../assets/img/photo/photo-1522771739844-6a9f6d5f14af.jpg" data-toggle="gallery-top" title="Bedroom"><img src="../../assets/img/photo/photo-1522771739844-6a9f6d5f14af.jpg" alt="Bedroom" class="img-fluid"></a>
          </swiper-slide>
          <swiper-slide>
            <a href="../../assets/img/photo/photo-1488805990569-3c9e1d76d51c.jpg" data-toggle="gallery-top" title="Bedroom"><img src="../../assets/img/photo/photo-1488805990569-3c9e1d76d51c.jpg" alt="Bedroom" class="img-fluid"></a>
          </swiper-slide>
        </swiper>
        <div class="swiper-pagination swiper-pagination-white"></div>
        <div class="swiper-button-prev swiper-button-white"></div>
        <div class="swiper-button-next swiper-button-white"></div>

    </section>
    <div class="container py-5">
      <div class="row">
        <div class="col-lg-8"> 
          <div class="text-block">
            <p class="text-primary"><i class="fa-map-marker-alt fa mr-1"></i> Brooklyn, New York</p>
            <h1>Mid-Century Modern Garden Paradise</h1>
            <p class="text-muted text-uppercase mb-4">Entire Apartment </p>
            <ul class="list-inline text-sm mb-4">
              <li class="list-inline-item mr-3"><i class="fa fa-users mr-1 text-secondary"></i> 4 guests</li>
              <li class="list-inline-item mr-3"><i class="fa fa-door-open mr-1 text-secondary"></i> 1 bedroom</li>
              <li class="list-inline-item mr-3"><i class="fa fa-bed mr-1 text-secondary"></i> 3 beds</li>
              <li class="list-inline-item mr-3"><i class="fa fa-bath mr-1 text-secondary"></i> 1 bath</li>
            </ul>
            <p class="text-muted font-weight-light">Our garden basement apartment is fully equipped with everything you need to enjoy your stay. Very comfortable for a couple but plenty of space for a small family. Close to many wonderful Brooklyn attractions and quick trip to Manhattan. </p>
            <h6 class="mb-3">The space</h6>
            <p class="text-muted font-weight-light">Welcome to Brooklyn! We are excited to share our wonderful neighborhood with you. Our modern apartment has a private entrance, fully equipped kitchen, and a very comfortable queen size bed. We are happy to accommodate additional guests with a single bed in the living room, another comfy mattress on the floor and can make arrangements for small children with a portable crib and highchair if requested. </p>
            <p class="text-muted font-weight-light">Also in the apartment:</p>
            <ul class="text-muted font-weight-light"> 
              <li>TV with Netflix and DirectTVNow</li>
              <li>Free WiFi</li>
              <li>Gourmet Coffee/Tea making supplies</li>
              <li>Fresh Sheets and Towels</li>
              <li>Toaster, microwave, pots and pans and basic cooking needs like salt, pepper, sugar, and olive oil.</li>
              <li>Air Conditioning to keep you cool all summer!</li>
            </ul>
            <p class="text-muted font-weight-light">The apartment is surprisingly quiet for being in the heart of a vibrant, bustling neighborhood.</p>
            <h6 class="mb-3">Interaction with guests</h6>
            <p class="text-muted font-weight-light">We live in the two floors above the garden apartment so we are usually available to answer questions. The garden apartment is separate from our living space. We are happy to provide advice on local attractions, restaurants and transportation around the city. If there's anything you need please don't hesitate to ask!</p>
          </div>
          <div class="text-block">
            <h4 class="mb-4">Amenities</h4>
            <div class="row"> 
              <div class="col-md-6">
                <ul class="list-unstyled text-muted">
                  <li class="mb-2"><i class="fa fa-wifi text-secondary w-1rem mr-3 text-center"></i> <span class="text-sm">Wifi</span></li>
                  <li class="mb-2"><i class="fa fa-tv text-secondary w-1rem mr-3 text-center"></i> <span class="text-sm">Cable TV</span></li>
                  <li class="mb-2"><i class="fa fa-snowflake text-secondary w-1rem mr-3 text-center"></i> <span class="text-sm">Air conditioning</span></li>
                  <li class="mb-2"><i class="fa fa-thermometer-three-quarters text-secondary w-1rem mr-3 text-center"></i> <span class="text-sm">Heating</span></li>
                </ul>
              </div>
              <div class="col-md-6">
                <ul class="list-unstyled text-muted">
                  <li class="mb-2"><i class="fa fa-bath text-secondary w-1rem mr-3 text-center"></i><span class="text-sm">Toiletteries</span></li>
                  <li class="mb-2"><i class="fa fa-utensils text-secondary w-1rem mr-3 text-center"></i><span class="text-sm">Equipped Kitchen</span></li>
                  <li class="mb-2"><i class="fa fa-laptop text-secondary w-1rem mr-3 text-center"></i><span class="text-sm">Desk for work</span></li>
                  <li class="mb-2"><i class="fa fa-tshirt text-secondary w-1rem mr-3 text-center"></i><span class="text-sm">Washing machine</span></li>
                </ul>
              </div>
            </div>
          </div>
          <div class="text-block">
            <h4 class="mb-0">Amenities alternative</h4>
            <p class="subtitle text-sm text-primary mb-4">Alternative amenities display</p>
            <ul class="list-inline">
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Wifi</span></li>
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Cable TV</span></li>
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Air conditioning</span></li>
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Heating</span></li>
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Toiletteries</span></li>
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Equipped Kitchen</span></li>
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Desk for work</span></li>
              <li class="list-inline-item mb-2"><span class="badge badge-pill badge-light p-3 text-muted font-weight-normal">Washing machine</span></li>
            </ul>
          </div>
          <div class="text-block">
            <div class="media"><img src="../../assets/img/avatar/avatar-10.jpg" alt="Jack London" class="avatar avatar-lg mr-4">
              <div class="media-body">
                <p> <span class="text-muted text-uppercase text-sm">Hosted by </span><br><strong>Jack London</strong></p>
                <p class="text-muted text-sm mb-2">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore.</p>
                <p class="text-muted text-sm">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. </p>
                <p class="text-sm"><a href="#">See Jack's 3 other listings <i class="fa fa-long-arrow-alt-right ml-2"></i></a></p>
              </div>
            </div>
          </div>
          <div class="text-block">
            <h5 class="mb-4">Listing location</h5>
            <div class="map-wrapper-300 mb-3">
              <div id="detailMap" class="h-100"></div>
            </div>
          </div>
          <div class="text-block">
            <h5 class="mb-4">Gallery</h5>
            <div class="row gallery mb-3 ml-n1 mr-n1">
              <div class="col-lg-4 col-6 px-1 mb-2"><a href="../../assets/img/photo/photo-1426122402199-be02db90eb90.jpg" data-fancybox="gallery" title="Our street"><img src="../../assets/img/photo/photo-1426122402199-be02db90eb90.jpg" alt="..." class="img-fluid"></a></div>
              <div class="col-lg-4 col-6 px-1 mb-2"><a href="../../assets/img/photo/photo-1512917774080-9991f1c4c750.jpg" data-fancybox="gallery" title="Outside"><img src="../../assets/img/photo/photo-1512917774080-9991f1c4c750.jpg" alt="..." class="img-fluid"></a></div>
              <div class="col-lg-4 col-6 px-1 mb-2"><a href="../../assets/img/photo/photo-1494526585095-c41746248156.jpg" data-fancybox="gallery" title="Rear entrance"><img src="../../assets/img/photo/photo-1494526585095-c41746248156.jpg" alt="..." class="img-fluid"></a></div>
              <div class="col-lg-4 col-6 px-1 mb-2"><a href="../../assets/img/photo/photo-1484154218962-a197022b5858.jpg" data-fancybox="gallery" title="Kitchen"><img src="../../assets/img/photo/photo-1484154218962-a197022b5858.jpg" alt="..." class="img-fluid"></a></div>
              <div class="col-lg-4 col-6 px-1 mb-2"><a href="../../assets/img/photo/photo-1522771739844-6a9f6d5f14af.jpg" data-fancybox="gallery" title="Bedroom"><img src="../../assets/img/photo/photo-1522771739844-6a9f6d5f14af.jpg" alt="..." class="img-fluid"></a></div>
              <div class="col-lg-4 col-6 px-1 mb-2"><a href="../../assets/img/photo/photo-1488805990569-3c9e1d76d51c.jpg" data-fancybox="gallery" title="Bedroom"><img src="../../assets/img/photo/photo-1488805990569-3c9e1d76d51c.jpg" alt="..." class="img-fluid"></a></div>
            </div>
          </div>
          <div class="text-block">
            <p class="subtitle text-sm text-primary">Reviews    </p>
            <h5 class="mb-4">Listing Reviews </h5>
            <div class="media d-block d-sm-flex review">
              <div class="text-md-center mr-4 mr-xl-5"><img src="../../assets/img/avatar/avatar-8.jpg" alt="Padmé Amidala" class="d-block avatar avatar-xl p-2 mb-2"><span class="text-uppercase text-muted text-sm">Dec 2018</span></div>
              <div class="media-body">
                <h6 class="mt-2 mb-1">Padmé Amidala</h6>
                <div class="mb-2"><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i>
                </div>
                <p class="text-muted text-sm">One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed in his bed into a horrible vermin. He lay on his armour-like back, and if he lifted his head a little he could see his brown belly, slightly domed and divided by arches into stiff sections     </p>
              </div>
            </div>
            <div class="media d-block d-sm-flex review">
              <div class="text-md-center mr-4 mr-xl-5"><img src="../../assets/img/avatar/avatar-2.jpg" alt="Luke Skywalker" class="d-block avatar avatar-xl p-2 mb-2"><span class="text-uppercase text-muted text-sm">Dec 2018</span></div>
              <div class="media-body">
                <h6 class="mt-2 mb-1">Luke Skywalker</h6>
                <div class="mb-2"><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-gray-200"></i>
                </div>
                <p class="text-muted text-sm">The bedding was hardly able to cover it and seemed ready to slide off any moment. His many legs, pitifully thin compared with the size of the rest of him, waved about helplessly as he looked. &quot;What's happened to me?&quot; he thought. It wasn't a dream.     </p>
              </div>
            </div>
            <div class="media d-block d-sm-flex review">
              <div class="text-md-center mr-4 mr-xl-5"><img src="../../assets/img/avatar/avatar-3.jpg" alt="Princess Leia" class="d-block avatar avatar-xl p-2 mb-2"><span class="text-uppercase text-muted text-sm">Dec 2018</span></div>
              <div class="media-body">
                <h6 class="mt-2 mb-1">Princess Leia</h6>
                <div class="mb-2"><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-gray-200"></i><i class="fa fa-xs fa-star text-gray-200"></i>
                </div>
                <p class="text-muted text-sm">His room, a proper human room although a little too small, lay peacefully between its four familiar walls. A collection of textile samples lay spread out on the table.     </p>
              </div>
            </div>
            <div class="media d-block d-sm-flex review">
              <div class="text-md-center mr-4 mr-xl-5"><img src="../../assets/img/avatar/avatar-4.jpg" alt="Jabba Hut" class="d-block avatar avatar-xl p-2 mb-2"><span class="text-uppercase text-muted text-sm">Dec 2018</span></div>
              <div class="media-body">
                <h6 class="mt-2 mb-1">Jabba Hut</h6>
                <div class="mb-2"><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i>
                </div>
                <p class="text-muted text-sm">Samsa was a travelling salesman - and above it there hung a picture that he had recently cut out of an illustrated magazine and housed in a nice, gilded frame.     </p>
              </div>
            </div>
            <div class="py-5">
              <button type="button" data-toggle="collapse" data-target="#leaveReview" aria-expanded="false" aria-controls="leaveReview" class="btn btn-outline-primary">Leave a review</button>
              <div id="leaveReview" class="collapse mt-4">
                <h5 class="mb-4">Leave a review</h5>
                <form id="contact-form" method="get" action="#" class="form">
                  <div class="row">
                    <div class="col-sm-6">
                      <div class="form-group">
                        <label for="name" class="form-label">Your name *</label>
                        <input type="text" name="name" id="name" placeholder="Enter your name" required="required" class="form-control">
                      </div>
                    </div>
                    <div class="col-sm-6">
                      <div class="form-group">
                        <label for="rating" class="form-label">Your rating *</label>
                        <select name="rating" id="rating" class="custom-select focus-shadow-0">
                          <option value="5">&#9733;&#9733;&#9733;&#9733;&#9733; (5/5)</option>
                          <option value="4">&#9733;&#9733;&#9733;&#9733;&#9734; (4/5)</option>
                          <option value="3">&#9733;&#9733;&#9733;&#9734;&#9734; (3/5)</option>
                          <option value="2">&#9733;&#9733;&#9734;&#9734;&#9734; (2/5)</option>
                          <option value="1">&#9733;&#9734;&#9734;&#9734;&#9734; (1/5)</option>
                        </select>
                      </div>
                    </div>
                  </div>
                  <div class="form-group">
                    <label for="email" class="form-label">Your email *</label>
                    <input type="email" name="email" id="email" placeholder="Enter your  email" required="required" class="form-control">
                  </div>
                  <div class="form-group">
                    <label for="review" class="form-label">Review text *</label>
                    <textarea rows="4" name="review" id="review" placeholder="Enter your review" required="required" class="form-control"></textarea>
                  </div>
                  <button type="submit" class="btn btn-primary">Post review</button>
                </form>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-4">
          <div style="top: 100px;" class="p-4 shadow ml-lg-4 rounded sticky-top">
            <p class="text-muted"><span class="text-primary h2">$120</span> per night</p>
            <hr class="my-4">
            <form id="booking-form" method="get" action="#" autocomplete="off" class="form">
              <div class="form-group">
                <label for="bookingDate" class="form-label">Your stay *</label>
                <div class="datepicker-container datepicker-container-right">
                  <input type="text" name="bookingDate" id="bookingDate" placeholder="Choose your dates" required="required" class="form-control">
                </div>
              </div>
              <div class="form-group mb-4">
                <label for="guests" class="form-label">Guests *</label>
                <select name="guests" id="guests" class="form-control">
                  <option value="1">1 Guest</option>
                  <option value="2">2 Guests</option>
                  <option value="3">3 Guests</option>
                  <option value="4">4 Guests</option>
                  <option value="5">5 Guests</option>
                </select>
              </div>
              <div class="form-group">
                <button type="submit" class="btn btn-primary btn-block">Book your stay</button>
              </div>
            </form>
            <p class="text-muted text-sm text-center">Some additional text can be also placed here.</p>
            <hr class="my-4">
            <div class="text-center">
              <p> <a href="#" class="text-secondary text-sm"> <i class="fa fa-heart"></i> Bookmark This Listing</a></p>
              <p class="text-muted text-sm">79 people bookmarked this place </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="py-6 bg-gray-100">
          <DisplayCatalog2/>
    </div>
  </div>
</template>
<script type="text/javascript">
  
import DisplayCatalog2 from '@/components/DisplayCatalog2.vue'

export default {
    name: 'product-detail',
    components: {
      DisplayCatalog2,
    },
    data() {
      return {
        swiperOption: {
            slidesPerView: 2,
            spaceBetween: 0,
            centeredSlides: true,
            loop: true,
            // If we need pagination
            pagination: {
                el: '.swiper-pagination',
                clickable: true,
                dynamicBullets: true
            },

            // Navigation arrows
            navigation: {
                nextEl: '.swiper-button-next',
                prevEl: '.swiper-button-prev',
            },
          }
        }
      }
    }
</script>
```

### Step 8.5: Configure `router.js` Component

In `myproject-consumer-web/src/router.js`

Add the following snippet:
```js
{
  path: '/products',
  name: 'products',
  component: () => import('./views/Products.vue'),
},
{
  path: '/products/:id',
  name: 'product_detail',
  component: () => import('./components/products/ProductDetail.vue')

}
```

Final version of `router.js`:
```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from './views/Home.vue'

Vue.use(Router)

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/about',
      name: 'about',
      component: () => import('./views/About.vue')
    },
    {
      path: '/login',
      name: 'login',
      component: () => import('./views/Login.vue')
    },
    {
      path: '/signup',
      name: 'sigup',
      component: () => import('./views/SignUp.vue')
    },
    {
      path: '/products',
      name: 'products',
      component: () => import('./views/Products.vue'),
    },
    {
      path: '/products/:id',
      name: 'product_detail',
      component: () => import('./components/products/ProductDetail.vue')
    }
  ]
})
```

## Step 9: Set up Booking Page

### Step 9.1: Set up `Booking.vue` Component
In `src/views` folder create a file called `Booking.vue`
In `Booking.vue`, copy the following code:
```html
<template>
  <div class="booking">
    <router-view/>
  </div>
</template>
<script>
</script>
```

In `myproject-consumer-web/src/`

Add the following snippet in `router.js`:

```js
{
    path: '/booking',
    name: 'booking',
    component: () => import('./views/Booking.vue'),
}
```

### Step 9.2: Set up BookingPanel Component
In `src/components` folder create a folder called `booking`
```bash
$ cd src/components
$ mkdir booking
$ cd booking
```
In the `booking` folder, create a file called `BookingPanel.vue`
```bash
$ touch BookingPanel.vue
```

In `BookingPanel.vue` copy the following code:

```html
<template>
  <div class="booking-panel">
     <div class="card border-0 shadow">
      <div class="card-body p-4">
        <div class="text-block pb-3">
          <div class="media align-items-center">
            <div class="media-body">
              <h6> <a href="detail-rooms.html" class="text-reset">Modern Apt - Vibrant Neighborhood</a></h6>
              <p class="text-muted text-sm mb-0">Entire home in New York</p>
              <div class="mt-n1"><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-primary"></i><i class="fa fa-xs fa-star text-gray-200"></i>
              </div>
            </div><a href="detail-rooms.html"><img src="../../assets/img/photo/photo-1512917774080-9991f1c4c750.jpg" alt="" width="100" class="ml-3 rounded"></a>
          </div>
        </div>
        <div class="text-block py-3">
          <ul class="list-unstyled mb-0">
            <li class="mb-3"><i class="fas fa-users fa-fw text-muted mr-2"></i>3 guests</li>
            <li class="mb-0"><i class="far fa-calendar fa-fw text-muted mr-2"></i>Apr 17, 2019 <i class="fas fa-arrow-right fa-fw text-muted mx-3"></i>Apr 18, 2019</li>
          </ul>
        </div>
        <div class="text-block pt-3 pb-0">
          <table class="w-100">
            <tbody>
              <tr>
                <th class="font-weight-normal py-2">$432.02 x 1 night</th>
                <td class="text-right py-2">$432.02</td>
              </tr>
              <tr>
                <th class="font-weight-normal pt-2 pb-3">Service fee</th>
                <td class="text-right pt-2 pb-3">$67.48</td>
              </tr>
            </tbody>
            <tfoot>
              <tr class="border-top">
                <th class="pt-3">Total</th>
                <td class="font-weight-bold text-right pt-3">$499.50</td>
              </tr>
            </tfoot>
          </table>
        </div>
      </div>
      <div class="card-footer bg-primary-light py-4 border-0">
        <div class="media align-items-center">
          <div class="media-body">
            <h6 class="text-primary">Flexible – free cancellation</h6>
            <p class="text-sm text-primary opacity-8 mb-0">Cancel within 48 hours of booking to get a full refund. <a href="#" class="text-reset ml-3">More details</a></p>
          </div>
          <svg class="svg-icon svg-icon svg-icon-light w-3rem h-3rem ml-2 text-primary">
            <use xlink:href="#diploma-1"> </use>
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>
```

### Step 9.3: Set up Book-1 Page

In the `booking` folder, create a file called `Step1.vue`

In `Step1.vue` copy the following code:
*Note that `Step1.vue` imports BookingPanel as a child component
```html
<template>
  <div class="booking-step1">
    <!-- progress bar -->
    <div style="height: 8px; top: 71px;" class="progress rounded-0 sticky-top">
      <div role="progressbar" style="width: 25%" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100" class="progress-bar"></div>
    </div>

    <section class="py-5">
      <div class="container">
        <div class="row">
          <div class="col-lg-7">
            <p class="subtitle text-primary">Book your holiday home</p>
            <h1 class="h2 mb-5"> Review house rules <span class="text-muted float-right">Step 1</span>      </h1>
            <div class="text-block">
              <div class="alert alert-warning text-sm mb-3">
                <div class="media align-items-center">
                  <svg class="svg-icon svg-icon svg-icon-light w-2rem h-2rem mr-3 text-reset">
                    <use xlink:href="#heart-1"> </use>
                  </svg>
                  <div class="media-body"><strong>This home is on people’s minds.</strong> It’s been viewed 43 times in the past week.</div>
                </div>
              </div>
            </div>
            <div class="text-block">
              <h5 class="mb-4">1 night in London</h5>
              <div class="row mb-3">
                <div class="col-md-6 d-flex align-items-center mb-3 mb-md-0">
                  <div class="date-tile mr-3">
                    <div class="text-uppercase"> <span class="text-sm">Apr</span><br><strong class="text-lg">17</strong></div>
                  </div>
                  <p class="text-sm mb-0">Wednesday check-in<br>3PM - 7PM</p>
                </div>
                <div class="col-md-6 d-flex align-items-center">
                  <div class="date-tile mr-3">
                    <div class="text-uppercase"> <span class="text-sm">Apr</span><br><strong class="text-lg">18</strong></div>
                  </div>
                  <p class="text-sm mb-0">Thursday check-out<br>11AM</p>
                </div>
              </div>
            </div>
            <div class="text-block">
              <h5 class="mb-4">Things to keep in mind</h5>
              <ul class="list-unstyled">
                <li class="mb-2"> 
                  <div class="media align-items-center mb-3">
                    <div class="icon-rounded icon-rounded-sm bg-secondary-light mr-4"><i class="fa fas fa-child text-secondary fa-fw text-center"></i></div>
                    <div class="media-body"><span class="text-sm">Not suitable for children and infants - The entrance staircase doesn't have handrails</span></div>
                  </div>
                </li>
                <li class="mb-2"> 
                  <div class="media align-items-center mb-3">
                    <div class="icon-rounded icon-rounded-sm bg-secondary-light mr-4"><i class="fa fas fa-glass-cheers text-secondary fa-fw text-center"></i></div>
                    <div class="media-body"><span class="text-sm">No parties or events</span></div>
                  </div>
                </li>
                <li class="mb-2"> 
                  <div class="media align-items-center mb-3">
                    <div class="icon-rounded icon-rounded-sm bg-secondary-light mr-4"><i class="fa fa-smoking-ban text-secondary fa-fw text-center"></i></div>
                    <div class="media-body"><span class="text-sm">No smoking</span></div>
                  </div>
                </li>
                <li class="mb-2"> 
                  <div class="media align-items-center mb-3">
                    <div class="icon-rounded icon-rounded-sm bg-secondary-light mr-4"><i class="fa fa-cat text-secondary fa-fw text-center"></i></div>
                    <div class="media-body"><span class="text-sm">No pets</span></div>
                  </div>
                </li>
              </ul>
            </div>
            <div class="row form-block flex-column flex-sm-row">
              <div class="col text-center text-sm-left">
              </div>
              <div class="col text-center text-sm-right"><router-link to="step2" class="btn btn-primary px-3">
                  
                  Next step<i class="fa-chevron-right fa ml-2"></i></router-link></div>
            </div>
          </div>
          <div class="col-lg-5 pl-xl-5">
            <!-- Add booking panel here -->
            <BookingPanel/>

          </div>
        </div>
      </div>
    </section>
</div>    
</template>
<script>
  import BookingPanel from '@/components/booking/BookingPanel.vue'

  export default {
    name: 'step1',
    components: {
      BookingPanel
    }
  }
</script>
```

### Step 9.3: Set up Book-2 Page
In the `booking` folder, create a file called `Step1.vue`

In `Step2.vue` copy the following code:
```html
<template>
    <div class="booking-step2">
  <div style="height: 8px; top: 71px;" class="progress rounded-0 sticky-top">
      <div role="progressbar" style="width: 50%" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100" class="progress-bar"></div>
    </div>
    <section class="py-5">
      <div class="container">
        <div class="row">
          <div class="col-lg-7">
            <p class="subtitle text-primary">Book your holiday home</p>
            <h1 class="h2 mb-5"> Who's coming? <span class="text-muted float-right">Step 2</span>      </h1>
            <div class="text-block">
              <div class="alert alert-warning text-sm mb-3">
                <div class="media align-items-center">
                  <svg class="svg-icon svg-icon svg-icon-light w-2rem h-2rem mr-3 text-reset">
                    <use xlink:href="#heart-1"> </use>
                  </svg>
                  <div class="media-body"><strong>This home is on people’s minds.</strong> It’s been viewed 43 times in the past week.</div>
                </div>
              </div>
            </div>
            <div class="text-block">
              <label for="form_guests" class="h5">Guests</label>
              <p class="text-sm text-muted">One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed in his bed in.</p>
              <div class="row">
                <div class="col-lg-6 mb-3">
                  <select name="guests" id="form_guests" data-style="btn-selectpicker" title=" " class="selectpicker form-control">
                    <option value="guests_0">1</option>
                    <option value="guests_1">2</option>
                    <option value="guests_2" selected>3</option>
                    <option value="guests_3">4</option>
                    <option value="guests_4">5</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="text-block">
              <h5>What's the main purpose of this trip?</h5>
              <p class="text-sm text-muted">The bedding was hardly able to cover it and seemed ready to slide off any moment. His many legs, pit.</p>
              <ul class="list-unstyled">
                <li>
                  <div class="custom-control custom-radio">
                    <input type="radio" id="purpose_0" name="purpose" class="custom-control-input">
                    <label for="purpose_0" class="custom-control-label">Personal travel      </label>
                  </div>
                </li>
                <li>
                  <div class="custom-control custom-radio">
                    <input type="radio" id="purpose_1" name="purpose" class="custom-control-input">
                    <label for="purpose_1" class="custom-control-label">Business travel      </label>
                  </div>
                </li>
              </ul>
            </div>
            <div class="text-block">
              <div class="media">
                <div class="media-body">
                  <h5>Say hello to your host</h5>
                  <p class="text-sm text-muted">His room, a proper human room although a little too small, lay peacefully between its four familiar .</p>
                </div><img src="../../assets/img/avatar/avatar-10.jpg" alt="Jack London" class="avatar ml-4">
              </div>
              <textarea name="hello" rows="4" class="form-control"></textarea>
            </div>
            <div class="row form-block flex-column flex-sm-row">
              <div class="col text-center text-sm-left"><router-link to="step1" class="btn btn-link text-muted"> <i class="fa-chevron-left fa mr-2"></i>Back</router-link>
              </div>
              <div class="col text-center text-sm-right"><router-link to="payment" class="btn btn-primary px-3">
                   
                  Next step<i class="fa-chevron-right fa ml-2"></i></router-link></div>
            </div>
          </div>
          <div class="col-lg-5 pl-xl-5">
           <!-- add booking panel here -->
           <BookingPanel/>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import BookingPanel from '@/components/booking/BookingPanel.vue'

  export default {
    name: 'step1',
    components: {
      BookingPanel
    }
  }
</script>
```

### Step 9.4: Set up Payment and Confirmation Component
In the `booking` folder, create a file called `Step3.vue`
In `Step3.vue` copy the following code:
```html
<template>
    <div class="booking-step3">
  <div style="height: 8px; top: 71px;" class="progress rounded-0 sticky-top">
      <div role="progressbar" style="width: 75%" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100" class="progress-bar"></div>
    </div>
    <section class="py-5">
      <div class="container">
        <div class="row">
          <div class="col-lg-7">
            <p class="subtitle text-primary">Book your holiday home</p>
            <h1 class="h2 mb-5"> Confirm and pay <span class="text-muted float-right">Step 3</span>      </h1>
            <div class="text-block">
              <div class="alert alert-warning text-sm mb-3">
                <div class="media align-items-center">
                  <svg class="svg-icon svg-icon svg-icon-light w-2rem h-2rem mr-3 text-reset">
                    <use xlink:href="#heart-1"> </use>
                  </svg>
                  <div class="media-body"><strong>This home is on people’s minds.</strong> It’s been viewed 43 times in the past week.</div>
                </div>
              </div>
            </div>
            <div class="text-block">
              <form action="#">
                <div class="d-flex justify-content-between align-items-end mb-4">
                  <h5 class="mb-0">Pay with your card</h5>
                  <div class="text-muted"><i class="fab fa-cc-amex fa-2x mr-2"> </i><i class="fab fa-cc-visa fa-2x mr-2"> </i><i class="fab fa-cc-mastercard fa-2x"></i></div>
                </div>
                <select name="payment" id="form_payment" data-style="btn-selectpicker" class="selectpicker form-control mb-3">
                  <option value="">Visa •••• 5687</option>
                  <option value="">Mastercard •••• 4569</option>
                </select>
                <button type="button" data-toggle="collapse" data-target="#addNewCard" aria-expanded="false" aria-controls="addNewCard" data-expanded-text="Close" data-collapsed-text="Add a new card" class="btn btn-link btn-collapse pl-0 text-muted">Add a new card</button>
                <div id="addNewCard" class="row collapse">
                  <div class="form-group col-md-6">
                    <label for="card-name" class="form-label">Name on Card</label>
                    <input type="text" name="card-name" placeholder="Name on card" id="card-name" class="form-control">
                  </div>
                  <div class="form-group col-md-6">
                    <label for="card-number" class="form-label">Card Number</label>
                    <input type="text" name="card-number" placeholder="Card number" id="card-number" class="form-control">
                  </div>
                  <div class="form-group col-md-4">
                    <label for="expiry-date" class="form-label">Expiry Date</label>
                    <input type="text" name="expiry-date" placeholder="MM/YY" id="expiry-date" class="form-control">
                  </div>
                  <div class="form-group col-md-4">
                    <label for="cvv" class="form-label">CVC/CVV</label>
                    <input type="text" name="cvv" placeholder="123" id="cvv" class="form-control">
                  </div>
                  <div class="form-group col-md-4">
                    <label for="zip" class="form-label">ZIP</label>
                    <input type="text" name="zip" placeholder="123" id="zip" class="form-control">
                  </div>
                </div>
              </form>
            </div>
            <div class="text-block">
              <h6>Cancellation policy</h6>
              <p class="text-sm text-muted">Samsa was a travelling salesman - and above it there hung a picture that he had recently cut out of .</p>
              <p class="text-sm text-muted">He must have tried it a hundred times, shut his eyes so that he wouldn't have to look at the flounde.</p>
            </div>
            <div class="row form-block flex-column flex-sm-row">
              <div class="col text-center text-sm-left"><a href="step2" class="btn btn-link text-muted"> <i class="fa-chevron-left fa mr-2"></i>Back</a>
              </div>
              <div class="col text-center text-sm-right"><a href="confirmed" class="btn btn-primary px-3">
                   
                  Next step<i class="fa-chevron-right fa ml-2"></i></a></div>
            </div>
          </div>
          <div class="col-lg-5 pl-xl-5">
           <!-- add booking panel here -->
           <BookingPanel/>
          </div>
        </div>
      </div>
    </section>
    </div>
</template>

<script>
  import BookingPanel from '@/components/booking/BookingPanel.vue'

  export default {
    name: 'step1',
    components: {
      BookingPanel
    }
  }
</script>
```

### Step 9.5: Set up Confirmed Component
In the `booking` folder, create a file called `Step4.vue`

In `Step4.vue` copy the following code:
```html
<template>
    <div class="booking-step4">
  <div style="height: 8px; top: 71px;" class="progress rounded-0 sticky-top">
      <div role="progressbar" style="width: 100%" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" class="progress-bar"></div>
    </div>
    <section class="py-5">
      <div class="container">
        <div class="row">
          <div class="col-lg-7">
            <p class="subtitle text-primary">Book your holiday home</p>
            <h1 class="h2 mb-5"> Booking placed <span class="text-muted float-right">Step 4</span>      </h1>
            <div class="text-block">
              <p class="text-muted">Thank you for your booking, Ondrej. </p>
              <p class="text-muted mb-5">Samsa was a travelling salesman - and above it there hung a picture that he had recently cut out of an illustrated magazine and housed in a nice, gilded frame.</p>
              <p class="text-center mb-5"><a href="user-booking-detail.html" class="btn btn-primary mx-2 mb-2"> <i class="far fa-file mr-2"></i>View your order</a><router-link to="/" class="btn btn-outline-muted mb-2">Or something else</router-link></p>
              <p class="mb-5 text-center"><img src="img/illustration/undraw_celebration_0jvk.svg" alt="" style="width: 400px;" class="img-fluid"></p>
            </div>
          </div>
          <div class="col-lg-5 pl-xl-5">
           <!-- add booking panel here -->
           <BookingPanel/>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
  import BookingPanel from '@/components/booking/BookingPanel.vue'

  export default {
    name: 'step1',
    components: {
      BookingPanel
    }
  }
</script>
```


### Step 9.6: Set up Router for all Bookings 

In `myproject-consumer-web/src/`
Add the following snippet in `router.js`:

```js
{
    path: '/booking',
    name: 'booking',
    component: () => import('./views/Booking.vue'),
}
```

under the path `/booking`, add a key called children that takes in a list of child paths:
```js
 {
      path: '/booking',
      name: 'booking',
      component: () => import('./views/Booking.vue'),
      children: [
        {
          path: 'step1',
          component: () => import('./components/booking/Step1.vue'),
        },
        {
          path: 'step2',
          component: () => import('./components/booking/Step2.vue'),
        },
        {
          path: 'payment',
          component: () => import('./components/booking/Step3.vue'),
        },
        {
          path: 'confirmed',
          component: () => import('./components/booking/Step4.vue'),
        }
      ]
    }
``` 

*this will allow us to access our bookings via, `/booking/<path to step>`

eg:
```bash
http://[hostname]/booking/step1
http://[hostname]/booking/step2
http://[hostname]/booking/payment
http://[hostname]/booking/confirmed
```

Final version of `router.js`:
```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from './views/Home.vue'

Vue.use(Router)

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/about',
      name: 'about',
      component: () => import('./views/About.vue')
    },
    {
      path: '/login',
      name: 'login',
      component: () => import('./views/Login.vue')
    },
    {
      path: '/signup',
      name: 'sigup',
      component: () => import('./views/SignUp.vue')
    },
    {
      path: '/booking',
      name: 'booking',
      component: () => import('./views/Booking.vue'),
      children: [
        {
          path: 'step1',
          component: () => import('./components/booking/Step1.vue'),
        },
        {
          path: 'step2',
          component: () => import('./components/booking/Step2.vue'),
        },
        {
          path: 'payment',
          component: () => import('./components/booking/Step3.vue'),
        },
        {
          path: 'confirmed',
          component: () => import('./components/booking/Step4.vue'),
        }
      ]
    },
    {
      path: '/products',
      name: 'products',
      component: () => import('./views/Products.vue'),
      children: [
        {
          path: ':id',
          component: () => import('./components/products/ProductDetail.vue'),
        }
      ] 
    }
  ]
})
```


## Step 10: Set up Axios to Consume Data 

### Step 10.1: Install Axios
In the terminal run, inside your project folder, the following command: 
```bash
$ npm install axios --save
```

in `myproject-vuejs-web/package.json` you must see the following dependencies:
```json
  "dependencies": {
    "bootstrap": "^4.3.1",
    "jquery": "^3.4.1",
    "popper.js": "^1.15.0",
    "axios": "^0.18.0"
  },
```

### Step 10.2: Modify Home Page to Include Axios

In `myproject-vuejs-web/src/main.js`
Add the following lines:

```js
import axios from 'axios'
Vue.prototype.$http = axios;
```

### (Optional) Clean up
```
$ aws codecommit delete-repository --repository-name myproject-vuejs-web
$ rm -rf ~/environment/myproject-vuejs-web
```

