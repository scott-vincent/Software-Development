In all of the following instructions, please replace `<you>` with something sensible depending on the context!


Eclipse Neon (IDE)
============

Download from:

https://www.eclipse.org/downloads

Download the 64-bit version.  

Create the following folder:

```
C:\Program Files\Eclipse\Neon
```

Right-click the folder and select Properties. Click the Security tab, in "Group or user names" choose "Users",
then in "Permissions for Users" click Full Control and click Apply.

Start the installation by double-clicking the file you downloaded. 

Select Eclipse IDE for Java EE Developers and change the installation folder to the one you created above.
When installation is complete, click on Menu button (top-right) with the exclamation mark on it and choose Update.
Launch Eclipse and change the workspace to:

```
C:\Users\<you>\workspace_java
```

You can tick the box to always use this workspace.
When the Eclipse IDE loads, just quit.


Java 8 Development Kit (JDK)
======================

Download from: 

http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

Choose the Windows x64 version.
Run the installation by double-clicking the file you downloaded. 

You need to create an environment variable to tell your system where Java is installed. You do this as follows:

Either use the windows search box and search for "Edit environment variables for your account"
or right-click Start menu ->  System -> System info -> Advanced system settings -> Environment Variables.

Add a new variable called "JAVA_HOME" and set it to "C:\Program Files\Java\jdk1.8.0_131".


Maven (Build Control)
=====

Download from:

https://maven.apache.org/download.cgi 

Choose the Binary zip archive.
Unzip to C:\ so you end up with:

```
C:\apache-maven-3.5.0
```

You need to create an environment variable to tell your system where JMaven is installed
and to be able to run it from the command line. You do this as follows:

Either use the windows search box and search for "Edit environment variables for your account"
or right-click Start menu ->  System -> System info -> Advanced system settings -> Environment Variables.

Add a new variable called "MAVEN_HOME" and set it to "C:\apache-maven-3.5.0".

Edit existing variable "PATH" and add "%MAVEN_HOME%\bin".


Git (Source Code Control)
===

Download from: 

https://git-scm.com

Click on Downloads for Windows and the download should start.
Run the installation by double-clicking the file you downloaded. 
Choose all the default options.


GitHub (Source Code in the Cloud)
======

Go to:

https://github.com/

and register to create your own account (my username is scott-vincent).


Validate Environment
====================

Make sure you set everything up correctly. Run a Command Prompt and try the following:

```
java -version
mvn --version
git --version
```

Getting Started (Your first Java program)
===============

Let's start by seeing what Maven does for us. We won't use Eclipse to start with, just the command line. Later on,
we can import our project into Eclipse using the "Import existing Maven project into Eclipse" menu option.

It can create a project structure for you and get you started. Run a command prompt and do the following:

```
cd c:\users\<you>
mkdir "Java Programs"
cd Java Programs
mvn archetype:generate -DgroupId=com.<you> -DartifactId=my-first-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

This has created a directory for you and put some dummy code in it. Use Windows Explorer to examine it.
It created a Java source file for you:

```
C:\Users\<you>\Java Programs\my-first-app\src\main\java\com\<you>\App.java
```

Maven also created a pom (build file) for you:

```
C:\Users\<you>\Java Programs\my-first-app\pom.xml
```

Have a look at the pom file. It tells Maven how to build your program. If your program relies on external JAR files (similar to Python modules), there will be lines in the pom file telling it where to download them from and which version your program needs.

For a fuller description of what Maven does see here: https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html   

Note that the pom file includes a dependency called junit. This is a module that runs the unit tests you write alongside your code.
Whenever you write source code you should also write unit test code. This gets run everytime you build your source and confirms
that the source is functioning as you intended. Your unit test code is here:

```
C:\Users\<you>\Java Programs\my-first-app\src\test\java\com\<you>\AppTest.java 
```

Now let's compile and run your App.java source.

```
cd C:\Users\<you>\Java Programs\my-first-app
mvn clean install
```

This should compile your app.java and create a JAR file for you. Note that a JAR file is just a zip file in disguise. You can
load a JAR file into 7-zip to unzip it and see what it contains.

The JAR file should be here: C:\Users\`<you>`\Java Programs\my-first-app\target\my-first-app-1.0-SNAPSHOT.jar

