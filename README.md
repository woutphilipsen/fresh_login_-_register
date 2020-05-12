## git clone this project & cd into it, run the following commands
    composer install
    npm install
    npm run watch

## Make a database en setup .env file for local development & run
    php artisan migrate

## Start project & yor app will be available @ localhost:8000
    php artisan serve
## ---------------------------------------

## things that changed from fresh laravel project
##  inertia after initializing 

SERVER-SIDE

## Install dependencies
## Install the Inertia server-side adapters using the preferred package manager for 
## that language or framework.
    composer require inertiajs/inertia-laravel
## ---------------------------------------

## Next, setup the root template that will be loaded on the first page visit. This will be used to load 
## your site assets (CSS and JavaScript), and will also contain a root <div> to boot your JavaScript  
## application in resources/js/app.js.
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
        <link href="{{ mix('/css/app.css') }}" rel="stylesheet" />
        <script src="{{ mix('/js/app.js') }}" defer></script>
    </head>
    <body>
        @inertia
    </body>
    </html>

## Make controller for dashboard & set up the rote to this controller
    php artisan make:controller DashboardController
## --------------------------------------------

## Make route in routes.php
    <?php
    use App\Http\Controllers\DashboardController;

    Route::get('/', function () {
        return view('welcome');
    });

    Route::get('dashboard', [DashboardController::class, 'index']);
## ------------------------------------------------------------

## Creating responses
## That's it, you're all ready to go server-side! From here you can start creating Inertia responses. See ## the responses page for more information.
    <?php
    namespace App\Http\Controllers;

    use Illuminate\Http\Request;
    use Inertia\Inertia;

    class DashboardController extends Controller
    {
        public function index() 
        {
            $data = [
                'fname' => 'Wout',
                'lname' => 'Philipsen',
            ];

            return Inertia::render('Dashboard/Index', $data);
        }
    }
## -------------------------------------------

## IN NEED OF LOGIN/REGISTER SYSTEM, YOU CAN IMPLEMENT NEXT PACKAGES
    composer require laravel/ui
## -------------------------------------------
## Install vue authentication scaffolding for CSS, JavaScript & BOOTSTRAP4
    php artisan ui vue --auth 
## -------------------------------------------
## generate file with package manager
    npm install
## -------------------------------------------
## Setup .env file, make link to database
## Run following command to initialize database
    php artisan migrate
## -------------------------------------------
## COMPILE PROJECT
    npm run watch
## -------------------------------------------


## CLIENT-SIDE

## Install dependencies
## Install the Inertia client-side adapters using NPM or Yarn.
    npm install @inertiajs/inertia @inertiajs/inertia-vue
## --------------------------------------------------

## Initialize app
## Next, update your main JavaScript file to boot your Inertia app. All we're doing here is initializing 
## the client-side framework with the base Inertia page component.
## resources/js/app.js
    require('./bootstrap');

    import { InertiaApp } from '@inertiajs/inertia-vue'
    import Vue from 'vue'

    Vue.use(InertiaApp)

    const app = document.getElementById('app')

    new Vue({
    render: h => h(InertiaApp, {
        props: {
        initialPage: JSON.parse(app.dataset.page),
        resolveComponent: name => require(`./Pages/${name}`).default,
        },
    }),
    }).$mount(app)
## The resolveComponent is a callback that tells Inertia how to load a page component. It receives a page ## name (string), and must return a component instance.
## ----------------------------------------------------

## We need to create a Pages folder resources/js
## ---------------------------------------------

## After this step our LOGIN/REGISTR will stop working
## go to resources/views/layouts/app.blade.php & change line 23 in to
    <div id="no-app">
## ---------------------------------------------

## In app.js -> make an if statement on if (app)
    if (app) {
    new Vue({
        render: h => h(InertiaApp, {
        props: {
            initialPage: JSON.parse(app.dataset.page),
            resolveComponent: name => require(`./Pages/${name}`).default,
        },
        }),
    }).$mount(app)
    }
## ---------------------------------------------

## EVERYTHING SHOULD BE SETUP & READY TO GO FROM HERE