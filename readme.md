##A [Generator-Angular-Fullstack](https://github.com/DaftMonk/generator-angular-fullstack) written by Tong Xiang for the students of Fullstack Academy. 

##INTRODUCTION 
So you’re now beginning to understand and master Mongo, Express, Angular, and Node. But instead of hacking together all these components before beginning the real work on your app, why not use a time-saving generator? Generators are either applications you can install which include a command-line tool that automatically creates the bare bones of a app (think of how we can use the `express newappname` command), or a public repo we can clone. 

Today, we’ll walk through how to install one of my favorite MEAN generators--[*Generator-Angular-Fullstack*](https://github.com/DaftMonk/generator-angular-fullstack)--which has been built on top of [Yeoman’s Angular generator](https://github.com/yeoman/generator-angular) by [Tyler Henkel](https://github.com/DaftMonk). You may have used the Yeoman Angular generator in the past; this version adds an Express backend with a MongoDB database. 

###INSTALLATION###

First, install the generator application: 

{% terminal %}
$ npm install -g generator-angular-fullstack
{% endterminal %}

Next, we need to check to make sure that things install properly. 

###RUBY PREREQUISITES###
While the generator runs on Express, there are certain components of the generator (Compass, which facilitates a lot of the built-in SASS functionality) which run on Ruby. Let’s make sure 1) that we have Ruby installed, 2) that our Ruby Gems (the Ruby gem package manager, like Node package manager) is updated, and 3) that the Compass gem installed. 

To check if Ruby is installed: 
{% terminal %}
$ ruby -v
{% endterminal %}

Make sure you’re in the directory of the generated application, and run the following command to determine where our gem-system is located: 
{% terminal %}
$ which gem
{% endterminal %}

If the version of Gems is located a directory with a filepath that’s something like `/Users/tong/.rvm/rubies/ruby-2.0.0-p353/bin/gem`, then we know that we’re running our **self-installed** version of Ruby and Gems with this app. In this case, run: 

{% terminal %}
$ gem update
{% endterminal %}

If we see a filepath that’s something like `/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby, we know that we’re running the version that comes with OSX. In this case, run: 

{% terminal %}
$ gem update --system 
{% endterminal %}

###INITIALIZING AN INSTANCE OF YOUR APP

After running the previous checks, now we can initialize an instance of the generator. Make a new directory titled with the name of your app, and enter that directory. 

{% terminal %}
$ mkdir new-mean-project
$ new-mean-project
{% endterminal %}

Run `yo angular-fullstack`, optionally passing in the name of your app. 

{% terminal %}
$ yo angular-fullstack new-mean-project
{% endterminal %}

The generator then asks you six configuration questions, which you can answer by pressing ‘Y’ or ‘N’ and then enter. 

*The first question* asks you whether you’d like to use [SASS](http://sass-lang.com/)--a CSS extension language--to pre-format your stylesheets. If you’ve never played around with SASS before, it’s pretty useful, allowing to use CSS as a programming language, among many other functions. *If you’ve never used SASS before and want to be productive quickly (i.e., without learning how to use SASS), I wouldn’t select this option.*

{% terminal %}
1. Would you like to use Sass (with Compass)? 
{% endterminal %}

*The second question* asks you whether you’d like to include [Bootstrap](http://getbootstrap.com/2.3.2/), a super commonly-used front-end framework. All Fullstack students should’ve already used Bootstrap before, and it’s a good idea to include it to get more productive quickly. Even if you haven’t used Bootstrap’s grid layout system before, it’s easy to pick up quickly. *I’d select this option.*

{% terminal %}
$ gem update --system 
{% endterminal %}
2. Would you like to include Twitter Bootstrap?

*The third question* asks if you’d like to use the version of Bootstrap configured for SASS--i.e., using versions of Bootstrap’s CSS files that have been configured for SASS. *Select if you’ve already selected the first two options, don’t select if you didn’t select either one.*

{% terminal %}
3. Would you like to use the SASS version of Twitter Bootstrap? 
{% endterminal %}

*The fourth question* toggles the inclusion of four different Angular services: [$resource](https://docs.angularjs.org/api/ngResource/service/$resource), a factory which creates a resource object that lets you interact with RESTful server-side data sources; [$cookies](https://docs.angularjs.org/api/ngCookies/service/$cookies, which provides read and write access to a client’s cookies; [$sanitize](https://docs.angularjs.org/api/ngSanitize/service/$sanitize), a service which sanitizes HTML you pass into it from malicious code; and [$route](https://docs.angularjs.org/api/ngRoute/service/$route), used as a reference to the to the current route definition.

For your projects, I’d recommend *including all these services*, even if you’re uncertain whether or not you’re going to use them. (As you become more and more comfortable with Angular, you’ll begin to see more use-cases for these services. $resource, in particular, is **very** useful as a means of interacting with a server-side data store through your Angular controllers.) When you include the services in your install, not only are theyincluded in your bower install, they’re also automatically placed in your index.html footer scripts as well as injected as a dependency with app-level angular module in `app/scripts/app.js`. 

{% terminal %}
4. Which modules would you like to use? (Use arrow keys, then spacebar to select/de-select options)
    *angular-resource.js
    *angular-cookies.js
    *angular-sanitize.js
    *angular-route.js
{% endterminal %}

*The fifth question* asks if you’d like to “include MongoDB with Mongoose.” If you answer yes to this question, you’re not just installing Mongoose, but you’re also installing also Connect-Mongo (a library which facilitates the Express connection with MongoDB), as well as including a lot of boilerplate MongoDB connection code--initializing your MongoDB database, creating dummy Mongoose models. Unless your project doesn’t require a database, or you plan on using another type of database, I’d *always select this option.* 

{% terminal %}
5. Would you like to include MongoDB with Mongoose?
{% endterminal %}

Toggling *the final question* allows you to include not only the standard Passport npm modules, but also Passport authentication boilerplate code which sets up a pretty standard CRUD app behind a wall of authentication. *If you’re going to use authentication with your app, I’d select this option, but not otherwise.* (Check out [Fullstack’s Passport.js workshop](https://github.com/FullstackAcademy/privatewikistack) to get a refresher about what’s going on under the hood here.)  

{% terminal %}
6. Would you like to include a Passport authentication boilerplate?
{% endterminal %}

Once all your options are configured, the generator automatically runs the `npm install` and `bower install` commands. 

##WHAT NPM AND BOWER MODULES ARE ALWAYS INCLUDED? 

###LAUNCHING YOUR SERVER

There are three different ways we can launch our server. Note that each of the grunt commands automatically opens a new browser window at the correct port. To launch your server in development mode: 

{% terminal %}
$ grunt serve
{% endterminal %}

During development mode, [*LiveReload*](http://livereload.com/) will be running. This automatically watches all file types in both your `app` and `lib` directories, and will restart your Express server when a change is detected. 

To launch in debugging mode, which runs node-inspector, use the following command. ([Here’s](http://howtonode.org/debugging-with-node-inspector) a good introduction to the use-cases of node inspector, and [here’s](https://github.com/node-inspector/node-inspector) its documentation. 

{% terminal %}
grunt serve:debug
{% endterminal %}

To launch your server in production mode, which automatically generates a `dist file with a minified version of your app and runs your app from that folder, run the following command: 

