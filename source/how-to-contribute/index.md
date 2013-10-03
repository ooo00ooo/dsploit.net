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