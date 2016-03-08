# Multi-Layered, Intelligent Scaffolding

## A helpful and friendly node based tool to help individuals/teams create and maintain highly personalized web apps 

*This project is only at the conceptual stages at this point.  We hope to release the first batch of Micro commands and work our way up from there.  If you want to contribute let me know!*

### Goals

1. Make a lightwieght, multi-purpose and highly customizable scaffolding/templating/mockup app that can fit into a wide range of work flows.
2. Be able to continually integrate new scripts as new frameworks and systems arise without having to rewrite the entire program from scratch (ex. extend scripts used to build express apps to build Angular/Ionic apps).  This does not mean that refactoring on the app will not be done, however.
3. Build an app with the idea in mind to store and recycle materials (templates,scripts,functions) acquired by a developer or team over long periods of time in a way that is maintaible and accessible.


### Guiding principles

A core principle of Multi-Layered, Intelligent Scaffolding (hereby called mlis) is to always stay at the root of a project in your bash shell.  No 'cd'ing into a 'app/public/store/list/views' folder and then 'touch'ing a file or 'mkdir'ing a folder and then copying and pasting into 4 different files from getbootstrap over and over and over again.  

mlis utilizes Node to allows a user to run a command from the root of the app using variables taken from the mlis.settings.json file.  This file will set roots to folders, which sets of commands a user will want, and settings on where styles, templates, data, etc.. should go.  In this way, a three word command can produce multiple files and folders as well as inject content that is relevent to the project at hand.

The "Intelligent" aspect of mlis happens in several ways:
1. When a user is not entirely sure what the name of a script or template that he/she wants to run is, every command or directory can be run followed with a '?' to get the contents of the folder in question.
2. If a command is run which fits the scheme of a typical mlis command but a variable used is not defined (for example 'make views lovely.js' where views is usually a location, but is not defined) a prompt will come up for you to add this variable into the mlis.settings.json.  In this way, your flow of work is not broken by having to manually open the mlis.seetings.json file and you can continue along with the task at hand.
3. Templates will have a series of special fields which a user will be prompted to fill in.  For example, if using a jumbotron template, a user will be prompted for the "main title", "button link text", "page to link to", and "styles to add".  For every prompt, a user can enter '?' (with no quotes) to quiry what is availble such as which pages are current built. (for string tasks, there will be mock language options from libraries like loremipsum, hiperipsum, cupcakeisum, etc.)   In this way, a novice user of mlis can learn while making projects and expert users can have reminders where needed.
4. Eventually a mapping process can be used to create a visual representation of the project at hand for collaborators to discuss progress or plans as well as documentation.  The generated map should be thorough enough to generate a nearly identicle project while flexible enough to edit parts of its contents and generate a second highly unique project with a similar folder structure.  These process will be categorized as Supra commands and will be discussed in detail later. 

### The Four Tiers of Scaffolding

To help with working only at the root, a four tier shell heiarchy is strictly implemented to allow scripts to be reused and combined as well as allow a user to drop into a shell that is for a particular task.  

The four levels used in this application are called Micro, Meso, Macro, and Supra.  These levels will be explained in depth in their respctive sections.  In one sentance, the general idea of mlis is that a Supra command is comprised of a series of Macro commands which are themselves comprised of a series of Meso commands which are themselves comprised of a series of Micro commands! However, a use can at any time use a Micro command without referencing a Meso command or a Meso command without referencing a Macro command.  In this way, high code reuse is employed in this app without limiting the level of control a user has.

## Inspiration

while learning meteorJS from an online tutorial, I watched a professional Meteorite tell me to do the same routine over and over again with each new component.  I make a folder named "whatever" and put a "whatever.js" with "template.Helper = function(1,2,3) { etc ...}" inside next to a "whatever.html" with the an open and closing tag of "<template name="whatever"></template>" and a "whatever.css" style added.  After the tenth, I wrote a shell script did this for me and realized I was now faster and less error prone than my teacher!

At this point, I tried to share my script with somebody.  However, I use windows at work and did not have access to something like a bash_profile to link my scripts to.  The work of frontend development is moving more and more in the direction that if you can't npm install it or bower install it, it's too much trouble for what it's worth.

The layered approach of control came a couple months after the micro prototype was built in pure shell.  The names and concept come from the writings of electronic artist Curtis Roads  about [Musical Time Scales] as found in his book Microsound which I studied extensively in my MSc.  This layered approach to sonic art composition helped me unlock the computer's potential in art and I believe this approach can be very effective in application development.