{% terminal %}
grunt serve:dist
{% endterminal %}


##SERVER-SIDE

##CLIENT-SIDE 


##FRONTEND: YEOMAN ANGULAR GENERATORS
Yeoman’s Angular generator provides us with a quite a few useful command line commands which automatically generate various Angular components. 

Note that: 

1. The prefix for these commands have been changed from generator-angular’s `angular` to `angular-fullstack` with generator-angular-fullstack. 

2. *The generator commands should be run from the root directory of your app.*

3. These commands generate **not only** the Angular components themselves, but **also** attendant testing files in the `/test` directory.

4. If the command generates a script file--such as `yo angular-fullstack:controller controllerName`--the script is automatically included in the end of the <body> tag in the main view’s `app/views/index.html` html page. Pretty convenient, right? 

The commands are below, and here’s a [link to their documentation](https://github.com/yeoman/generator-angular#controller). 
* angular-fullstack:controller
* angular-fullstack:directive
* angular-fullstack:filter
* angular-fullstack:route
* angular-fullstack:service
* angular-fullstack:provider
* angular-fullstack:factory
* angular-fullstack:value
* angular-fullstack:constant
* angular-fullstack:decorator
* angular-fullstack:view

##GENERATOR OPTIONS
It’s unlikely that you’ll use the following options with your first apps, but the following commands will be helpful to know in the future if you decide to use Coffeescript or Jade

###CONFIGURE GENERATORS TO PRODUCE VIEWS IN JADE
The angular-fullstack generators that generate views--(for instance, using the `yo angular-fullstack:view yourViewName` command)--can be given an optional argument to generate those views with Jade. The following command will change your app’s rendering engine from EJS to Jade, and will generate your views as Jade files instead of HTML. 

Assets that will be minified or compressed--scripts, styles, images--still need to  use normal html tags so they can be read into the `grunt-usemin` service and compressed. 

###CONFIGURE GENERATORS TO PRODUCE SCRIPTS IN COFFEESCRIPT
Those angular-fullstack generators that generate scripts--for instance, `yo angular-fullstack:controller yourControllerName`--can be given an optional argument to output those scripts in CoffeeScript instead of Javascript. 

For example, running the following command: 

{% terminal %}
$ yo angular-fullstack:controller user --coffee
{% endterminal %}

Produces a new controller at `app/scripts/controller/user.coffee` with the following code: 

```javascript
'use strict'

angular.module('tongTestApp')
  .controller 'CoffeescriptcontrollerCtrl', ($scope, $http) ->
    $http.get('/api/awesomeThings').success (awesomeThings) ->
      $scope.awesomeThings = awesomeThings

```

##TESTING 

##HEROKU DEPLOYMENT
While the generator can easily deploy to either Openshift or Heroku, we’ll cover their simple Heroku deployment here. To push your app up to Heroku, run: 

{% terminal %}
$ yo angular-fullstack:heroku
{% endterminal %}

This single command compress four different tasks (the attendant commands for those tasks in parentheses): 

1. It builds a dist folder which contains the minified version of your app (`grunt build`)
2. It creates a Procfile in the dist folder--the Procfile is a mechanism for declaring what commands are run by your application’s dynos in the Heroku platform. For instance, for our node application, the Procfile specifies that the command to run our server would just be `web: server.js`. 
3. It creates a repository (git init && git add -A && git commit -m "Initial commit"`
4. Finally, it creates a heroku app (heroku apps:create && heroku config:set NODE_ENV=production)

###HOW DOES THIS HEROKU PUSH WORK?

If you’ve installed the [Heroku Toolbelt](https://toolbelt.heroku.com/) to your machine, the install has also included the [Heroku client](https://devcenter.heroku.com/articles/heroku-command), a command line interface tool that allows you to 1) authenticate your machine as being linked to your Heroku account, and 2) push apps up to Heroku deployments from your local repositories. 

TIP: Your Heroku CLI is authenticated to your remote account in your .heroku directory in your home directory. To check out your .heroku directory, and then the authentication file, input the following in your terminal: 

{% terminal %}
$ cd ~/.heroku
$ subl ./client/data/cacert.pem
{% endterminal %}

###PUSHING UPDATES TO HEROKU
When you’re ready to ship changes to your live app, run the following command to 1) generate a new build (version of your app) for deployment. Remember, this build is located in your `dist` directory. 

{% terminal %}
$ yo angular-fullstack:heroku
{% endterminal %}

You can then 1) enter that directory, 2) push the new build to git, and 3) push the new build to Heroku. 

{% terminal %}
$ cd dist
$ git push yourAppName master
$ git push heroku master
{% endterminal %}

QUESTIONS FOR NIMIT OR DAVID
What exactly does the running the app in production mode with `grunt serve:dist` do? 
what processes are run to create the dist file, aside from minification? 
it’s about keeping your code more obfuscated, so it’s harder to reverse-engineer. 10% of it. 
90% of it is about how quickly the browser loads files. But it’s way better to download a 100k file, then 10 10k files. 
Collapsing all front-end scripts into one file. 
Heroku deployment commands not working >>> is something missing? 
https://devcenter.heroku.com/articles/git

##COMPILATION OF OTHER MEAN GENERATORS / BOILERPLATES
As you gain more experience with the MEAN stack, you’ll begin to appreciate the need for additional functionality in your generator. Feel free to check out and use the following generators; I’ve put together a bit of information to help you compare and contrast them: 

mean.io - http://mean.io/#!/ 
(4,240 stars, 1,287 forks) 
https://github.com/linnovate/mean
last commit May 23rd, 2014; heavily updated
very heavy, uses a complex module-generating system
yeoman/generator-angular - https://github.com/yeoman/generator-angular 
(1785 stars, 828 forks) 
doesn’t have mongoose, you need to install mongo yourself
isn’t running express  
last commit May 16th, 2014 
generator-angular-fullstack: https://github.com/DaftMonk/generator-angular-fullstack
1109 stars, 828 forks 
sample app code: https://github.com/DaftMonk/fullstack-demo
advantages if you deploy to heroku--yo angular-fullstack:deploy heroku generates a dist folder that is deployment ready for heroku.com 
mean.js - https://github.com/meanjs/mean 
(445 stars, 83 forks)
latest commit May 9th, 2014 
generator-mean - https://github.com/jrcryer/generator-mean
83 stars, 15 forks 
last commit April 29th, 2014, 32 commits, 1 branch, 4 contributors 
angular express seed - https://github.com/btford/angular-express-seed
921 stars, 373 forks 
last commit March 2nd, 2014, 
doesn’t include Mongoose 
tutorial on how to use it to build a blog: http://briantford.com/blog/angular-express.html

##ACKNOWLEDGMENTS
Thanks to [Tyler Henkel](https://github.com/DaftMonk) for his extensive documentation of the Angular Fullstack generator--a good portion fo this walkthrough is lifted from his [README](https://github.com/DaftMonk/generator-angular-fullstack/blob/master/readme.md). 
