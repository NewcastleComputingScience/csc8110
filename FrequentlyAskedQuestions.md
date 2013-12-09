## CSC8110 - Frequently Asked Questions #

---

<a name="Overview" />
## Overview ##

This page will be updated regularly by CSC8110 demonstrators to include answers to frequently asked questions and solutions to any issues encountered by students.

If you are encountering an issue and cannot find a solution here, please do not hesitate to contact a demonstrator during the practical sessions, or post to the relevant forum on the Blackboard discussion boards.

If there is something you would like to appear on this page, don't hesitate to contact Matthew Forshaw (m.j.forshaw@ncl.ac.uk) and he will do his best to update the page accordingly.

---

<a name="PracticalOne" />
### Practical One ###

<a name="PracticalTwo" />
### Practical Two ###

<a name="Coursework" />
### Coursework###

#### Which Jar file to I need for Azure Table Storage? ####
A number of you have encountered issues locating the correct Jar file required for the Azure Table Storage SDK in Java.

This can be located at the following URL.

    http://go.microsoft.com/fwlink/?linkid=253887&clcid=0x409
    
#### How can I use Azure SDK for Java in my Java project using Maven ####

Add the following dependency to your pom.xml.

    ````Linux
    <dependency>
        <groupId>com.microsoft.windowsazure</groupId>
        <artifactId>microsoft-windowsazure-api</artifactId>
        <version>0.4.6</version>
    </dependency>
    ````

#### Running JBoss on an Azure VM ####
A number of students have encountered problems viewing their JBoss applications remotely, with JBoss running on their Azure VMs. To get JBoss running correctly on your VM you should

- Ensure an endpoint is set up using the TCP protocol, pointing from port 80, to port 8080 on the server.
- When you start up your server you should ensure it binds to port *0.0.0.0* to ensure it is accessible externally, as follows...

    ````Linux
    sh bin/standalone.sh -b 0.0.0.0
    ````
    
  or, for Windows...

    ````Linux
    standalone.bat -b 0.0.0.0
    ````