### How is this different from Yeoman?

mlis draws a lot of inspiration from Yeoman.  If you don't know Yeoman, check it out.  It's a great tool to kickstart a project if you are unfamiliar with a framework.  It's how I got started with angular and first got a gruntfile to actually work.  In fact, the supra and macro level commands for mlis should work very similarly to initalizing a project with Yeoman.  

The main differences between mlis and Yeoman is the personalization and level of control a user has when working on thier project made possible through the mlis.settings.json file. Although many Yeoman generators have smaller commands (like 'yo backbone:collection name' in the backbone package to generate a certain structure), not all generators do and even the commands available are not easily modifiable.  Because yeoman generators are installed and run globally, small changes to a yeoman generator will in turn affect all projects using that generator, where changes to an mlis file, because it is stores at the root of every project, will only affect the project you are currently working on.  

After working with Yeoman generators, a user comes to the conclusion that not every angular/backbone/express project is going to be the same.  Every project has something unique about it, but most Yeoman generators do not allow a team/user to change small setting to meet the needs of a particular project (like folder generation paths or where to get content/templates from or even what templating language to use).   

MLIS takes a different approach to rapid development to webapps, one that is not only for the inital steps of app development, but is intended to follow and grow with the whole life cycle of an application as well as maintance later.

### How it works

mlis tries to keep the user in one CLI the entire time while it makes the magic happen.  If a detail is not given or the user gives a ? instead of an argument, instead of just failing, a prompt appears either asking for the variable again or listing all the options available.  

For ease of typing several commands at in the same scaffolding level, mlis allows a user to drop into virtual shell levels in order to run commands with varying levels of control. All commands can be run from the root level, such as 'supra init' or 'micro mkdir', or a user can drop into the meso shell by simply typing 'meso' and hitting enter.  This is particularly useful when running several commands in succession at the micro level. 

The folder structure is specifically set up for you to hack to your hearts content and refactor later.  All of the custom.js files are completely empty with only the basic require call to the lower level scripts (meso requires micro and macro requres meso, etc...)

*project_root*
```
mlis.settings.json
mlis.js
mlis[folder]
-mlis.custom.js
-framework[folder]->mlis.cylipso.js,mlis.ionic.js,etc...
-supra[folder]
--supra.js
--supra.custom.js
--framework[folder]->supra.react.js,supra.flux.js,etc...
--macro[folder]
---macro.js
---macro.custom.js
---framework[folder]->macro.meteor.js,macro.angular.js,etc...
---meso[folder]
----meso.js
----meso.custom.js
----framework[folder]->meso.express.js,meso.backbone.js,etc...
----micro[folder]
-----micro.js
-----micro.custom.js
-----framework[folder]->micro.knockout.js,micro.ember.js,etc...
mlis.content.starter[optional-folder]
mlis.content.project[optional-folder]
```

You will notice that in this folder structure, there are no html,css,sass,less,etc... no non-js content!  This is by design.  As a user accumulates assets in the form of templates and styles over a project or several projecs, a content folder will become simply too large to be portable between projects.  Also, work related projects might not give permission for their templates to be used by competitors or may contain sensitive information.  For these reaons, the actual templates have been seperated from the logic that generate and place them.  This is another huge differnce between Yeoman and mlis.

For convienience, there is a [starter content folder here] which if placed at the root of the project allows several "out-of-the-box" projects to be created as well as references for how to make a mlis template for various fields to be prompted.  If content locations are not specified in mlis.settings.json, this is one of the first prompts which will arise when running node mlis.  

If you have an awesome template that you developed and you wish to share it with the mlis community, please fork the start content project and insert your template and fork the mlis project to add any specialized logic that is needed to accomplish your templates.  A gallery is coming soon to display all the different starter content and commands to create and customize them.

General
---

Because mlis is a CLI based app and runs on node, you just need to type these two words while in the root of your project to get started:  
```javascript
node mlis
```
In general, commands on all level follow this pattern:

0. which level *(see note below),
1. what action (verbs),
2. where (location from mlis.settings.json)(prompted for if needed and not given),
3. what content (nouns)(prompted for if needed and not given),
4. optional arguments (prompted for if needed and not given)

*Because a user will often want to make multiple commands in succession at a given level of control, a user can type just the level they wish to work in (supra, macro, meso, micro), and drop into a virutal shell.  This effectively can skip the '0' level as noted above.  To get back to the virtual root level, run the mlis command or any other level (like meso or supra) to change levels.

