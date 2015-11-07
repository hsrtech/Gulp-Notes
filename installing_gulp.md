# Installation

Before you start using Gulp, you need node.js installed on your computer.

We will install and configure everything one by one, as needed. Let’s start with installation of Node.js


Installation of node.js is very simple. Go to [nodejs.org](https://nodejs.org/) and click on install button. It will download the installer according to your operating system.


Install the file you just downloaded, and follow the installation instructions. 

*If you are on Mac, you can use Terminal for executing node.js commands. If you are on Windows, node will install its own command prompt. *

To make sure you have installed Node properly, open terminal (on mac) or Node.js command prompt (on windows) and type ```node -v```, press enter, and you should get version number of your node installation. 


### Next let’s install Gulp

Different libraries or scripts are called **package** in Node’s terminology. 

For installing packages, we use **Node Package Manager**, commonly knows as **NPM**. 
(*You can read more about NPM on https://www.npmjs.com/*)

Go to terminal (on mac) or node.js command prompt on (windows), and type the command ```npm install -g gulp``` and hit enter.

With this command, we are instructing node package manager to install gulp globally. 

If you get error during installation:
* On mac you may need to add ```sudo``` command in front of npm, so it will be ```sudo npm install -g gulp```, sudo will also prompt you to add your system password
* On windows, you may need to right click on node.js command prompt, and select “Run as Administrator”, This will allow NPM to install packages with administrator privileges.

Now you have Gulp.js installed and ready to be used.

