# Server and autorefresh

Sometime you need a server (localhost) to perform certain tasks, for example if you are use fonts from typekit.com, they will not load until your files are on a server.

Let’s prepare our project to work on localhost. You can do this using gulp.

For this task we are going to use gulp-connect package. 

First 2 steps are same for most of the tasks.

Install gulp-connect as developer dependency:   
```npm install --save-dev gulp-connect```

Add a variable in gulpfile.js to create a reference to this package.   
```var connect = require(‘gulp-connect’);```

Now let’s add a new task

```
gulp.task('serve', function() {
  connect.server();
});
```

You can use command ```gulp serve``` to execute this task

This will show you a message like *Server started http://localhost:8080* on command prompt. 
you can use URL http://localhost:8080 for your project now.

You need to use ```Ctrl + C``` to stop server when needed.

But till now, this task do not know anything about which files to display in browser, by default it's trying to display files from root folder of project.

We can simply add a root parameter to provide path of desired folder.

```
gulp.task('serve', function() {
  connect.server({
    root: outputDir
  });
});
```

In the above code, we have added a root parameter, and variable outputDir as its value, This will show results in browser depending on the environment we are working on. (we have discussed about environment in a previous section).


*Note: because we have not created builds folder yet, there will be no output in browser. You will get a message “Cannot GET /”, this means that gulp-connect is not able to find the folder we have mentioned.*

*Alternatively you can add files manually to /builds/production/ and /build/development/ folders for testing of various tasks. You can delete build folder once your gulp file is ready, to make sure that gulp is doing all tasks properly, as expected.*

Next, let us add 2 more parameters to our task:

1. port: this allow us to change port from 8080 to anything we want. Some other applications may already be using port 8080, so we can change it easily with port parameter, and provide our own port number.
2. livereload: this parameter will allow us to refresh browser automatically when any file is changed.

Following is the updated code with both parameters added to it:


```
gulp.task('serve', function() {
  connect.server({
    root: outputDir,
    livereload: true,
    port: 4567
  });
});
```

We have changed port to 4567, so our URL to preview project files will change to:  http://localhost:4567 

Our task is ready and working as expected, but let’s append this task to default task, so that we do not need to run it separately.   

Updated default task:

```
gulp.task('default', ['serve'], function() {
  console.log(gutil.colors.green('Environment: ' + env));
});
```

We can add  an array of task names to default task, now when you execute ```gulp``` or ```gulp --production``` serve task will also be executed.

Following is the final code we have so far:

```
var gulp = require('gulp'),
    gutil = require('gulp-util'),
    argv = require('yargs').argv,
    connect = require('gulp-connect');

var env = argv.production ? 'production' : 'development';
var outputDir = 'builds/' + env;

gulp.task('default', ['serve'], function() {
  console.log(gutil.colors.green('Environment: ' + env));
});

gulp.task('serve', function() {
  connect.server({
    root: outputDir,
    livereload: true,
    port: 4567
  });
});
```