At anytime a user is uncertain of how to continue with a command, they can simply type ? to recieve a prompt with a list of possible commands that would complete what is already typed or a list of all possible commands at the current stage in the build process.

Explicit Supra commands or setting in the mlis.settings.json can be activated to document exactly which commands are being run when in order to track progress and help refactor future commands.  Alternatively, a supra command can also be run to guess which scripts have been run based on tag and pattern recognition and document them retroactively.

# Level Specifications

Supra
---
Supra commands are intended to globally modify the mlis application itself, auto create documention for a application analysis and sharing, and store unique parts of an application (such as scripts or templates) a user found useful and wishes to use again in future projects. 

#### Supra example commands:

```javascript
map projectName
```
-creates a special JSON/YAML object with the folder structure and recognizable content within files.  
-if a structure is not recognized, the user is prompted to write what the structure is called and a brief description of it.  This is in turn stored in the JSON and will not be prompted for again.

```javascript
init projectNmae
```
-reads a settings.mlis.json if available to create a project 
-prompts the user for variables that are left out of the json file. These are then written into the json file.

```javascript
share (style)
```	
-creates a JSON of the folder structure is one does not exist
-Generates a 'projectName_share' folder with an index.html, projectName.css, and projectName.js.  
-launch a small website to convey the structure and content of the project to project leaders or collaborators.  

Macro
---
These commands focus on generating build systems and large scale scaffolding.  These commands will show the highest coupling to framework best practices and should be able to set up a small working app.  

#### Macro example commands 

with all details previously written in mlis.settings.json, the command
```javascript
create  
```	
will read the mlis.settings.json and create a project of a specified name (ex. 'My-Awesome-Project'), type (ex. angular), with folder structure of specified type (ex. dev/prod/test/node_modules) in specified location.

if a user did not set these in mlis.settings.json before hand, then they can set them now directly in the CLI if they are known such as:
```javascript
create name:"My-Awesome-Project", framework:angular-ionic, folder-structure:dev prod test, dev:base-template:sports-center-project-feb-2013
```	
All details given in the command line are then written into a mlis for documentation and potential further use.  exact variables for 'macro create' command are listed in the documentation.  

Of course if a user CBA to look at the documentation or says TL;DR, they can simply run from the macro shell
```javascript
create
```	
or 
```javascript
create ?
```	
or
```javascript
create name:"My-Awesome-Project", framework:?, folder-structure:?, dev:base-template:sports-center-project-feb-2013
```	
to be prompted only on specific components that they know they want, but either cannot remember what options are available or want to see which options there are now.  If a framework:argument is given where the argument is unknown to mlis, a prompt will arise for this particular entry to be re-entered and not the entire command.  If the user sees that it is a simple typo, he can correct and type enter to continue as usual.  Otherwise, a user can then type ? to get all the frameworks available. 

Meso
---
These commands are where highly individualed or project driven 'best practices' can be implemented.  Although these commands can in theory be used over a wide range of frameworks, there are usually some 'best practices' dictated by certain frameworks.  

For example, when working in an angular 1.X project, you might like to have all of your components in name.component.js files in a folder called components in the views folder.  Or you might like to have your components in a folder called the name of the component with three files called name.directive.js, name.js, and name.html.  Or you might like to have your directives in a folder literally called directives which itself is in a folder called the name of your directive which itself is not in the view folder but in a folder called 'Kitchen' because it has something to do with the particular app you are building.....you see all the different possibiities.  


or have each component broken into three  folder while I like to have my components in a folder with the name of the  Here is where you can generate multiple files and folders in one go that share variables between them.  Meso commands are basically a composition of Mico commands which share variables.  

#### Meso example commands

```javascript
mkdirstr component form contact
```
-read from settings.mlis.json to detect which framework we are working in. 
-If there is a script called mkdirstr in the framworks folder at this level, it will be called instead of the generic call.  
-In this case, the framework is angular so the component function in frameworks/angular.js is called which creates a contact.component.js, contact.html, and a contact.css file in a contact folder in the directory location for components given in the settings.mlis.json.  
-this particular script would lead to a series of prompts such as 'field name 1','required?','another field?' with suggestions for each step.  optional arguments can be put in from the command line initially to avoid these prompts. 

If no framework was given in settings.mlis.json or any other part of a command is missing, a user will be prompted to enter something the mlis understands and/or be given options which they can choose.  

