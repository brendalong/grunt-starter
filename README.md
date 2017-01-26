# Task Runner Starter - Grunt
 
Create a lib folder

cd into the lib folder

## Start From Scratch
**`npm init`** - walk through the steps for creating a basic package.json file

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

**Common packages for projects include:**
* `npm install grunt --save-dev`
* `npm install jshint --save-dev`
* `npm install grunt-contrib-jshint --save-dev`
* `npm install jshint-stylish --save-dev`
* `npm install grunt-contrib-watch --save-dev`
* `npm install grunt-contrib-sass --save-dev`
* `npm install matchdep --save-dev`

After each install - your package.json file will update

The grunt install will create a node_modules folder. This will become the location for the other items installed.

**Setup Your Gruntfile.js**

* Setup jshint - location of javascript files
* Setup sass compilation - location of scss and where to put compiled version.
* Setup watch - have grunt run specific tasks when changes occur.

### Sample Gruntfile.js
```javascript
module.exports = function(grunt) {
  grunt.initConfig({
    jshint: {
      files: ['../javascripts/**/*.js'], //location of javascript files
      options: {
        predef: ["document", "console", "$" ], //allows for predefined things not found in js
        esnext: true, //allows for ES6 
        globalstrict: true,
        globals: {"Sandwich":true} //name value pairs, allows to define global vars used in many files.
      }
    },
    sass: { //setup sass compilation
      dist: {
        files: {
          '../css/styles.css': '../sass/styles.scss'
        }
      }
    },
    watch: { //automatically watch for changes
      javascripts: {
        files: ['../javascripts/**/*.js'], 
        tasks: ['jshint']
      },
      sass: {
        files: ['../sass/**/*.scss'],
        tasks: ['sass']
      }
    }
  });

  require('matchdep').filterDev('grunt-*').forEach(grunt.loadNpmTasks);
  grunt.registerTask('default', ['jshint', 'sass', 'watch']);
};

```
## Start From boilerplate
Already have a package.json file and Gruntfile.js
* Run `npm install` - this looks at the package.json file and installs the needed items.
* Run `grunt`


***********************
So, what's up with `"use strict"`
* Disallows global variables. (Catches missing var declarations and typos in variable names)
* Silent failing assignments will throw error in strict mode (assigning NaN = 5;)
* Attempts to delete undeletable properties will throw (delete Object.prototype)
* Requires all property names in an object literal to be unique (var x = {x1: "1", x1: "2"})
* Function parameter names must be unique (function sum (x, x) {...}) 
* Some ES6 features require you to be in strict mode
  
