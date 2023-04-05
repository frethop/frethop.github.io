---
share: true
---
# Writing Your Own Plugin: An Introduction
My family enjoys board games.  From the standard to the odd, we love to play them.  Many board games have the idea of *expansion packs* -- new additions to a game that changes the way to play or adds a new challenge.  Several of the games we have played are actually boring without a few expansions.

When we carry the idea of an expansion pack to software, we get the idea of a *plugin*.  A plugin is code that is dynamically added to an established software platform, expanding the way that software is used.  Many times the original software is designed to be enhanced with plugins.  And sometimes the best plugins come from real users of the software.

A great example of a plugin system is the knowledge management software called **Obsidian**.  Obsidian is designed with a solid, basic functionality and a plugin system that lets the user choose new functions to add to the basics.  There are hundreds of plugins written for Obsidian users to add to their basic Obsidian platform.  For example, there is a plugin that enables the camera on a mobile device for adding picture to Obsidian notes.  There is a plugin that builds a todo list system into Obsidian notes.  There are plugins for book writing, for importing highlights made on a Kindle, for rendering diagrams drawn on tablets.  All these plugins are available through the Obsidian application for free.

While it is fun to go shopping through Obsidian plugins, sometimes a user might need some extra functionality not addressed by a plugin.  This is the time to write your own plugin.  Need a plugin that makes Obsidian smoother for teaching a class?  Write your own!  Need a plugin that changes colors for people who are colorblind?  Write it yourself.  The plugin system has tools and -- yes -- plugins that help with this kind of development.

This article starts a series about writing your own plugins.  This first article will discuss the idea of a plugin, walk through the cycle of how plugin code is executed, and show the tools you need to get started.  Future articles in this series will get you started on a simple plugin and will step through how to code up increasingly more difficult plugins.  We will conclude with some interesting ideas about using Obsidian and the plugin system for things they might not have intended.

## Javascript and Typescript
We start this discussion where all software has to start: a programming language.  All code executed on a computer starts with a programming language. Obsidian plugins start with Javascript.

Javascript was invented in 1995 by a man named Brendan Eich.  Eich invented Javascript as a way to write code that could be executed within a Web browser.  At that time, the Web browser of choice was Netscape, the first Web browser[^1].  The idea was that a Javascript program could be loaded from a site on the Internet and the code could be executed within the Web browser itself to provide some new function that was not there before.

[^1]: Javascript went on to the European Computer Manufacturers Association and became an ECMA standard in 1997.  The Mozilla foundation actually continued to develop JavaScript for the Firefox browser.

That should sound familiar.

In fact, Javascript grew in popularity and use because of this niche: code that was executed inside other software.  The Web browser applications have expanded to include Web frameworks -- a kind of code library -- that help build complex code bases.  Javascript is used to implement extensions to Visual Studio Code, a rich editing and programming environment tool.  It has been used to liven up presentations and to contribute apps for smartwatches.

Javascript has indeed seen a lot of use.  But the language itself is a bit sloppy.  The language was designed to be "forgiving", that is, it tries to hide any mistakes in the code.  In order to do this, it has to guess what the programmer meant by the code, and often, this guess is wrong.  In addition, this sloppiness does not enforce good coding practices, which, in turn, allows poorly written code.  Javascript was really never meant for serious programming.  

That brings us to Typescript.  Typescript adds some syntax to Javascript that adds strong typing to the language.  By enforcing data typing, many errors that would have made it to execution and caused program crashes can now be caught before a program is executed.  In fact, by using the appropriate editor, a programmer can catch these errors as the code is written.  

Plugin programming for Obsidian plugins uses Typescript.

## Tools that Help Develop Plugins
Javascript is a programming language and is meant to be executed.  We mentioned in the previous section that Javascript is code that was executed inside other software.  To be executed, Javascript code needs an "execution engine", something that executes that code in a software environment.  In addition, Javascript also needs a set of tools that transform it into the code that gets executed.  

Obsidian provides the environment and the engine in which Javascript executes.  MORE

When someone writes code in Javascript, that code must be converted into a form that Obsidian can execute.  

## Obsidian and How Plugins Plug in
blah blah

## The Lifecycle of a Plugin with Obsidian
blah blah

## Some Other Tools
blah blah

## Finally: Why Write Your Own Plugins
blah blah