Let's say a user has already specified they are working on an angular project in their settings.mlis.json file but wishes to take a Meso routine from an used when working with the express framework, but can't remember which routine it was, but remembers all the arguments!  
No worries, you can run:
```javascript
mkdirstr express:? form contact name:placeholder:"Joe Smith":required email:placeholder:"yourname@whatevs.com" sendemailto:'DjRussRuss@beastdj.com'
```
a prompt will appear giving you the options of which express Meso script you are trying to run and will input the arguments given and/or prompt you for ones that you have missed.  Because the filepath variables set in settings.mlis.json, Meso routines can often be shared between frameworks without breaking the structure of your project.


Micro  
---
This is ths meat and potatoes of mlis.  You will find that many of these commands are simply shell commands with more flavor and personalization.  

Micro example commands

mkdir views aboutUs
	
-this will make a folder in the views directory (specified in the settings.mlis.json file) called aboutUs.  
-if views is not specified in settings.mlis.json, a prompt will appear to ask where views is and it will be written into settings.mlis.json for future use.

touch views/aboutUS aboutUs.jade

-this will make a aboutUs.jade 

inject views/aboutUs aboutUs.jade jumbotron/standard 'hey check us out' 'we are number one' '/#contact.html' --style red

-this will inject a jumbotron into aboutUs.jade (in the jade format as specified in the settings.mlis.json file) with the first line as 'hey check us out', button text 'we are number one' and link to '/#contact.html'
-the 'style' flag with the argument red will add a css snippet in the location specified in settings.mlis.json.  This could be in a master styles file or a new _jumbotron.scss file creates and an @import injected into a master styles.scss
-mlis searchs for the template jumbotron in the folders given as the root for content in the settings.mlis.json

inject views/aboutUs aboutUs.jade jumbotron/?

-this will lead to a series of prompts about which jumbotron to use and which variables a user would like to insert. Suggestions will be given so that a rapid sucessions of returns will generate pleasant content.

inject views/aboutUs jumbotron/* 'hey checkit' 'represent' '/#contact.html' --style turquoise

-this will lead to an injection of every jumbotron in the jumbotron folder with the arguments passed into each
-if a variable is needed for a particular jumbotron, it will be prompted for before proceeding.


## Template generation
---

mlis already relies on many underscore.js functions to maximize code reuse between levels, so it was a natural choice to use underscore's built in templating language as a starting point for building templates.  

although pure underscore templating can still be implemented on templates, the mlis starter templates extends underscores templating engine with handlebars.js to create more semantically readable templates.

when an inject function is called to retrieve content from the content folder and place it into a file, mlis scans the template for special markers with the helper function mlis.prompt to either take and place arguments given in CLI or ask the user for input.

for example, if we have an about us page, the top of the about_01.html file may looks like this: 
```html
	<h1>{{ mlis.prompt name="title" }}</h1>
	<h2>{{ mlis.prompt name="sub-title" }}</h2>
	<div class="{{mlis.prompt.title}}">
		{{ mlis.prompt name="content" options=input|mock loop=true as="paragraph" }}
			{{#each content }}
				<p>{{ mlis.prompt.content.paragraph }}</p>
			{{/each}}
		{{ mlis.prompt name="find out more" options=Y|n as=FOM }}
		{{#if findOutMore}}
			<a href="{{ FOM.prompt name='link'}}"
			class="btn btn-{{ FOM.prompt name='button-type' 
			options=default|success|warning|error }}">
				{{ FOM.prompt name="find out more text" as="FOMT" }}{{FOMT}}
			</a>
		{{/if}}
	</div>
````
mlis will see the function mlis.prompt and send the name to the CLI to prompt the user.  Default options can be given with the options argument.  If the loop variable is set to true, the prompt will call the loop prompt "another {name}?" and if yes (the default), the prompt will be called again until a user types 'no' to the "another {name}?" prompt.   

In certain situations, a user may not want to replace these handlebar markers, but rather transform them in some way to match the framework langauge currently being used in a project. For example, a setting could be made to store all the prompt variables in a json file with the name of the template to be placed in the same folder and called by the template at runtime.  These options can be set in the mlis.settings.json file in the template options section.


#### CSS templates

#### SASS templates

#### LESS templates

#### HTML templates

#### JADE templates

#### JS templates

[Musical Time Scales]: https://slowdensity.files.wordpress.com/2013/05/timescales-diagram.jpg?w=549 "Curtis Roads: Musical Time Scales"
[starter content folder here]: https://google.com "starter content folder here"