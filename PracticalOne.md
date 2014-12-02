<a name="handsonlab" />
## Practical 1: Introduction to Windows Azure Virtual Machines #

---

<a name="Overview" />
## Overview ##

In this practical exercise, you will learn how to use the Windows Azure IaaS platform to provision a Linux based Virtual Machine (VM) in the cloud and manage it remotely.

If you have any questions, do not hesitate to talk to the demonstrators during practical lab sessions or on the Blackboard discussion board.

<a name="Objectives" />
### Objectives ###

In this practical session, you will: p

- Familiarise yourself with the Windows Azure management portal
- Create Linux virtual machines (VMs) in Windows Azure

<a name="Prerequisites" />
### Prerequisites ###

- Your Windows Azure trial subscription provided in the first practical session.
- SSH client software. A copy of PuTTY is available on Campus-managed machines under CS Portable Apps, but you are free to use a client of your choice.

---
 
<a name="Exercises" />
## Exercises ##

This practical session includes the following exercises:

1. [Creating a Linux Virtual Machine in Windows Azure](#Exercise1)


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
 
1. In the **Virtual Machine operating system selection** page, click **SUSE** on the left menu and select the **openSUSE 13.1** OS image from the list. Click the arrow to continue.	

	![Selecting openSUSE from the image list](Images/creating-a-vm-suse.png?raw=true)	
	 
	_Selecting openSUSE from the image list_

1. In the **Virtual Machine Configuration** page, enter a **Virtual Machine Name**.

   In the **Authentication** section, uncheck **Upload compatible ssh key for authentication** and check **Provide password**.
   
   Provide a password (use only alphanumeric characters, avoid any symbols, particularly hyphens) for the **New Password** and **Confirm Password** fields.
   
   Lastly, set the Virtual Machine **Size** to _A1_ and click **Next** to continue.
   
   >**Important:** It is not possible to recover or reset the username and password for your Virtual Machine, so it is important you make a note of these in a safe place!

	![Configuring a Custom Virtual Machine](Images/creating-a-vm-configuration.png?raw=true)	
	 
	_Creating a Virtual Machine - Configuration_
 
	>**Note:** It is suggested to use secure passwords for admin users, as Windows Azure virtual machines could be accessible from the Internet knowing just their DNS.

	>You can also read this document on the Microsoft Security website that will help you select a secure password:  [https://www.microsoft.com/security/pc-security/password-checker.aspx](https://www.microsoft.com/security/pc-security/password-checker.aspx)
	
 
1. Under **Cloud Service** page, select **Create new cloud service**.

   Under **Cloud Service DNS Name** enter a unique **DNS Name**.

   Select **Northern Europe** as your **Region/Affinity group/Virtual Network**.

	![Configuring a Custom VM, VM Mode](Images/creating-a-vm-vm-mode.png?raw=true)
	 
	_Creating a Virtual Machine - Virtual Machine Mode_
 
    > **Note:** Your DNS name must be unique across the Azure service, so yourself and another student may not use the same DNS name. A good option to ensure you pick a unique name would be to append your student number or initials at the end of your chosen DNS name.
    
1. Now, you will create the endpoints required to manage the Virtual Machine. By default, **SSH** access is enabled on **TCP** port **22**.

   You must also add an endpoint to allow **HTTP** access on **TCP** port **80**. In the **Enter or select a value** input type **HTTP**, select **TCP** as the protocol, and port **80** as both **Public Port** and **Private Port**.

   ![Adding an HTTP endpoint to a Virtual Machine](Images/adding-a-new-endpoint-http.png?raw=true "Adding a new Endpoint")

	_Adding an HTTP endpoint to a Virtual Machine_
	
1. Click the **next** button followed by the **tick** button on the next dialog to create your new Virtual Machine. In the **Virtual Machines** section of the Azure portal, you will see the Virtual Machine you created with a _provisioning_ status. Wait until it changes to _Running_ in order to continue with the following step.

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
Copyright 2014 Matthew Forshaw, Newcastle University (matthew.forshaw@ncl.ac.uk)

Copyright 2014 Microsoft. This course material is adapted from Microsoft training material licensed under the terms of the Apache License, Version 2.0. The terms of this license can be found in http://www.apache.org/licenses/LICENSE-2.0.
