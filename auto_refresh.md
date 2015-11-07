## Auto Refresh

By now we have added multiple things to ‘sass’ task. We have converted our SCSS files to CSS files, added autoprefixer, created map files, and compressed CSS code. But during development process, after i make any small change in SCSS code, i will need to refresh my browser to see those changes. How about adding an auto refresh to our task?

For this process we are going to use gulp-connect package, we have used previously. To recall we added livereload:true in our ‘serve’ task. livereload allow us to refresh browser automatically when any file is changed.

we just need to pipe the new command ```.pipe(connect.reload());```

Following is the final code of our ‘**sass**’ task:

```
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