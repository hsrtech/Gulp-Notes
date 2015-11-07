## CSS Compression

gulp-ruby-sass package provide us inbuilt options to compress the CSS code. But i want CSS code to be compressed in production environment only. 
Let’s create a new variable named ‘sassStyle’. This variable will hold the style of CSS output we want based on environment. 

We can add a condition to check environment and store a value on sassStyle variable according to result. Following is the code. In this code we are checking if environment is production, sassStyle will be ‘compressed’, otherwise it will be ‘expanded’.

```var sassStyle = argv.production ? 'compressed' : 'expanded';```

Now we need to add a parameter named ‘style’ to our sass function, and value of this style parameter will be our newly created variable sassStyle.

Updated Code:

```
gulp.task('sass', function(){
  return sass('source/scss', {
                              sourcemap: true,
                              style: sassStyle
                            })
    .pipe(autoprefixer('last 3 versions'))
    .pipe(gulpif(env === 'development', sourcemaps.write('../maps')))
    .on('error', sass.logError)
    .pipe(gulp.dest(outputDir + '/css'));
});
```

Run commands ```gulp sass``` and ```gulp sass --production``` to see the difference in output of CSS files in both development and production folders. 


