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
    
#### How can I use Azure SDK for Java in my Java project using Maven? ####

Add the following dependency to your pom.xml.

    <dependency>
        <groupId>com.microsoft.windowsazure</groupId>
        <artifactId>microsoft-windowsazure-api</artifactId>
        <version>0.4.6</version>
    </dependency>

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

#### JSP and Servlets ####
A few students have contacted us who have little previous experience developing web applications, but are confident in Java and would like advice on which technologies to use when developing their web application. Rebecca has prepared the following guide, including links to some useful resources, which you may find helpful.

> Here is a quick guide on using JSP and servlet technologies to create a web application. The steps below and the resources that are given will allow you to make a JSP page and a servlet to run in your server in the application layer. I would suggest reading through all the material given before starting if you are new to this.

> 1) create a simple form based JSP so you can enter information about customers or orders, think about what information needs to be added to your database (these forms are very similar to PHP and HTML, if you have used this before).

> The following links should help:

> http://www.tutorialspoint.com/jsp/jsp_form_processing.htm

> http://apekshit.com/t/56/Writing-JSP-in-Eclipse

> 2) a servlet is used to take the data from the form and then run the correct query, so if you are adding a customer the details of that customer are what is passed to the query. The servlet allows for application logic to be preformed so it is not confused with the visualisation of the website. Servlets are written in java and will allow you to use the java table storage code in them. The servlet identifies which code is to be executed by looking at the parameter string of the URL. It does this by using the HTTP request and response objects.

> 3) The code must be built into a war. It is the .war file that you will place into the application server and that will allow you to access the web application from the browser (the link below will explain this in more detail)

> http://docs.oracle.com/cd/E19316-01/820-3748/aduvz/index.html

> This link provides servlet information AND the last point shows how to create a war file, there are examples for your local machine which is fine for testing but you will need to upload the war file to run it on your azure vm.
> http://www.vogella.com/articles/EclipseWTP/article.html
