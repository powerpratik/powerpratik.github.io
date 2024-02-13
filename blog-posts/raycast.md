# Raycast; A spotlight search Replacement for keyboard warriors.

You might be wondering why do I need to replace spotlight search on my Mac? It works just great. Yes, it is great, but it can be so much better. From doing all the simple operations of spotlight like quick search files, currency conversion etc to complex operations like deploying this very Markdown on a webpage all automated through a simple trigger word. Let's take a look into some features I like about Raycast.

### All of the features Imention can be invoked using a custom keyword or a custom keybind of your choice.
## 1) Extensions: A lot of extensions
There are tons and tons of community driven extensions that you can install on raycast with just a click. It enables you to do things like search youtube content with metadata directly onto your spotlight like search box, compose mails directly into search box, play and control spotify music directly from the "cmd+space"  box. You get it, there are tons of extensions for you to use and it's increasing everyday. There is definitely something for you. 
### This image shows how easy it is to control spotify directly from raycast without going into the app itself
<!-- ![spotify](./images/spotify.png "Spotify Extension"|width = 25%) -->
<img src="./images/spotify.png" alt="Spotify Extension" width="50%"/>

## 2) Snippets
This is a rather simple  but  effective feature. A very quick way to boost your keyboard speed. Quick scenario: Say in your daily line of work there are phrases or sentences you use more often use to search: like in this case say you need weight estimation of objects:  "How much does something weigh?". Instead of typing everytime for the whole thing, you can just use a trigger word for instance "#weigh" and the keyboard expands it to "How much does something weigh" automatically. Another quick example would be expanding "omw" to "On my way" automatically.That is cool for repititve tasks. Yes, there are keyboard binds you can use for this but it's better to use in raycast especially when you couple all of the features raycast provides toogether.   
### This snippet converts your word #blog to a phrase "Create file at Md Script" which in my case is a name to invoke a bash script which performs automatically opens a new file with the desired filename at my project folder. 
<!-- ![snippet](./images/snippet.png "Snippet"|width = 25%) -->


## 3) Quick links
Just like snippets but imagine using some trigger phrases to do operations like opening an application, website , another raycast extensions etc. Example: Instead of opening apps like spotify or your favorite webpage in your favorite browser directly by simply using the keyword of your choice. 
### This image shows many quicklinks to open a folder in finder to open webpages like youtube or chess.com directly by typing the custom keyword.
<!-- ![quicklink](./images/quicklink.png "Quicklink"|width = 25%) -->
<img src="./images/quicklink.png" alt="Quicklink " width="75%"/>

## 4) Script Commands
Now you might consider, as a power user, you want to be able to script in your favorite language and have that be invoked directly from raycast. Well, you have that flexibility to. This is how I was able to deploy the website, post new blog posts on to the website directly by invoking the command. You can have a bash script or any script to automate the deployment of the changes in your project to the github repository. Now invoke the bash script using raycast with a simple trigger word so everytime you use the trigger word, it pushes any new changes you made to the project directly to the website. Using this trick I was able to add new blog post in Markdown, have it convert into js and post the newly converted md to my project folder using "#blog" "#upload" trigger respectively.  

<!-- ![script-command](./images/script-command.png "Script Command" | width = 25%) -->
<img src="./images/script-command.png" alt="Script Command " width="75%"/>

### The "#blog" command on snippet triggers this bash script that lets me input filename of the Markdown directly and it opens the markdown ready for me to start blogging easily