Notice that the JAR file contains com/`<you>`/App.class. This is the compiled version of App.java.
Also notice the structure. All your source starts with com.`<you>`. This is called the package name in Java.
You will see it in your source file. All external JAR files (modules) have a similar structure so that everything can be kept
tidy inside a single JAR file. E.g. Look at a JAR file supplied by Microsoft and all the files inside it will start with
com.microsoft.*

You can now run this JAR file using java:

```
cd C:\Users\<you>\Java Programs\my-first-app\target
java -cp my-first-app-1.0-SNAPSHOT.jar com.<you>.App
```
  
It would be simpler to run it if you had a manifest file inside the JAR file. Try doing this:

```
java -jar my-first-app-1.0-SNAPSHOT.jar
```
  
You will see it complains. See if you can work out how to modify your pom file to make it include a manifest file in your JAR.
All it basically needs to know is the entry point for your program, i.e. com.`<you>`.App

For a big hint, go here: http://www.avajava.com/tutorials/lessons/how-do-i-specify-a-main-class-in-the-manifest-of-my-generated-jar-file.html  


Exercise 1 - Using Eclipse IDE
===========

Try loading your project into Eclipse because the IDE will give you hints and help you when you write your source.
Use File -> Import -> Maven -> Existing Maven Projects  

Use the Project Explorer to examine your files. Double click your App.java file to load it into the IDE's editor.

See if you can get it to build and run inside Eclipse. You will probably find that Build Automatically is enabled so
your project gets built whenever you edit your source and press Ctrl S (save). It builds very quickly so you may not
even notice!


Exercise 2 - Using external JAR files
===========

"Don't re-invent the wheel"

If you need a module that does some vaguely standard sort of thing, somebody has already been there before and done it for you!
Search for what you need on GitHub, there will be many versions doing similar things so try the one that looks good to you, or try them all.
Things you might want to consider when choosing are:

```
Does the license (if there is one) give you the freedom you need and is it approved by the company you work for?
How long has the module been around?
Has it had many updates (bug fixes)?
Are there many outstanding issues?
Are there multiple contributers? (more can quite often mean better tested, more bug-free code)
Is it generally well-received by the community? 
```

If in doubt, just try it and see if it does what you need (or maybe you can modify it to suit your needs).

Somebody has written a Java package to calculate sunrise/sunset times for a particular location and date.
See if you can call it from your App.java.

The instructions are here: https://github.com/mikereedell/sunrisesunsetlib-java  

Note that you don't need to download or build his code. All you need to do is add the relevant bit (shown below) to your pom
file. This will download his JAR file and include it in your project automatically!

```
<dependency>
  <groupId>com.luckycatlabs</groupId>
  <artifactId>SunriseSunsetCalculator</artifactId>
  <version>1.2</version>
</dependency>
```

Note that you can edit your pom.xml file directly in Eclipse by double clicking it and choosing the pom.xml tab at the bottom.
After editing any file in Eclipse remember to press Ctrl S to save it. 

Whenever you edit your pom you will need to do the following in Eclipse:

Right-click your project name (my-first-app) in the Project Explorer windows and select Maven -> Update Project  

Now work out how to modify your App.java code to show sunrise/sunset times for Crowthorne.


Exercise 3 - Using Git
==========  

I've done the exercise above and checked my source code into the cloud (GitHub).
You can retrieve my code using Git. Then you can load it into Eclipse and examine/run it.

Do the following:

```
cd C:\Users\<you>\Java Programs
git clone https://github.com/scott-vincent/CrowthorneSun.git
```

You now have a copy of my source in: C:\Users\`<you>`\Java Programs\CrowthorneSun  

Load the project into Eclipse:

```
File -> Import -> Maven -> Existing Maven Projects
```

Examine it using the project explorer and press the Run button to run it. 


Exercise 4 - Using GitHub
==========  

You can see my source in the cloud using GitHub.
 
Go here: https://github.com/scott-vincent

Click on my CrowthorneSun repository.
You can examine all the files using the web interface.
 
GitHub lets you grab a copy of anybody's source (all source is public by default, you have to pay if you want to store code privately!).
Click the "Clone or download" button and it gives you the URL that you used in the previous exercise with the "git clone" command.
 
Now you are going to add your own code to GitHub.

First, use the web interface to create a new repository.
Login to GitHub and click the Repositories tab, then the New button.
Name your repository, e.g. my-first-app and click Create repository.

GitHub will then display some helpful instructions. You want to "create a new repository on the command line" so do
the following in the Windows command prompt:

