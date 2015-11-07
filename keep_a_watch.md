# Keep a Watch

In the previous chapter We have created a task for processing our CSS files, but there is one major issue. Every time we need to make a change in SCSS files, we need to go to command prompt and execute ```gulp sass``` command to process our changes. 

Gulp have a special task named ‘**watch**’, this task is used to keep a watch on certain files (that we ask this task to watch), and whenever we make any change in file and save it, watch task will execute the task associated with that file.

For example we can tell ‘watch’ task to keep a watch on our SCSS folder, and whenever we change any file in that folder, it will execute the task ‘sass’, that we created previously.

Here’s our watch task, we are telling it to keep a watch on our scss folder, and whenever anything changes, it will execute the ‘sass’ task, that we have created previously.

```
gulp.task('watch', function() {
  gulp.watch('source/scss/**/*.scss', ['sass']);
});
```

** matches all files, folders, and subfolders, this will ensure that watch task in watching all subfolders too, and then we are telling it to look for all files with .scss extension. 

Go to terminal / command prompt and try command ```gulp watch```. Now make some changes in your SCSS files, and save them. As soon you will save your changes, gulp will execute the ‘sass’ task. You can see this on command prompt. And because we have added livereload for refreshing the browser automatically, your changes will reflect in browser too.

*Note: You will need to use Ctrl + C to terminate the watch task.*

We can improve the process further by adding ‘watch’ task to ‘default’ task. So we will only need to use command gulp. 

Gulp will execute the ‘serve’, and ‘sass’ tasks once, and then execute the ‘watch’ task to keep watching for any changes.

Following is the updated code for default task, after adding both ‘sass’, and ‘watch’ tasks to it.

```
gulp.task('default', ['serve', 'sass', 'watch'], function() {
  console.log(gutil.colors.green('Environment: ' + env));
});
```

Now you can use commands ```gulp``` or ```gulp --production``` to execute all tasks we have created so far.

Following is the complete code for your reference:

```
var gulp = require('gulp'),
    gutil = require('gulp-util'),
    argv = require('yargs').argv,
    connect = require('gulp-connect'),
    sass = require('gulp-ruby-sass'),
    sourcemaps = require('gulp-sourcemaps'),
    autoprefixer = require('gulp-autoprefixer'),
    gulpif = require('gulp-if');;

var env = argv.production ? 'production' : 'development';
var sassStyle = argv.production ? 'compressed' : 'expanded';
var outputDir = 'builds/' + env;

gulp.task('default', ['serve', 'sass', 'watch'], function() {
  console.log(gutil.colors.green('Environment: ' + env));
});

gulp.task('watch', function() {
  gulp.watch('source/scss/**/*.scss', ['sass']);
});

gulp.task('serve', function() {
  connect.server({
    root: outputDir,
    livereload: true,
    port: 4567
  });
});

gulp.task('sass', function(){
  return sass('source/scss', {
                              sourcemap: true,
                              style: sassStyle
                            })
    .pipe(autoprefixer('last 3 versions'))
    .pipe(gulpif(env === 'development', sourcemaps.write('../maps')))
    .on('error', sass.logError)
    .pipe(gulp.dest(outputDir + '/css'))
    .pipe(connect.reload());
});

```

