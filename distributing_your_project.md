# Distributing your project

You will often need to work with other developers, or share your projects through GIT.

When you are sharing your project, you do not need to share *node_modules* folder, and builds folder. This will save space in your repository, and also there will be less number of files to share. On 

Every user can have his/her own copy of *node_modules* folder, and builds folder.

Once you get files of a shared project, first thing you need to do is go to terminal or command prompt, and run ```npm install``` command. This will install all dependencies listed in package.json file.

(You may need to provide administrative privileges, as described during installation process)

Once all packages are installed, you can use gulp tasks as required, or as per configurations of your gulpfile. 