```
cd C:\Users\<you>\Java Programs\my-first-app
git init
git add pom.xml
git add src\main\java\com\<you>\App.java
git add src\test\java\com\<you>\AppTest.java
git commit -m "My first commit"
git remote add origin https://github.com/<your-name>/my-first-app.git
git push -u origin master
```

Now look at your repository in GitHub using the web interface. You should see the 3 source files you added.


Exercise 5 - Java Classes and Unit Tests
==========

Download the FamilyCars application from GitHub by doing the following:

```
cd C:\Users\<you>\Java Programs
git clone https://github.com/scott-vincent/FamilyCars.git
```

Import it into Eclipse and run it. The output is incorrect due to a bug.
Examine the source to understand what the bug is and then fix it. The correct output should look like this:

```
Family Cars
-----------
Ford Focus owned by Scott Vincent
Honda Jazz owned by Clare Vincent
Honda Jazz driven by Ross Vincent
```

Run the unit tests in Eclipse. One of them will fail due to the above bug. Click on the Assert failure to see
the expected result and the actual result.

If you run the build on the command line it always runs the unit tests. Try it:

```
cd C:\Users\<you>\Java Programs\FamilyCars
mvn clean install
```

Fix the unit test so that it no longer fails.


Exercise 6 - Spring Boot
==========

You are now ready to do some serious development!

All the best projects these days involve Web Services. This is so that anybody (or even multiple users) can access your application from anywhere.
All they need is a web browser. They don't need to download or install anything, they just point their browser at your URL and off they go.

There are two main parts to a Web-based application. The back-end that runs on the server and the front-end (User Interface or UI) that runs in the web browser.
The back-end may also access other services/databases running on the same or possibly different servers.

We are going to write the front-end in JavaScript and the back-end in Java. But we want to do it fast, and we certainly don't want to re-invent the wheel.

What if there was some super-duper frameworks where somebody has already done all the hard-work for us, making it super easy for us so we only have to write
the actual app-specific code and not have to worry about wiring up the front-end to the back-end, converting to and from serialised to internal object formats
(so data can be transferred over the internet), configuring our web-service, manipulating the DOM, etc. etc. etc.

Introducing Spring Boot (back-end Java) and AngularJS (front-end JavaScript).

If you want to know what these can do for you, have a look here:

Spring Boot: https://projects.spring.io/spring-boot/  
AngularJS: https://angularjs.org/  

All 'modern' web services generally involve REST and JSON. Find out more about them here:

REST: https://en.wikipedia.org/wiki/Representational_state_transfer  
JSON: https://en.wikipedia.org/wiki/JSON  

Let's start with Spring Boot to see how easily we can create a RESTful back-end web server. 

Download gs-rest-service from GitHub by doing the following:

```
cd C:\Users\<you>\Java Programs
git clone https://github.com/scott-vincent/gs-rest-service.git
```

Import it into Eclipse and examine the source.

There are only 3 small source files (and a unit tests file):

Application.java - Basically, just a single line that starts the Spring Boot application  
Greeting.Java - This is the class that gets serialised into JSON format and returned by our web server.  
GreetingController.java - This defines our REST methods. There is only one called "/greeting".  

and that's it!!

Now run it. The first time, you may have to right-click on "src/main/java" within the project and choose "Run as -> Java Application -> SpringApplication".
After that, you can just click the green play icon  in the top menu bar to run it. It is a web server so it will run forever.
To stop it, click the red stop icon on the bottom "Console" tab.
If you try to run it and it is already running, you will get error "The Tomcat connector configured to listen on port 8080 failed to start. The port may already be in use".

Remember, whenever you modify the source you will need to stop and then re-start the web server to pick up the changes.

Once it's running use your favourite web browser (e.g. Chrome) to access it.

Your web server is running on port 8080 so try typing this in the address bar:

```
localhost:8080
```

You will get an error, but if you stop the web server and try again you will get a different error so at least we know it's listening on that port!

It's a REST service so it only listens on certain endpoints. Try this:

```
localhost:8080/greeting
```

That's better, we got some JSON back. Notice in the source, that REST method has an optional "name" query parameter. Try this:

```
localhost:8080/greeting?name=Bob
```

You should have got some personalised JSON back.

The unit tests include tests for calling the greeting with and without a name. Run them and make sure they succeed.

Wow, that was super easy!
Who said software development was hard work?


Exercise 7 - AngularJS
==========
Coming soon!
