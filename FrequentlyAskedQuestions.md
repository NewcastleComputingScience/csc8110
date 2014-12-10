## CSC8110 - Frequently Asked Questions #

---

<a name="Overview" />
## Overview ##

This page will be updated regularly by CSC8110 demonstrators to include answers to frequently asked questions and solutions to any issues encountered by students.

If you are encountering an issue and cannot find a solution here, please do not hesitate to contact a demonstrator during the practical sessions, or post to the relevant forum on the Blackboard discussion boards.

If there is something you would like to appear on this page, don't hesitate to contact Matthew Forshaw (matthew.forshaw@ncl.ac.uk) and he will update the page accordingly.

---

<a name="PracticalOne" />
### Practical One ###

None (yet).

---

<a name="Coursework" />
### Coursework###


#### Should the Point of Sale (POS) application also store all customers/orders locally? ####

Your Point of Sale (POS) application does _not_ need to store all customers/orders locally. Data storage may be entirely cloud-based with one exception - if someone attempts to create a customer or order while there is no working internet connection, these customer(s)/order(s) should be stored locally and an attempt made to resend them when the internet connection comes back online.

#### How can I use Apache Commons CLI in my Java project using Maven? ####

If you are using Java as your chosen language for your implementation, you are strongly encouraged to make good use of build tools such as Maven.

Add the following dependencies to your pom.xml to use the Apache Commons CLI in your Maven project.

    <dependency>
        <groupId>commons-cli</groupId>
        <artifactId>commons-cli</artifactId>
        <version>1.2</version>
    </dependency>
    
#### How can I use Azure SDK for Java in my Java project using Maven? ####

If you are using Java as your chosen language for your implementation, you are strongly encouraged to make good use of build tools such as Maven.

Add the following dependencies to your pom.xml to use the Azure SDK for Java in your Maven project.

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-management</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-management-compute</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-management-network</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-management-sql</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-management-storage</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-management-websites</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-media</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-servicebus</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-serviceruntime</artifactId>
        <version>0.6.0</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-storage</artifactId>
        <version>1.3.1</version>
    </dependency>

#### Dependencies not found when running Jar ####

A number of students encountered issues with their Maven builds saying that libraries (e.g. Commons CLI) were not recognised. Error messages when running your program from the jar may look like the following:

    Exception in thread "main" java.lang.NoClassDefFoundError: org/apache/commons/cli/Options
            at org.cloudcomputing.Main.main(Main.java:24)
    Caused by: java.lang.ClassNotFoundException: org.apache.commons.cli.Options
            at java.net.URLClassLoader$1.run(URLClassLoader.java:372)
            at java.net.URLClassLoader$1.run(URLClassLoader.java:361)
            at java.security.AccessController.doPrivileged(Native Method)
            at java.net.URLClassLoader.findClass(URLClassLoader.java:360)
            at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
            at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:308)
            at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
            ... 1 more
            
This occurs because the dependencies you specify in your pom.xml file are not on the class path when you run your application. This can easily be solved by adding the following to your pom.xml file to create a "fat jar" - a jar file containing all dependencies.

    <plugin>
      <artifactId>maven-assembly-plugin</artifactId>
      <configuration>
        <archive>
          <manifest>
            <mainClass>fully.qualified.MainClass</mainClass>
          </manifest>
        </archive>
        <descriptorRefs>
          <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
      </configuration>
      <executions>
        <execution>
          <id>make-assembly</id> <!-- this is used for inheritance merges -->
          <phase>package</phase> <!-- bind to the packaging phase -->
          <goals>
            <goal>single</goal>
          </goals>
        </execution>
      </executions>
    </plugin>

You should change ```fully.qualified.MainClass``` to the full package and class name of the default main method you wish to be called when you run your Jar file.

For more information please see the following [StackOverflow article](http://stackoverflow.com/questions/574594/how-can-i-create-an-executable-jar-with-dependencies-using-maven).

#### How should I handle dates in Java? ####

You may handle dates in your application however you see fit, but I strongly suggest making use of [Joda Time](http://www.joda.org/joda-time/) which provides a number of benefits over Java's built-in date and time support. This may be included in your project by adding the following dependency to your pom.xml file.

    <dependency>
      <groupId>joda-time</groupId>
      <artifactId>joda-time</artifactId>
      <version>2.6</version>
    </dependency>

#### What should I use as my partition key for 4.3 Management Report C? ####

Hint: [Stackoerflow article: Get the number of days, weeks, and months, since Epoch in Java](http://stackoverflow.com/questions/6158053/get-the-number-of-days-weeks-and-months-since-epoch-in-java)
