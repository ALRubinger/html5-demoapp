html5-demoapp: Testing an AeroGear Application Using Multiple HTML5, Mobile & JAX-RS Technologies with Arquillian
=================================================================================================================
Author: Jay Balunas, Karel Piwko

What is it?
-----------

This is your project! It's a deployable Maven 3 project to help you
get your foot in the door developing HTML5 based desktop/mobile web applications with Java EE 6
on JBoss. This project is setup to allow you to create a basic Java EE 6 application
using HTML5, jQuery Mobile, JAX-RS, CDI 1.0, EJB 3.1, JPA 2.0 and Bean Validation 1.0. It includes
a persistence unit and some sample persistence and transaction code to help 
you get your feet wet with database access in enterprise Java.

This application is built using a HTML5 + REST approach. This uses a pure HTML
client that interacts with with the application server via restful end-points (JAX-RS).  This
application also uses some of the latest HTML5 features and advanced JAX-RS. And since testing
is just as important with client side as it is server side, this application uses QUnit to show
you how to unit test your JavaScript.

What is a modern web application without mobile web support? This application also integrates
jQuery mobile and basic client side device detection to give you both a desktop and mobile 
version of the interface. Both support the same features, including form validation, member
registration, etc. However the mobile version adds in mobile layout, touch, and performance 
improvements needed to get you started with mobile web development on JBoss.  

Going through tutorial
----------------------

The easiest way how to go through the tutorial is to rewind it to the original application state 
and have a look what steps are done in order to make application test table.

You can rewind the application state using:

    ./git-navigator.sh rewind

Once you did the rewind, you can navigate either to a next step or to the last step:

    ./git-navigator.sh next
    ./git-navigator.sh forward

Note, you have to be on a git branch in order to rewind, it does not work in detached state.


System requirements
-------------------

All you need to build this project is Java 6.0 (Java SDK 1.6) or better, Maven
3.0 or better.

The application this project produces is designed to be run on JBoss AS 7 or JBoss Enterprise Application Platform 6.

An HTML5 compatible browser such as Chrome, Safari 5+, Firefox 5+, or IE 9+ are
required. and note that some behaviors will vary slightly (ex. validations) based on browser support,
especially IE 9.

Mobile web support is limited to Android and iOS devices.  It should run on HP,
and Black Berry devices as well.  Windows Phone, and others will be supported as 
jQuery Mobile announces support.
 
With the prerequisites out of the way, you're ready to build and deploy.

Testing requirements
--------------------

To test the application, you additionally need an Android SDK, Selenium APK application for Android  
and optionally an Android device and an account on OpenShift. If you want to test in Jenkins, 
you additionally need a Jenkins instance with XVNC plugin and a few nodes.

You can get them from following locations:

* [Android SDK](http://developer.android.com/sdk/index.html) 
* [Selenium APK](http://code.google.com/p/selenium/downloads/list)

[Register on OpenShift](http://www.openshift.com), it's free and you get your own cloud instance!


Deploying the application
-------------------------

First you need to start the JBoss container. To do this, run
  
    $JBOSS_HOME/bin/standalone.sh
  
or if you are using windows
 
    $JBOSS_HOME/bin/standalone.bat
    
Note: Adding "-b 0.0.0.0" to the above commands will allow external clients (phones, tablets, 
desktops, etc...) connect through your local network.
      
For example

    $JBOSS_HOME/bin/standalone.sh -b 0.0.0.0 

To deploy the application, you first need to produce the archive to deploy using
the following Maven goal:

    mvn package

You can now deploy the artifact by executing the following command:

    mvn jboss-as:deploy

The client application will be running at the following URL <http://localhost:8080/html5-demoapp/>.

To undeploy run this command:

    mvn jboss-as:undeploy

You can also start the JBoss container and deploy the project using JBoss Tools. See the
<a href="https://docs.jboss.org/author/display/AS71/Getting+Started+Developing+Applications+Guide" title="Getting Started Developing Applications Guide">Getting Started Developing Applications Guide</a> 
for more information.

Running the Arquillian tests
============================

By default, tests are configured to be skipped. The reason is that the sample
test is an Arquillian test, which requires the use of a container. You can
activate this test by selecting one of the container configuration provided 
for JBoss.

To run the test in JBoss, first start the container instance. Then, run the
test goal with the following profile activated:

    mvn clean test -Parq-jbossas-remote

Additionally, you have to activate a browser profile as well, according to the 
browser type you want to test.

    mvn clean test -Parq-jbossas-remote,webdriver-chrome

Running the QUnit tests
============================

QUnit is a JavaScript unit testing framework used and built by jQuery. This 
application includes a set of QUnit tests in order to verify JavaScript that
is core to this HTML5 application. Executing QUnit test cases is quite easy. First,
make sure the server is running and the project has been deployed as some of the
tests will be testing the functionality of the services. Then, simply load the
following HTML in the browser you wish to test.

    <project-root>/src/test/qunit/index.html

For more information on QUnit tests see http://docs.jquery.com/QUnit

Importing the project into an IDE
=================================

If you created the project using the Maven archetype wizard in your IDE
(Eclipse, NetBeans or IntelliJ IDEA), then there is nothing to do. You should
already have an IDE project.

Detailed instructions for using Eclipse / JBoss Tools with are provided in the 
<a href="https://docs.jboss.org/author/display/AS71/Getting+Started+Developing+Applications+Guide" title="Getting Started Developing Applications Guide">Getting Started Developing Applications Guide</a>.

If you created the project from the command line using archetype:generate, then
you need to import the project into your IDE. If you are using NetBeans 6.8 or
IntelliJ IDEA 9, then all you have to do is open the project as an existing
project. Both of these IDEs recognize Maven projects natively.

Downloading the sources and Javadocs
====================================

If you want to be able to debug into the source code or look at the Javadocs
of any library in the project, you can run either of the following two
commands to pull them into your local repository. The IDE should then detect
them.

    mvn dependency:sources
    mvn dependency:resolve -Dclassifier=javadoc

Development notes
=================

Copyright headers
-----------------

To update the copyright headers, just run `mvn license:format -Dyear=<current year>`

