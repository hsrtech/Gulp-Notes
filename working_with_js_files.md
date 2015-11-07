# Concatenate and Compress JavaScript files

We normally use multiple JavaScript files in a website, for different tasks. For example, jQuery, Carousel, form validation, etc. 

When we link these files individually, browser makes a request for each individual file to server. Computers are not smart enough to respond to all these calls at one time, they handle them one by one in a que. As a result this slows down your website’s load time. 

Easiest solution of this issue is to concatenate all your JavaScript files in a single file, so that browser get all data in one call/request to server. 

Also it's always to good idea to compress the JavaScript file to reduce the file size. Smaller files will load fast.

Let’s see how we can utilize Gulp for concatenation and compression of JavaScript files. 

