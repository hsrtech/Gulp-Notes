#Project Setup

After node.js and gulp are installed, the first step is to create **package.json** file. This file keeps information about your project, and different packages (*Node based javascript libraries*) that you need to automate your workflow.

First create a folder for your project, and navigate inside that folder using command prompt.

1. To do so, type ```cd <path of your working folder>```
(*On Mac you can drag and drop folder on command prompt to get full path of folder.*)

2. After you are inside your working folder, type ```npm init``` and hit enter. (*npm init command helps you create a [package.json](https://docs.npmjs.com/files/package.json) file for your project by asking you few questions. You can also create this file manually if you want to.*)

Following is the list of questions that are asked. Only name and version are required, you can leave all other empty for now. (You can edit package.json file manually whenever you want.) 

*Press enter to move to next question.*

```
name: (project name)
version: (1.0.0)
description:
entry point: (index.js)
test command:
git repository: 
keywords:
author: 
license: (ISC)
```

(You can read more about package.json file on its documentation here: https://docs.npmjs.com/files/package.json)

You will find package.json file created in your folder with content like following:

```
{
  "name": "learngulp",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Alok Jain",
  "license": "ISC"
}
```
