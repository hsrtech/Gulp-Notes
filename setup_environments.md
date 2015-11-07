# Development and Production Environments

In most of the cases, we need to make 2 versions of our website, development version usually have uncompressed files for easy readability, few files for debugging (usually map files), and maybe few other things that can help you during development.

On the other side on Project environment, we need everything compressed to improve load speed, and remove any debugging related files or information.

So let us setup our gulpfile in a way so that we can instruct gulp to build files differently for both development and production environments.  

For this we are going to use [yargs](https://www.npmjs.com/package/yargs) package. 

Install yargs as developer dependency:  
```npm install --save-dev yargs```

Add a variable in gulpfile.js to create a reference to yargs package.   
```var argv = require('yargs').argv;```

yargs allow us to pass parameters to gulp tasks, we can use these parameters according to our requirement. 

In our case we will use ```--production``` to instruct gulp that we want to use production environment.


Next create a variable to store name of environment  
```var env = argv.production ? 'production' : 'development';```

Here we are using a conditional (ternary) operator to check if ```--production``` is passed as an parameter, value of env will be production, otherwise it will be development. So development will be our default environment.

Let’s update the default task that we created previously to test this.

```
gulp.task('default', function() {
  console.log(gutil.colors.green('Environment: ' + env));
});
```

This will print the value of env variable on command prompt.

gutil.colors.green will change color of output to green, this will help us in distinguishing the output from other commands. You can use any color of your choice. 

Save the file, and try following commands:

``` gulp ```

   
```gulp --production ```


You will see different values of environment variable as output.

Now we have two different commands ready to differentiate between development and production environments. 

As the last step if this task, let’s create one more variables for later use.

```var outputDir = 'builds/' + env;```

To understand use of this variable, take a look at the folder structure we will be using for this project:

```
Project
  |- package.json
  |- gulpfile.js
  |- sources
  |- builds
    |-- development
    |-- production
```

So far we have created package.json and gulpfile.js files in our project folder. We will use ‘sources’ folder to store all our source files. Gulp will automatically build other 3 folders for us. 

‘builds/development’ folder will be used to store files for development environment. and ‘builds/production’ folder will be used to store files for production environment.

If you are using GIT, you can add /builds folder in .gitignore file. You do not need to share these folders because other developers will be able to recreate these folders with help of gulp commands.

Here’s the complete code we have created so far:

```
var gulp = require('gulp'),
    gutil = require('gulp-util'),
    argv = require('yargs').argv;

var env = argv.production ? 'production' : 'development';
var outputDir = 'builds/' + env;

gulp.task('default', function() {
  console.log(gutil.colors.green('Environment: ' + env));
});
```

For the next parts of this guide, you will need some files for practice. 
If you do not have your own files, you can download a copy of my code from here:   
~~[path of git repository to be added]~~
