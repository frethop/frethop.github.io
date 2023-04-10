---
share: true
title: A-first-plugin
---
# A First Plugin
In this article, we will get started with a simple plugin for Obsidian.  We will walk through how  to start, what tools we need to do development work, and how to do a little experimentation.

Much has been written and recorded about first plugins.  In fact, in the "Obsidian Plugin Developer Docs" there is a nice set of instructions, written by Marcus Olsson, on how to get started.  There are many videos that you can watch to get started, including "Create Your Own Obsidian Plugin" by Antone Heyward and 

We will try to add to the wealth of information you can access.  

## Frustration gets you started
To write a good plugin, you need to be able to use the plugin.  Plugins -- and phone apps, and other pieces of software -- come from your experience, and a lot of times from your frustration.  It's really hard to come up with an idea out of thin air; you typically need to have some personal investment in the software you are writing.  (This is likely not true if you are writing software for a development company.)

For example, it might be hard to write a plugin that implements a day planner if you don't really use one.  However, it would be easier to develop a plugin that MORE  

Looking for plugin ideas can be assisted by MORE

> [!tip] A plugin idea!
> The plugin created here as an example was indeed born from frustration.  We are going to develop a plugin that autocorrects when you type two capital letters in a row.  I do this all the time and having something automatically fixing this would be great! 

## Things you need to get started
Before you start writing your Obsidian plugin, you need a few things.  

- **Computer and storage:** It's pretty obvious that you need a computer to create a plugin.  You also need storage, but not a lot.  Complex plugins with a lot of code take up around 250 MB of storage; smaller, less complex plugins take up less than 80 MB.  Installed plugins take up a lot less.
- **Github account:** blah blah
- **Git:** Git is a 
- **Node.js:** blha blah

## Let's get started
Let's get started by following the steps in the set of instructions written by Marcus Olsson.  

1. We'll start by cloning the "Obsidian Sample Plugin" repository.  We will call this one "obsidian-twocaps".
   ![[02-create.png]]
2. We need to download the code from Github to our local computer so we can work with it. We will clone this from the Github repository we just created.
![[02-clone.png]]
3. To get started with development and "npm", we need to initialize npm data with "npm install":
   ![[02-npminstall.png]]
4. The final step is to compile the source code into Javascript.  To do this, we can execute "npm run dev".
![[02-npmrundev.png]]
Note that the "npm" command is now in "[watch]" mode, meaning that when it determines a file has been changed, it will automatically go through the compile cycle again.

## Plugin files
We are now ready to make changes to the code to start developing our example.  Before we do that, however, let's examine a few the files we have copied.  
![[02-listing.png]]
- **main.ts: ** This is the file that holds the source code for the plugin.  We will make changes to this file.  This file gets compiled to "main.js", which contains the Javascript code that Obsidian will execute.
- "manifest.json: " This is a JSON file that contains information about the plugin we are working on.  We need to change the information in this file before we install the plugin into Obsidian.
- "**package.json: **" This file is a JSON file containing development information.  It specifies what tools to use to compile the code.  It contains a list of the code this plugin uses, so the tools we use can automatically download all that code (the "npm install" did that for us).
- "**styles.css: **" This is a CSS file (Cascading Style Sheets) that we will use to specify the appearance of our user interface.  Note that, since our plugin has not user interface other than settings, we will not work with this file.  We will, however, use it extensively in future articles that describe some more plugin work.

There are other files in the folder we cloned, but these are files used by tools and commands and are maintained by other programs.  The four files above are the most important and should be set up before we start any real development.

## The lifecycle of a plugin
Plugins have a "lifecycle", that is, they have a sequence they go through, executing specific code sections as they go through this sequence.  We should examine this sequence so we know what code to change to make the plugin do what we want.

1. Load time: This happens when a plugin is loaded from the code file in storage into Obsidian's memory.  This happens most often when Obsidian starts, but it could also happen when a plugin is enabled in Obsidian's settings.  When a plugin is loaded, the "onLoad" method defined in the plugin's class is called.  The "onLoad" method is responsible for setting up and initializing parts of the plugin, including the user interface, the ribbon and the status bar,  and the plugin settings.
   
2.  Opening a file: If the plugin has been started to manage a file, then the "onOpen" method is called to do some initialization with that file.

3. Events:  After loading and opening a file, the plugin calls code in response to *events*.  Events are actions performed by either the user or the computer that require a response from the plugin.  For example, a mouse click would be considered an event, but events are usually more specific than that.  Mouse clicks on icons are different than mouse clicks in text areas.  Events are handled by *callbacks* in your code, which are set up at load time.  

4. Closing a file: When the user is done with a file, if they opened one.  When file use is terminated, the method "onClose" will be called to clean up data and close the file.

5. Terminating a plugin: Eventually, the user will also be done with the plugin.  Perhaps they have closed a file or moved to a different plugin.  When a plugin is terminated, the "onunload" method is called before stopping the execution of the plugin code.

> [!note] The Minimum Plugin
> Note that all of these method definitions are optional.  You could code up a plugin with only a plugin class and no methods defined inside.  The plugin would be really boring, because it would not respond to any events and it would not have a user interface.  

## Where do we start?
Let's get started by making sure Obsidian will know the plugin's name and what code it depends on.  

We will start by making changes to the "manifest.json" file.  
1. We need to change the "name" field to the name of the plugin.  In our case, let's change the name to "obsidian-twocaps".  
2. We need to change the version number.  Since our plugin is under development, let's set the version to "0.1".
3. Let's change the description to describe our plugin: "A plugin to fix two typed capital letters in a row."
4. Change the value of the author field to your name.

You could change other fields -- like "keywords" and "license" -- but they are not necessary right now.

Save the package file and make sure that the "npm run dev" command automatically builds the new code.

## Changes to the plugin code
Now let's examine the code in the "main.ts" file.  Let's make a couple of observations about the code that's in that file we copied from Github.
- The file contains 3 classes: one for the plugin, one for a "modal" (popup) that is started by the plugin code, and one that works with settings.
- This plugin does not work with files.  So it does not define "onopen" or "onclose" methods.
- The "onload" methods does various types of setup.  It adds to the command ribbon on the left ("addRibbonIcon"); it adds text to the status bar on the bottom ("addStatusBarItem"); it adds command to the command palette ("addCommand"); it adds a settings section for this plugin ("addSettingTab"); and it registers a callback for a Document Object Model (main Obsidian display) event.  It also registers a timer ("registerInterval") that logs a message every 5 minutes.  
- The "onunload" method is present, but empty.  We don't need to do anything when the plug is unloaded.

Let's start working on this plugin by cleaning up the "onload" method.  

> [! Step 1] Clean up the "onload" method
> Let's start by working on the "onload" method. Our plugin is going to change any text that gets typed, so we really do not need a lot of user interface items.  Remove everything except the "loadSettings" call at the beginning and the "addSettingTab" call and the "registerDomEvent" call at the end.

The "onload" method should look like this when you are done:
```
async onload() {
    await this.loadSettings();

    // This adds a settings tab so the user can configure various aspects of the plugin
    this.addSettingTab(new SampleSettingTab(this.app, this));
    
    // If the plugin hooks up any global DOM events (on parts of the app that doesn't belong to this plugin)
    // Using this function will automatically remove the event listener when this plugin is disabled.
    this.registerDomEvent(document, 'click', (evt: MouseEvent) => {
        console.log('click', evt);
    });

}
```

> [!Note] Next clean up the "MyPlugin" class code
> We are not going to use a model, so remove the "SampleModal" class code.

As before, save your file and make sure "npm" builds the plugin with no errors.

