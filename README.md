#generator-go-gas

>Yeoman Generator for Enterprise Angular Projects with Gulp and Sass

This generator follows the [Angular Best Practice Guidelines for Project Structure](https://docs.google.com/document/d/1XXMvReO8-Awi1EZXAXS4PzDzdNvV6pGcuaF4Q9821Es/pub).

Features

* Provides a directory structure geared towards large modularized Angular projects.
    * Each controller, service, filter, and directive are placed in their own file.
    * All files related to a conceptual unit are placed together.  For example, the controller, HTML, STYLUS, and unit test for a partial are placed together in the same directory.
* Provides a ready-made Gulp build that produces an extremely optimized distribution.
   * `gulp serve` task allows you to run a simple development server with watch/livereload enabled.  Additionally, JSHint and the appropriate unit tests are run for the changed files.
* Integrates Bower for package management
* Includes Yeoman subgenerators for directives, services, partials, filters, and modules.
* Integrates LESS and includes Bootstrap via the source LESS files allowing you to reuse Bootstrap vars/mixins/etc.
* Integrates SASS and includes Bootstrap via the source SASS files allowing you to reuse Bootstrap vars/mixins/etc.
* Easily Testable - Each sub-generator creates a skeleton unit test.  Unit tests can be run via `gulp test:unit` and they run automatically during the gulp watch that is active during `gulp serve`.

Directory Layout
-------------
All subgenerators prompt the user to specify where to save the new files.  Thus you can create any directory structure you desire, including nesting.  The generator will create a handful of files in the root of your project including `index.html`, `app.js`, and `app.styl`.  You determine how the rest of the project will be structured.

In this example, the user has chosen to group the app into an `admin` folder, a `search` folder, and a `service` folder.


    app.styl ........................... main app-wide styles
    app.js ............................. angular module initialization and route setup
    index.html ......................... main HTML file
    gulfile.js ......................... Gulp build file
    /app ............................... Root Application
      /modules ......................... Main folder for modularizerd app
        /admin ......................... example admin module folder
          admin.js ..................... admin module initialization and route setup
          admin.styl ................... admin module STYLUS
          /admin-directive1 ............ angular directives folder
            admin-directive1.js ........ example simple directive
            admin-directive1-spec.js.... example simple directive unit test
          /admin-directive2 ............ example complex directive (contains external partial)
            admin-directive2.js ........ complex directive javascript
            admin-directive2.html ...... complex directive partial
            admin-directive2.styl ...... complex directive STYLUS
            admin-directive2-spec.js ... complex directive unit test
          /admin-partial ............... example partial
            admin-partial.html ......... example partial html
            admin-partial.js ........... example partial controller
            admin-partial.styl ......... example partial STYLUS
            admin-partial-spec.js ...... example partial unit test
        /search ........................ example search component folder
          my-filter.js ................. example filter
          my-filter-spec.js ............ example filter unit test
          /search-partial .............. example partial
            search-partial.html ........ example partial html
            search-partial.js .......... example partial controller
            search-partial.styl ........ example partial STYLUS
            search-partial-spec.js ..... example partial unit test
        /service ....................... angular services folder
            my-service.js .............. example service
            my-service-spec.js ......... example service unit test
            my-service2.js ............. example service
            my-service2-spec.js ........ example service unit test
      /test ............................ test e2e and results
        /e2e ........................... test folder
      /vendor .......................... 3rd party libraries managed by bower
      /assets .......................... contains images (not created by default but included in /dist if added) and other resources
    /build .............................
      /dist ............................ folder where entire app packed is profived
      /tmp ............................. temp folder used for templtates.js and sass -> css file
      build.config.js .................. config file for gulp building process
      karma.config.js .................. config file for gulp unit test process
      protractor.config.js ............. config file for gulp e2e test process
    /node_modules ...................... npm managed libraries used by gulp


Getting Started
-------------

Prerequisites: Node, Yeoman, Gulp and Bower.  Once Node is installed, do:

    npm install -g yo bower gulp

Clone repo and npm link for install this generator:

    git clone https://github.com/CarlosOV/generator-go-gas.git
    cd generator-go-gas
    npm link o sudo npm link

To create a project:

    mkdir MyNewAwesomeApp
    cd MyNewAwesomeApp
    yo go-gas

Gulp Tasks
-------------

A description of every available task:

* **gulp serve** - When this task runs, the build will take care of watching filea. Every time you change a file into the `app/` folder, the build recompiles every file, and your browser will reload automagically showing you changes.
You just need to add new JavaScript and css files in the `app/index.html` file.
* **gulp serve:dist** - This task will run jshint and unit tests under the `app/test/unit` folder (thanks to `karma runner`), and create a fully-optimized version of your application under the `build/dist/` folder. The optimization consists of concatenate, minify and compress js and css files, optimize images, and put every template into a js file loaded by the application.
A code coverage report will be available inside the `app/test/unit-results`.
* **gulp serve:tdd** - Just like `gulp serve` but in continuous unit testing environment.
* **gulp test:unit** - For running unit tests one time then exit.
* **gulp test:e2e** - Run end-to-end tests inside the `app/test/e2e` folder with `protractor`. If a test fails, you should find a screenshot of the page inside the `app/test/screenshots` folder.
**Note that you need to have the application running in order to run e2e tests. You can launch this task from another terminal instance.**


Yeoman Subgenerators
-------------

There are a set of subgenerators to initialize empty Angular components.  Each of these generators will:

* Create one or more skeleton files (javascript, SASS, html, spec etc) for the component type.
* Update index.html and add the necessary `script` tags.
* Update app.less and add the @import as needed.
* For partials, update the app.js, adding the necessary route call if a route was entered in the generator prompts.

There are generators for `directive`,`partial`,`service`, `filter`, `module`, and `modal`.

Running a generator:

    yo go-gas:directive my-awesome-directive
    yo go-gas:partial my-partial
    yo go-gas:service my-service
    yo go-gas:filter my-filter
    yo go-gas:module my-module
    yo go-gas:modal my-modal
    yo go-gas:architecture  (file containing architecture has to be done)

The name paramater passed (i.e. 'my-awesome-directive') will be used as the file names.  The generators will derive appropriate class names from this parameter (ex. 'my-awesome-directive' will convert to a class name of 'MyAwesomeDirective').  Each sub-generator will ask for the folder in which to create the new skeleton files.  You may override the default folder for each sub-generator in the `.yo-rc.json` file.

The modal subgenerator is a convenient shortcut to create partials that work as modals for Bootstrap v3.1 and Angular-UI-Bootstrap v0.10 (both come preconfigured with this generator).  If you choose not to use either of these libraries, simply don't use the modal subgenerator.

Subgenerators are also customizable.  Please read [CUSTOMIZING.md](CUSTOMIZING.md) for details.

Architecture
-------------
With sub generators yo go-gas:architecture you can generate the first stub architecture through a simple json file that describe the entire application.
In this way is possible to startup more faster your app.

Following this simple steps:
```
    $ mkdir MyNewAwesomeApp
    $ yo go-gas ..............    creates the entire application scafolds  [this generator is optimized for Angular UI Router]
    $ touch architecture.json
        Example code:             cat and past json first draft into the file
        {   "appname": "scloby",
            "modules": [
                { "name": "module1",
                  "partials": [
                                { "name": "partial1" }
                              ],
                  "services": [
                                { "name": "service1" }                    
                              ],
                  "filters":  [
                                { "name": "filter1" }
                              ],
                  "directives": [
                                { "name": "directive1",
                                  "needpartial": true
                                }                    
                              ],
                  "modals": [
                                {"name": "modal1"}
                            ]
                },
                { "name": "module2",
                  "partials": [
                                {"name": "partial1"}
                              ],
                  "services": [
                                {"name": "service1"},
                                {"name": "service2"}
                              ]       
                }
          ]
        }
    $ yo go-gas:architecture    scaffold your app
```
This will create the first architecture structure.
NOTE: becareful, when you start to code, is possible that if you run this subgenerator your code will be replaced with a new empty stub.


Submodules
-------------

Submodules allow you to more explicitly separate parts of your application.  Use the `yo go-gas:module my-module` command and specify a new subdirectory to place the module into.  Once you've created a submodule, running other subgenerators will now prompt you to select the module in which to place the new component.

Preconfigured Libraries
-------------

The new app will have a handful of preconfigured libraries included. This includes Angular 1.3, Bootstrap 3, AngularUI Bootstrap, AngularUI Utils, FontAwesome 4, JQuery 2, Underscore 1.5, and Moment 2.5.  You may of course add to or remove any of these libraries.  But the work to integrate them into the app and into the build process has already been done for you.

Build Process
-------------

The project will include a ready-made Gulp build that will:

* Build all the STYLUS files into one minified CSS file.
* Uses [gulp-html2js](https://github.com/fraserxu/gulp-html2js) to turn all your partials into Javascript.
don't have to use the array syntax.
* Concatenates and minifies all Javascript into one file.
* Replaces all appropriate script references in `index.html` with the minified CSS and JS files.
* Minifies any images in `/build/dist/assets/images`.
* Minifies the `index.html`.
* Copies any extra files necessary for a distributable build (ex.  Font-Awesome font files, etc).

The resulting build loads only a few highly compressed files.


Release History
-------------
* 20/11/2016 - Migrate project to STYLUS.
