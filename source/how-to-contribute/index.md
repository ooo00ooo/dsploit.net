---
author: evilsocket
comments: true
date: 2013-03-20 20:55:44+00:00
layout: page
slug: how-to-contribute
title: How to Contribute
---

## How to Open an Issue

If you find a bug, weird behaviour, missing translation, a feature not working or anything strange in the application
you are encouraged to open an issue on the appropriate [github page](https://github.com/evilsocket/dsploit/issues).  
For your issue to be considered and solved ASAP please provide the following informations while opening it:

* Your Device model.
* Your ROM name and version.
* The version of dSploit your are running.
* As many details as possible on the network you are running dSploit on.
* A description of the issue you have, if it is a MITM feature not working, please specify if the other MITM features are working on your network.
* [A logcat](http://forum.xda-developers.com/showthread.php?t=1726238) taken while the application was running and the issue happened. 

**Any issue which will not contain those details, will be signaled with a link to this page and closed from 24h to 48h later.**

## Contribute to the Code

If you are an Android/Java developer and you want to contribute to the project, you are very welcome!  
Setting up the environment and building an apk is quite simple, just refer to the following procedure.

#### Requirements

First of all, you need the latest Android SDK installed and the git command line tool to clone the source code repository.  
If you want to modify the native tools, you will need the [Android NDK](http://developer.android.com/tools/sdk/ndk/index.html), but this is not mandatory to build the apk.

#### Cloning dSploit

The project uses GitHub as its main codebase and versioning control system, therefore you will start cloning the code repository:
		  
	git clone https://github.com/evilsocket/dsploit.git

This will create the dsploit folder and you are now ready to go.

#### Building with Gradle

If you want to build dSploit using [Gradle](http://www.gradle.org/), just cd to the source code directory and type:

	./gradlew build

This will generate an unsigned apk in build/apk

To generate a signed apk, rename your certificate to keystore.keystore and put it in dSploit/keystore.keystore.
Then modify dSploit/build.gradle as follows to add the required signing configuration:

    buildscript {
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:0.5.0'
        }
    }
    apply plugin: 'android'

    dependencies {
        compile fileTree(dir: 'libs', include: '*.jar')
        compile project(':actionbarsherlock')
    }

    android {
        compileSdkVersion 18
        buildToolsVersion "18.1"

        signingConfigs {
            release {
                storeFile file("keystore.keystore")
                storePassword "YOUR_KEY_PASSWORD"
                keyAlias "YOUR_KEY_ALIAS"
                keyPassword "YOUR_KEY_PASSWORD"
            }
        }

        buildTypes {
            release {
                signingConfig signingConfigs.release
            }
            debug {
                packageNameSuffix ".debug"
            }
        }

        sourceSets {
            main {
                manifest.srcFile 'AndroidManifest.xml'
                java.srcDirs = ['src']
                resources.srcDirs = ['src']
                aidl.srcDirs = ['src']
                renderscript.srcDirs = ['src']
                res.srcDirs = ['res']
                assets.srcDirs = ['assets']
            }

            instrumentTest.setRoot('tests')
        }
    }

Make sure to replace YOUR_KEY_PASSWORD and YOUR_KEY_ALIAS with the actual credentials of your keystore.

Then, to build the apk from the command-line use:

    ./gradlew build release

The signed apk will be in build/apk.

#### Using Android Studio

For Android Studio, select Import Project, navigate to the repo and select build.gradle (instead of choosing the whole folder like in Eclipse)
It should import everything properly as long as you have the build-tools and support repository installed from the SDK manager.  
Once the project is imported you can use the Build/Generate Signed APK menu entry. 

Here's a video of me building it under Windows.

<center>
    <iframe width="100%" height="600" src="//www.youtube.com/embed/Ow_R5HDYdwE" frameborder="0" allowfullscreen></iframe>
</center>

## How to translate.

Want to add a new language to dSploit or update already existing? 

Android resource files use the UTF-8 character set, so you have to use UTF-8 compatible text editor. [Notepad++] (http://notepad-plus-plus.org/) supports UTF-8, works on Windows
and is free. However, if you are modifying existing translation, you can just use github build-in editor. 

*You can use XML Syntax-Checker to check your modified XML for syntax errors. (http://www.w3schools.com/xml/xml_validator.asp)

#### Improving existing translation.

Open the translation file you want to modify (https://github.com/evilsocket/dsploit/blob/master/dSploit/res/values-XX/strings.xml) where the XX is the
short code for language. For example: Finnish is fi, Spanish is es and German is de.

Then press "Edit" button top of the translation file. Github should now open the file for editing, and you can make the changes you want.
If you need to add new lines that do not exists yet, copy them from English values.xml (https://github.com/evilsocket/dsploit/blob/master/dSploit/res/values/strings.xml) and
paste them inside the file you are translating and then translate them.

When you are done, scroll to the end of the page and write a small summary what you just did to the "commit summary". If you WANT to be more detailed
about what you just did, use the "Extended description". Using "Extended description" is not required. Then just press "Propose File Change".
You will now be directed to comparison page.  If you filled the 2 boxes earlier, you can just press "Send pull request".

Pull request will be sent to main repository, where it may/may not be accepted to dSploit.

#### Adding a new language.

Requirements:
*git installed (http://git-scm.com/)
*some git knowledge (http://rogerdudler.github.io/git-guide/)
*time.

First, fork dSploit repository to your account. You can do that by pressing "Fork" on top right corner of https://github.com/evilsocket/dsploit
Then clone the forked repository to your PC with: "git clone https://github.com/username/dsploit.git". Replace username with your username.
Now create new new folder for your translation to dsploit/dSploit/res/ called values-XX. Replace the XX with your locale code. Then paste strings.xml from values folder
to the new folder you created.

Now open the strings.xml you copied to your new values-XX folder and start translating it your language. You can use any text editor,
as long as it saves to UTF-8 character set.

After translating, use git to add the new files and folders. Use "git add *" to do that. Now you can commit the changes with "git commit".
you can see how to use git commit from the link above. Use "git push" to push the changes to your repository.

Now just create pull request to evilsocket/dsploit. To create pull request in Github, you can see this page: https://help.github.com/articles/creating-a-pull-request
