---
layout: post
title: Decompiling/Reverse Engineering Android Apps
---
For a few months, I have been working on Android development. I knew how easy is to get an app's apk
on the internet. That's why I researched ways of decompiling apk file and protection for reverse engineering
I was surprised by results because it was too easy to decompile an android application and I tried it with my app
Everything was so obvious.

### Requirements

Here's what you need to decompile an android app.

- A zip tool to unzip - you can use any
- A tool convert .dex to .jar - [Download dex2jar](https://code.google.com/p/dex2jar/downloads/detail?name=dex2jar-0.0.9.15.zip&can=2&q=)
- A tool to decompile .jar file - [Download JD-GUI](http://www.softpedia.com/get/Programming/Debuggers-Decompilers-Dissasemblers/JD-GUI.shtml)


### Steps

#### Open apk
Apk is a package which stores your app's files executables, resources etc. It is actually a folder. That's why
this is the easiest step.

- Change `app_name.apk` to `app_name.zip`
- Unzip `app_name.zip`

#### Dex to Jar
Dex is dalvik vm version of jar. When you open unzipped folder, you will be see classes.dex which
contains all of your .class files. (Btw class files are compiled .java files).
For easy use

- Move your classes.dex to dex2jar's folder (dowload link above).
- Navigate to dex2jar's folder by using terminal - `cd /Path/to/dex2jarfolder`
- Enter command `./dex2jar.sh classes.dex` on the terminal. It will produce .jar file named **classes_dex2jar.jar**in the working
directory.

#### Decompile Jar
JD-GUI is very simple tool to use.

- Open JD-GUI then drag&drop your .jar file to it.

After that you will be able to see java files, packages etc.

#### So what ?
As you could see code is pretty understandable, much more than decompiled ARM assembly codes :)
So you can

- understand how an important task performed.
- see external libraries used in the app.

I won't give the names but I tried this on some (a few of them popular) apps and results are same as my app


#### How to protect
The easiest way is using [proguard](http://developer.android.com/tools/help/proguard.html). It is a little pain if you use too much external libraries (especially native). However
it works. At least you can protect your code from unprofessional reverse engineers.
