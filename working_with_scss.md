# SCSS Compilation, Autoprefixer, and CSS Compression

SASS / SCSS (Also known as Sassy CSS), is one of the most commonly used library for extending CSS code. It adds lots of power to normal CSS. But you need a compiler to convert SCSS files to normal CSS files. Gulp can handle this compilation part for you, and can also provide few additional features

First requirement of using SCSS is that you have SASS installed on your computer.

You can find instructions to install SASS here: http://sass-lang.com/install
(On Windows you will also need to install [ruby](http://rubyonrails.org/) to use SCSS, on Mac Ruby is pre installed)

We are going to use a bunch of packages for this task, following is the list of packages we require:

* [gulp-ruby-sass](https://www.npmjs.com/package/gulp-ruby-sass)
* [gulp-sourcemaps](https://www.npmjs.com/package/gulp-sourcemaps)
* [gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer)  
* [gulp-if](https://www.npmjs.com/package/gulp-if)

Use following command to install all required packages:  
```npm install --save-dev gulp-ruby-sass gulp-sourcemaps gulp-autoprefixer gulp-if```

Next, create variables to add reference of each of these packages:

```
var sass = require('gulp-ruby-sass'),
    sourcemaps = require('gulp-sourcemaps'),
    autoprefixer = require('gulp-autoprefixer'),
    gulpif = require('gulp-if');
```

We are going to create a separate task for handling SCSS files. Let’s name this task ‘sass’ for easy identification.

we need source path and destination part for this task. Source path is path of your SCSS files. In my case its ‘source/scss’, and destination path will be where you want to save your CSS files after they are compiled. 

Because we have 2 different destination folders for development, and production environments, we are using variable outputDir, we have stored path of our output directory in this variable previously. I am concatenating path of a sub folder named ‘css’ to store my CSS files. 

Following is the code for task, it will take files from source folder and will save them in destination folder after compilation. Also it will log errors, if there is any error in your sass files.

```
gulp.task('sass', function(){
  return sass('source/scss')
    .on('error', sass.logError)
    .pipe(gulp.dest(outputDir + '/css'));
});
```

So far this task is very simple, but we can do a lot more with this task.




