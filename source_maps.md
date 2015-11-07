## Source maps

When we use SCSS, one most problematic part is debugging. Normally developer tools available in browsers display reference of CSS file. But when we are working with SCSS, we need a way to get reference to SCSS files in developer tools too. Easiest way to make this change is create source maps.

*Note: You may need to enable source maps from settings of your browser’s developer tools section, to be able to use source maps.*

We will use gulp-sourcemaps package to create source maps.

Here’s the code for updated sass task:

```
gulp.task('sass', function(){
  return sass('source/scss', {
                              sourcemap: true
                            })
    .pipe(sourcemaps.write('../maps'))
    .on('error', sass.logError)
    .pipe(gulp.dest(outputDir + '/css'));
});
```

Here we are informing gulp-ruby-sass package that we are going to use sourcemaps, by setting parameter sourcemap to true.

Also we have ```.pipe``` function to write sourcemaps, path of maps folder will be relative to output directory.

.pipe function is used to perform multiple actions in one task. As the name suggests, this functions make a pipe of actions, and gulp execute them one by one.

run the task with command ```gulp sass```, and you will see a new folder named map in build/development folder with .map files.

We still have one issue, we do not need map folder in production environment. We want to keep it clean. For this we have gulp-if available to help us. Let’s add a condition so that map files are generated only if we are in development environment. 

Here’s the updated code:

```
gulp.task('sass', function(){
  return sass('source/scss', { sourcemap: true })
    .pipe(gulpif(env === 'development', sourcemaps.write('../maps')))
    .on('error', sass.logError)
    .pipe(gulp.dest(outputDir + '/css'));
});
```
