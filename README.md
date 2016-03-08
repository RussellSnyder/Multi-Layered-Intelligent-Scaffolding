# Multi-Layered, Intelligent Scaffolding

## A helpful and friendly node based tool to help individuals/teams create and maintain highly personalized web apps 

** This project is only at the conceptual stages at this point.  We hope to release the first batch of Micro commands and work our way up from there.  If you want to contribute let me know! **

The goal

Make a lightwieght, multi-purpose app that can produce web apps as fast as you can concieve them.  Another goal is to be able to integrate new scripts for new frameworks without having to reinvent the entire program from scratch (ex. extend scripts used to build express apps to build Angular/Ionic apps).  This application is not meant to be an end tool, but rather a means to recycle/document materials acquired by a developer over their lifetime in a way that is maintaible and accessible in the future.


Guiding principles

A core principle of MILS is to always stay at the root of a project in your bash shell.  No 'cd'ing into a views folder and then 'touch'ing a file or 'mkdir'ing a folder and then copying and pasting into 4 different files over and over again.  A command run from the root of the app using variables taken from MILS.settings.json should set roots to folders and settings on where styles, templates, data, etc.. should go.  The Intelligent aspect of MILS is that when a user is not entirely sure what the name of a script or template that he/she wants to run is, every command or directory can be run with a '?' to get the contents of that folder.  Also, Supra commands will help a user communicate the project structure be building an easy to understand diagram directly from the project strucutre. 

To help with working only at the root, a four tier shell heiarchy is strictly implemented to allow scripts to be reused and combined as well as allow a user to drop into a shell that is for a particular task.  

The four levels used in this application are called Micro, Meso, Macro, and Supra.  This will be explained in depth soon.


How is this different from Yeoman?

This app is totally inspired from Yeoman, Yeoman is awesome!  It's a great tool to kickstart a project.  In fact, the Macro level commands for MILS should work very similarly to initalizing a project with Yeoman.  The main difference is the levels of control over scaffolding that MILS allows is not always built into every Yeoman generator.  Every angular or backbone project is going to have something unique about it, but Yeoman does not allow a team to change small setting to meet the needs of a particular project (like folder generation paths or where to get content from).   

MLIS takes a different approach to rapid development to webapps, one that is not only for the inital steps of development, but is intended to follow and grow with the whole life cycle of an application.


How it works

  MILS allows a user to drop into virtual shell levels in order to run commands with varying levels of control. All commands can be run from the root level, such as 'supra init', or a user can drop into the supra shell by simply typing 'supra'.  This is particularly handy when running several commands in succession at the micro level. 


Supra

	These commands will come only after all of the Macro, Meso and Micro commands are developed.  Theoretical commands will be as follows. 

Supra example commands:

```node
map projectName
```

	-create a JSON object with the folder structure and recognizable content within files.  if a structure is not recognized, the user is prompted to write what it is.

init projectNmae

	-reads settings.mils.json to create a project passing in the 
	-prompt the user for variables that are left out of the json file. These are then written into the json file.

share (style)
	
	-creates a JSON of the folder structure is one does not exist
	-Generates a 'projectName_share' folder with an index.html, projectName.css, and projectName.js.  These files will generate a small website to convey the structure and content of the project.  

Macro

	These commands are most similar to Yeoman commands.  They focus on generating build systems and large scale scaffolding.  Ideally, a single command is a composition of Meso commands (which are in turn a composition of Micro commands).

Macro example commands 

Meso

	These commands are where the 'best practices' of various frameworks begin to be seen.  Here is where you can generate multiple files and folders in one go that share variables between them.  Meso commands are basically a composition of Mico commands which share variables.  

Meso example commands

mkdirstr component form contact

	-read from settings.mils.json to detect which framework we are working in.  In this case, it is angular, so this command creates a contact.component.js, contact.html, and a contact.css file in a contact folder in the directory location for components given in the settings.mils.json.  
	-this particular script would lead to a series of prompts such as 'field name 1','required?','another field?' with suggestions for each step.  optional arguments can be put in from the command line initially to avoid these prompts. 



Micro  

	This is ths meat and potatoes of MILS.  You will find that many of these commands are simply shell commands with more flavor and personalization.

Micro example commands

mkdir views aboutUs
	
	-this will make a folder in the views directory (specified in the settings.mils.json file) called aboutUs.  
	-if views is not specified in settings.mils.json, a prompt will appear to ask where views is and it will be written into settings.mils.json for future use.

touch views/aboutUS aboutUs.jade

	-this will make a aboutUs.jade 

inject views/aboutUs aboutUs.jade jumbotron/standard 'hey check us out' 'we are number one' '/#contact.html' --style red

	-this will inject a jumbotron into aboutUs.jade (in the jade format as specified in the settings.mils.json file) with the first line as 'hey check us out', button text 'we are number one' and link to '/#contact.html'
	-the 'style' flag with the argument red will add a css snippet in the location specified in settings.mils.json.  This could be in a master styles file or a new _jumbotron.scss file creates and an @import injected into a master styles.scss
	-MILS searchs for the template jumbotron in the folders given as the root for content in the settings.MILS.json

inject views/aboutUs aboutUs.jade jumbotron/?

	-this will lead to a series of prompts about which jumbotron to use and which variables a user would like to insert. Suggestions will be given so that a rapid sucessions of returns will generate pleasant content.

inject views/aboutUs jumbotron/* 'hey checkit' 'represent' '/#contact.html' --style turquoise

	-this will lead to an injection of every jumbotron in the jumbotron folder with the arguments passed into each
	-if a variable is needed for a particular jumbotron, it will be prompted for before proceeding.


Naming inspiration
------------------
The inspiration for the layered approach of control come from Curtis Roads' writings on [Musical Time Scales] as found in his book Microsound which I studied in my MSc.  This layered approach to sonic art composition helped me unlock the computer's potential in art and I hope to continue with this apporach in application development with this project.



[Musical Time Scales]: https://slowdensity.files.wordpress.com/2013/05/timescales-diagram.jpg?w=549 "Curtis Roads: Musical Time Scales"