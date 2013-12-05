<a name="handsonlab" />
## Practical 1: Introduction to Windows Azure Virtual Machines #

---

<a name="Overview" />
## Overview ##

In this practical exercise, you will learn how to use the Windows Azure IaaS platform to provision a Linux based Virtual Machine (VM) in the cloud and manage it remotely.

If you have any questions, do not hesitate to talk to the demonstrators during practical lab sessions or on the Blackboard discussion board.

<a name="Objectives" />
### Objectives ###

In this practical session, you will: 

- Familiarise yourself with the Windows Azure management portal
- Create Linux virtual machines (VMs) in Windows Azure
- Install and configure an Apache web server with MySQL 
- Install and configure Drupal CMS

<a name="Prerequisites" />
### Prerequisites ###

- Your Windows Azure trial subscription provided in the first practical session.
- SSH client software. A copy of PuTTY is available on Campus-managed machines under CS Portable Apps, but you are free to use a client of your choice.

---
 
<a name="Exercises" />
## Exercises ##

This practical session includes the following exercises:

1. [Creating a Linux Virtual Machine in Windows Azure](#Exercise1)

1. [Installing and Configuring the Virtual Machine](#Exercise2)

1. [Installing and Configuring Drupal](#Exercise3)


---

<a name="Exercise1" />
### Exercise 1: Creating a Linux Virtual Machine in Windows Azure ###

In this exercise, you will learn how to provision a Linux Virtual Machine in the Azure portal.
	
<a name="Ex1Task1" />
#### Task 1 - Creating a New Linux Virtual Machine ####

1. Open Internet Explorer and browse [https://manage.windowsazure.com](https://manage.windowsazure.com) to enter the Windows Azure portal. Then, log in with your credentials.
1. In the menu located at the bottom, select **Compute** | **New Virtual Machine | From Gallery** to start creating a new virtual machine.
	 
	![Creating a new Virtual Machine](Images/creating-a-new-virtual-machine.png?raw=true)

	_Creating a new Virtual Machine_
 
1. In the **Virtual Machine operating system selection** page, click **SUSE** on the left menu and select the **openSUSE 12.3** OS image from the list. Click the arrow to continue.	

	![Selecting openSUSE from the image list](Images/creating-a-vm-suse.png?raw=true)	
	 
	_Selecting openSUSE from the image list_

1. In the **Virtual Machine Configuration** page, enter a **Virtual Machine Name**.

   In the **Authentication** section, uncheck **Upload compatible ssh key for authentication** and check **Provide password**.
   
   Provide a password for the **New Password** and **Confirm Password** fields.
   
   Lastly, set the Virtual Machine **Size** to _Small_ and click **Next** to continue.
   
   >**Important:** It is not possible to recover or resetthe username and password for your Virtual Machine, so it is important you make a note of these in a safe place!

	![Configuring a Custom Virtual Machine](Images/creating-a-vm-configuration.png?raw=true)	
	 
	_Creating a Virtual Machine - Configuration_
 
	>**Note:** It is suggested to use secure passwords for admin users, as Windows Azure virtual machines could be accessible from the Internet knowing just their DNS.

	>You can also read this document on the Microsoft Security website that will help you select a secure password:  [http://www.microsoft.com/security/online-privacy/passwords-create.aspx](http://www.microsoft.com/security/online-privacy/passwords-create.aspx)
	
 
1. Under **Cloud Service** page, select **Create new cloud service**.

   Under **Cloud Service DNS Name** enter a unique **DNS Name**.

   Select **Northern Europe** as your **Region/Affinity group/Virtual Network**.

   Under **Storage Account** select **csc8110[number]** where *[number]* is the number associated with your account (e.g. if you log in using *"students-one"*, select storage account *"csc8110one"*.

   Click the **right arrow** to continue. 

	![Configuring a Custom VM, VM Mode](Images/creating-a-vm-vm-mode.png?raw=true)
	 
	_Creating a Virtual Machine - Virtual Machine Mode_
 
    > **Note:** Your DNS name must be unique across the Azure service, so yourself and another student may not use the same DNS name. A good option to ensure you pick a unique name would be to append your student number or initials at the end of your chosen DNS name.
    
1. Now, you will create the endpoints required to manage the Virtual Machine. By default, **SSH** access is enabled on **TCP** port **22**.

   ![Default endpoint configuration for a Virutal Machine](Images/adding-a-new-endpoint-sshonly.png?raw=true "Adding a new Endpoint")

	_Default endpoint configuration for a Virutal Machine_

   You must also add an endpoint to allow **HTTP** access on **TCP** port **80**. In the **Enter or select a value** input type **HTTP**, select **TCP** as the protocol, and port **80** as both **Public Port** and **Private Port**.

   ![Adding an HTTP endpoint to a Virtual Machine](Images/adding-a-new-endpoint-http.png?raw=true "Adding a new Endpoint")

	_Adding an HTTP endpoint to a Virtual Machine_
	
	> **Note:** This endpoint enables the port 80 that will be used by the Apache Server in the following tasks.   

1. Click the **tick** button to create your new Virtual Machine. In the **Virtual Machines** section of the Azure portal, you will see the Virtual Machine you created with a _provisioning_ status. Wait until it changes to _Running_ in order to continue with the following step.

	![Creating Linux VM](Images/creating-linux-vm.png?raw=true)
	 
	_Creating Linux Virtual Machine_

<a name="Ex1Task2" />
#### Task 2 - Verification: Connecting to the Virtual Machine by using a SSH client ####

Now that you have provisioned and configured a Linux Virtual Machine, you will connect by using an SSH client.

>**Note:** **PuTTY** SSH client is available on Campus-managed machines under **CS Portable Apps**, but you are free to use an SSH client of your choice.


1.	In the Windows Azure Portal, select the Linux Virtual Machine from the list to enter the **Dashboard**. Take note of the **SSH Details** field at the "quick glance" section, which is the public address you will use to access and connect to the virtual machine using the SSH client.

    ![SSH Endpoint](Images/ssh-endpoint.png?raw=true "SSH Endpoint")

    _SSH Endpoint_

1. Open the Putty client (or any other SSH client) and create a new connection to the Virtual Machine, using address and port from the previous step.

	![Connecting to the Linux Virtual Machine via Putty Client](Images/connecting-to-the-linux-vm-via-putty-client.png?raw=true)
	 
	_Connecting to the Linux Virtual Machine via Putty Client_

	> **Note:** You can verify the public port for the SSH connection in the **Endpoints** section of the Virtual Machine. When using Putty, make sure you enable TCP Keepalives and set it with a value greater than 5.
 
1. Use the Virtual Machine credentials to login.

	> **Note:** When completing the password, the cursor won't move

	![Logging in to the Linux Virtual Machine](Images/logging-in-to-the-linux-virtual-machine.png?raw=true)

	_Logging in to the Linux Virtual Machine_

1. Execute the following command to impersonate with **Administrator** rights.

	````Linux
	sudo su -
	````

	![Logging in with Administrator rights](Images/logging-in-with-administrator-rights.png?raw=true)

	_Logging in with Administrator rights_

---

<a name="Exercise2" />
### Exercise 2: Installing and Configuring the Virtual Machine ###

In this exercise, you will learn how to install and configure a Web Server in the Linux Virtual Machine by using a SSH client. First, you will install the Apache Web server and the MySQL database server. Then, you will configure the Virtual Machine and create an example database. 

<a name="Ex2Task1" />
#### Task 1 - Installing and Configuring Apache and MySQL ####

In this task, you will install and configure an Apache HTTP Server and MySQL Database Management System.

1. In the terminal, execute the following commands to install the required packages.

	````Linux
	zypper install -t pattern lamp_server
	````

	>**Note**: If you get the following prompt "Do you want to reject the key, trust temporarily, or trust always? [r/t/a/?]", press **A** and then **Enter**. Pattern Lamp server installs only the needed packages for Lamp server.

1. Install the following packages in order to run PHP, MySQL (MariaDB distribution) and Apache2 in openSUSE.

	````Linux
	zypper install apache2 apache2-doc apache2-mod_php5 apache2-example-pages mariadb php5-gd php-db php5-mysql php5-json php5-dom php5-mbstring 
	````

1. In order to start MySQL service, execute the following commands.

	````Linux
	systemctl enable mysql.service 
	systemctl start mysql.service
	````

1. Execute the following commands in order to start Apache too.

	````Linux
	systemctl enable apache2.service
	systemctl start apache2.service
	````

	![Starting Apache and MySQL service](Images/starting-apache-and-mysql-service.png?raw=true "Starting Apache and MySQL service")

	_Starting Apache and MySQL service_


#### Task 2 - Validating Apache and MySQL are running ####

In this task you will check the status of MySQL and Apache service.

1. If not open, open SSL client and connect to the Virtual Machine

1. Run the following command to check MySQL Service status
	
	````Linux
	service mysql status 
	````

	![MySQL Service Status](Images/mysql-service-status.png?raw=true "MySQL Service Status")

	_MySQL Service Status_

1. Run the following command to check Apache Service status
	
	````Linux
	service apache2 status 
	````

	![Apache Server Status](Images/apache-server-status.png?raw=true "Apache Server Status")

	_Apache Server Status_

1. Open **Internet Explorer** and browse the **DNS name** of the Virtual Machine to ensure apache is accessible through the Web.
	
	![Browser checking status](Images/browser-checking-status.png?raw=true "Browser checking status")

	_Apache working_

---

<a name="Exercise3" />
### Exercise 3 - Installing and Configuring Drupal ###

In this exercise, you will install and configure the Drupal CMS in the Linux virtual machine. At the end of the exercise, you will be able to host a Drupal CMS website. 

>**Note:** Before starting this exercise, make sure you have completed Exercise 2.

<a name="Ex3Task1" />
#### Task 1 - Installing and Configuring Drupal ####

In this task, you will install and configure a Drupal portal on your Windows Azure Linux Virtual Machine. Additionally, you will create an empty database to be used by Drupal CMS.

1. Open the root websites folder and create a folder named **Drupal** by executing the following.

	````Linux
	cd /srv/www/htdocs
	mkdir drupal
	cd drupal
	````

1.	Execute the following command to install **wget**. Wget is a command line tool to retrieve files using HTTP, HTTPS and FTP.
	
	````Bash
	zypper install wget
	````

1. Download and extract **Drupal**.

	````Linux
	wget http://drupal.org/files/projects/drupal-7.22.tar.gz
	tar -xzf drupal-7.22.tar.gz --strip-components=1 
	````

	![Downloading Drupal](Images/downloading-drupal.png?raw=true)

	_Downloading Drupal_

1. Copy the **default.settings.php** file, located in the **sites/default** directory, and rename the copied file to **settings.php**. Additionally, give the web server write privileges to the configuration file.

	````Linux
	cp sites/default/default.settings.php sites/default/settings.php
	chmod a+w sites/default/settings.php
	chmod a+w sites/default
	````

	![Creating the configuration file and granting permissions](Images/creating-the-configuration-file-and-granting.png?raw=true)

	_Creating the configuration file and granting permissions_

1. To complete the installation, create an empty database for **Drupal** in **MySQL**. Execute the following:

	````Linux
	mysqladmin create drupaldb
	````

1. Execute **mysql** command. At the MySQL prompt execute the following query. Replace **username** and **password** with your Virtual machine user account. This command grants permissions for your user in MySQL.

	````Linux
	GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES	
	ON drupaldb.*
	TO 'username'@'localhost' IDENTIFIED BY 'password';
	````

	![Granting permissions in MySQL](Images/granting-permissions-in-mysql.png?raw=true)

	_Granting permissions in MySQL_
	
   Exit the MySQL command prompt by typing **exit**.
	
1. Open Internet Explorer and locate the virtual machine DNS Name. Browse to _http://[YOUR-DNS-URL]/drupal_ to complete Drupal installation.
 
	![Opening Drupal for the first time](Images/opening-drupal-for-the-first-time.png?raw=true)

	_Opening Drupal for the first time_ 

	>**Note:**  You can find more details about Drupal configuration in the official documentation ([http://drupal.org/documentation/install/run-script](http://drupal.org/documentation/install/run-script)).

1. In the Set up Database page, enter the name of the database you have created in Task 1 (‘drupaldb’), and the **username** and **password**. 
	 
	![Opening Drupal for the first time(2)](Images/opening-drupal-for-the-first-time2.png?raw=true)

	_Opening Drupal for the first time_
 
1. In the **Configure site** website, enter a user name, an e-mail address and a password to create a new **site maintenance account**.

	![Configuring a Drupal account](Images/configuring-a-drupal-account.png?raw=true)
	 
	_Configuring a Drupal account_

1. Click the **Visit your new site** link to verify that the Drupal home page loads. 

	![Drupal CMS home page](Images/drupal-cms-home-page.png?raw=true)
	 
	_Drupal CMS home page_
	
---

<a name='Shutdown' />
## Shutting down your VM ##

As students on CSC8110 you have been granted six months' free access to Windows Azure. However, cloud services such as Azure's IaaS VMs are typically charged on a per-hour or per-minute basis. Therefore, it is good practice to shut down (deprovision) resources when they are not in use. At the end of the practical session, you can shut down your virtual machine by pressing the **Shut Down** button in your virtual machine's **Dashboard**.

---

<a name='Summary' />
## Summary ##

In this practical session, you have learnt how to use the Windows Azure IaaS platform to provision Linux based Virtual Machines in the cloud and manage it remotely.

---

<a name='Acknowledgements' />
## Acknowledgements ##
Copyright 2013 Matthew Forshaw, Newcastle University (m.j.forshaw@ncl.ac.uk)

Copyright 2012 Microsoft. This course material is adapted from Microsoft training material licensed under the terms of the Apache License, Version 2.0. The terms of this license can be found in http://www.apache.org/licenses/LICENSE-2.0.
