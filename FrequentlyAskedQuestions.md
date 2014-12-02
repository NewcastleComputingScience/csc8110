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


<a name="Coursework" />
### Coursework###
    
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
