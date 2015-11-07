# Adding Packages

Now we need to add few packages that are required by gulp for certain tasks. We are going to add them to package.json file as dependencies.

As mentioned earlier, packages are small javascript libraries, developed by many developers worldwide. We can use multiple packages with gulp, each package will help us perform a certain task (or set of tasks).

All packages will be installed in your working folder within node_modules folder. One major benefit of using npm is that you don’t need to distribute node_modules folder with your project. Every user can have his own copy of node_modules folder. 

NPM can find list of dependencies from package.json folder and download and install all required packages automatically. (Reffer to section “Distributing your project” for details)

(Note: we are going to add things as devDependencies, because we only need them during development process.)

Let’s start adding devDependencies from command prompt.

```npm install --save-dev gulp```

This command will do following tasks:
1. It will add gulp as developer dependency in package.json file
2. It will create a *node_modules* folder (if it do not exist), and will download gulp package inside *node_modules* folder

We will keep installing other packages as required.

Now lets create a file named ```gulpfile.js``` in root directory of our project.  

in ```gulpfile.js``` add following code to get started:

```
var gulp = require('gulp');

gulp.task('default', function() {
  // place code for your default task here
});

```

First line of this code tells node.js that this script requires gulp library, and we are creating a reference to gulp library in a variable named gulp.

gulp have a ‘task’ method inbuilt, we will use ‘task’ method to create different tasks for gulp (as required). Here default is name of task or function.

Now to understand the process little better, let’s install a utility library named [gulp-util](https://github.com/gulpjs/gulp-util), and use it in our gulp file (gulpfile.js)

First we need to go back to terminal or command prompt, make sure you are in working directory.

Then execute following command:

```npm install --save-dev gulp-util```


As we saw previously, this will download required files in node_modules folder, and will also add gulp-util library in package.json file as developer dependency. 

Next let’s update code in our gulp file (gulpfile.js) as following:

```
var gulp = require('gulp'),
    gutil = require('gulp-util');

gulp.task('default', function() {
  gutil.log('Hello World!');
});

```

Here, I have added a reference to gulp-util library in gutil variable. then i have used this variable in gulp task (function) to log/print a message.

Now we are ready to test our gulp file.

Go to command prompt and type ```gulp```, hit enter. You will see gutil.log will execute and “Hello World!” will be displayed on command prompt. 

For any other task (except from default) you need to add task name in command, so it will be ```gulp task_name``` to execute that task.

This is how gulp works. Next we will add some useful tasks to gulp that can help us automate some tasks.
