## Browser Prefixes

Browsers are now implementing new CSS properties almost daily, but most of them remain in experimental stage for a long time, and we need to use browser prefixes in our CSS / SCSS code to use those properties. These prefixes like -webkit-, -moz-, -ms-, etc. makes the code dirty and sometime they are painful to add (CSS3 gradient is one example of complexity of code with use of browser prefixes)

Fortunately, we have JavaScript libraries called autoprefixer, they help us keep the CSS code clean, and they do the dirty task of adding browser prefixes where required.

We are going to use gulp-autoprefixer, main benefit of this package is that we are not adding any additional JavaScript code to our webpage. We will pipe this package within sass task, so it will add prefixes where needed in our CSS code, and we do not need to add them in our SCSS code.

We have already created a reference variable for this package named ‘autoprefixer’, so let’s see how to use it.

Following is the updated sass task, with autoprefixer added in it:

```
gulp.task('sass', function(){
  return sass('source/scss', {
                              sourcemap: true
                            })
    .pipe(autoprefixer('last 3 versions'))
    .pipe(gulpif(env === 'development', sourcemaps.write('../maps')))
    .on('error', sass.logError)
    .pipe(gulp.dest(outputDir + '/css'));
});
```

You will notice that i have used ‘last 3 versions’ as parameter in autoprefixer, this means we are telling autoprefixer to make our CSS code compatible with last 3 versions of all major browsers.

Autoprefixer uses [Browserlist](https://github.com/ai/browserslist), i suggest you to read documentation of Browserlist once, to understand what other options are available. You can make lots of different queries to match your requirements.

Here are few examples if queries you can use with autoprefixer:

**last 2 versions:** the last 2 versions for each major browser.  
**last 2 Chrome versions:** the last 2 versions of Chrome browser.  
**\> 5%:** versions selected by global usage statistics.  
**\> 5% in US:** uses USA usage statistics. It accepts two-letter country code.  
**ie 6-8:** selects an inclusive range of versions.  
**Firefox > 20:** versions of Firefox newer than 20.  
**Firefox >= 20:** versions of Firefox newer than or equal to 20.  
**Firefox < 20:** versions of Firefox less than 20.  
**Firefox <= 20:** versions of Firefox less than or equal to 20.  
**Firefox ESR:** the latest [Firefox ESR] version.  
**iOS 7:** the iOS browser version 7 directly.  
**not ie <= 8:** exclude browsers selected before by this query. You can add not to any query.  

Following is an example of autoprefixer with specific browser versions, this will ensure that CSS file have support for these browser versions mentioned

```.pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))```

Try to make few queries of your own, see how this makes an impact on CSS3 properties in your CSS file.