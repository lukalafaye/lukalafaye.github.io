---
date: 2019-04-21 00:00:42
layout: post
title: What is AppleScript?
subtitle: Reviewing the AppleScript Editor app and figuring out how to use it
description: Reviewing the AppleScript Editor app and figuring out how to use it
image: /img/2019-04-21.jpg
category: programming
tags: 
- Apple
- Computing
- AppleScript
paginate: false
---

# AppleScript

If you are a Mac user, you most probably have looked through all the apps you have in your Launchpad and may have noticed an app called "Script Editor" (called "AppleScript Editor" in older versions). 

<img src="https://en.hackdown.tech/img/osx-5ca26ee4c2289.png" /><br />

Looking upon that you may have wondered "What is AppleScript?" This article will tell you about that. 

# What is AppleScript?

**AppleScript** is a native scripting language for macOS designed to help you automate your tasks by providing rich access to various system features (such as window buttons, filesystem and so on). The syntax of the language is close to natural speech.

# How to use

To start developing AppleScripts, open the _Script Editor_ app (by default located in "Other" in Launchpad). 
<img src="https://en.hackdown.tech/img/osx-5ca26f0db6f6a.png"><br />
When you first type your code it will not be syntax highlighted, start or "build" it to perform syntax check and highlighting.<br /><br /> 
<img src="https://en.hackdown.tech/img/osx-5ca26f443ed12.png"><br /><img src="https://en.hackdown.tech/img/osx-5ca26f31b2848.png">

Press the "Play" button in the toolbar to execute the script. That will check and build as well.
# Basic Examples

## A hello world alert

To display an alert you can use the `display alert` method: 

```applescript
display alert "Hello world"
```
As expected, this pops up a little alert box saying "Hello world":<br />
<img src="https://en.hackdown.tech/img/osx-5ca26f5b72b9b.png"><br />

## A notification example
To display a notification you can use the `display notification` method:

```applescript
display notification "Work is done" with title "My awesome app" subtitle "Work status changed"
```

This will pop up a basic system notification with the given parameters.<br />
<img scr="https://en.hackdown.tech/img/osx-5ca62839957ec.png"><br />
All arguments except the first one (the main text) are optional.
## Modals 
You use the optional `buttons` argument of `display dialog` to turn it into a modal:
```applescript
display alert "Are you sure? This dialog will automatically close after 2,5 minutes." buttons {"Yes", "No"} giving up after 150
```
Result: <br />
<img src="https://en.hackdown.tech/img/osx-5ca629349e8b5.png"><br />
(this dialog will close in 150 seconds)

### Using the response
In order to **use** the data received from the prompt you need to save it into a variable (we will use `result`):
```applescript
set result to (display alert "Are you sure? This dialog will automatically close after 2,5 minutes." buttons {"Yes", "No"} giving up after 150)
if button returned of result = "Yes" then 
    display alert "Action not cancelled"
else
    display alert "Action cancelled"
end if
```
In this example we are asking the user for confirmation and displaying different alerts depending on what was the response.
## Asking user for information
We need to use `display dialog` with `default answer` set to any value (blank to provide empty box). This will make the dialog show a text box for user to answer the question.
Example:
```applescript
set result to (display dialog "Enter your name" default answer "" giving up after 150)
set userName to text returned of result
display alert "The user name is " & userName
```
This code asks the user for their name and shows a new alert box with it.<br />
<img src="https://en.hackdown.tech/img/osx-5ca62be7a12dd.png"><br />
<img src="https://en.hackdown.tech/img/osx-5ca62bf496019.png">

# Conclusion

AppleScript was designed as a simple way of automating tasks and is one of the ways to do so. Modern versions of Script Editor also support a special subset of JavaScript so if you don't like the unusual syntax you may feel more comfortable writing code in JS.
