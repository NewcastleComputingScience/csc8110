<a name="handsonlab" />
## Practical 2: Getting started with Windows Azure HDInsight #

---

<a name="Overview" />
## Overview ##

HDInsight Service makes [Apache Hadoop](http://hadoop.apache.org/) available as a service in the cloud. It makes the MapReduce software framework available in a simpler, more scalable, and cost efficient Windows Azure environment. HDInsight also provides a cost efficient approach to the managing and storing of data. HDInsight Service uses Windows Azure Blob Storage as the default file system.

In this practical exercise, you will learn how to provision an HDInsight cluster using the Windows Azure Management Portal and run a Hadoop MapReduce job using PowerShell.

If you have any questions, do not hesitate to talk to the demonstrators during practical lab sessions or on the Blackboard discussion board.

<a name="Objectives" />
### Objectives ###

In this practical session, you will: 

- Configure your development machine with PowerShell and required Azure modules.
- Learn how to provision an HDInsight cluster using the Windows Azure Management Portal
- Run a Hadoop MapReduce job using PowerShell.

<a name="Prerequisites" />
### Prerequisites ###

- Your Windows Azure trial subscription provided in the first practical session.
- A computer that is running Windows 8, Windows 7, Windows Server 2012, or Windows Server 2008 R2.

---
 
<a name="Exercises" />
## Exercises ##

This practical session includes the following exercises:

1. [Set up local environment for running PowerShell](#Exercise1)

1. [Provision an HDInsight cluster](#Exercise2)

1. [Run a WordCount MapReduce program](#Exercise3)

---

<a name="Exercise1" />
### Excercise 1: Set up local environment for running PowerShell ###

In this exercise, you will use PowerShell Tools for Windows Azure HDInsight to run a MapReduce job. It requires the following configuration steps:

1. install the Windows Azure module for Windows PowerShell

1. install PowerShell Tools for Windows Azure HDInsight

1. configure connectivity to your Windows Azure account

For more information, see [Install and Configure PowerShell for HDInsight](http://www.windowsazure.com/en-us/manage/services/hdinsight/install-and-configure-powershell-for-hdinsight/).
	
<a name="Ex1Task1" />
#### To install Windows Azure PowerShell ####

1. Open Internet Explorer, and browse to the [Windows Azure Downloads](http://www.windowsazure.com/en-us/manage/downloads/) page.
1. Under Windows downloads in the Command line tools section, click Windows Azure PowerShell, and then follow the instructions.



<a name="Ex1Task2" />
#### To install and import the PowerShell Tools for Windows Azure HDInsight ####

1. Open Internet Explorer, and then browse to [Microsoft .NET SDK for Hadoop](http://go.microsoft.com/fwlink/?linkid=325563&clcid=0x409) to download the package.
1. Click Run from the bottom of the page to run the installation package.
1. Open Windows Azure PowerShell. For instructions of opening a Windows Azure PowerShell console window, see Install and Configure PowerShell for HDInsight.

Your Windows Azure subscription information is used by the cmdlets to connect to your account. This information can be obtained from Windows Azure in a publishsettings file. The publishsettings file can then be imported as a persistent local config setting that the command-line interface will use for subsequent operations. You only need to import your publishsettings once.

>**Note:** The publishsettings file contains sensitive information. It is recommended that you delete the file or take additional steps to encrypt the user folder that contains the file. On Windows, modify the folder properties or use BitLocker.
	
	
<a name="Ex1Task3" />
#### To download and import publishsettings ####

1. Sign in to the [Windows Azure Management Portal](https://manage.windowsazure.com/) using the credentials for your Windows Azure account.
1. Open Windows Azure PowerShell. For instructions of opening Windows Azure PowerShell console window, see [Install and Configure PowerShell for HDInsight](http://www.windowsazure.com/en-us/manage/services/hdinsight/install-and-configure-powershell-for-hdinsight/).
1. Run the following command to download the publishsettings file.
	
	````Linux
	Get-AzurePublishSettingsFile
	````	
The command opens an Internet Explorer window and a web page. The URL is https://manage.Windowsazure.com/publishsettings/index?client=powershell.
1. When prompted, download and save the publishing profile and note the path and name of the .publishsettings file. This information is required when you run the Import-AzurePublishSettingsFile cmdlet to import the settings. The default location and file name format is:

	````Linux
	C:/Users/<UserProfile>/Desktop/[MySubscription-…]-downloadDate-credentials.publishsettings
	````
1. From the Windows Azure PowerShell window, run the following command to import the publishsettings file:

	````Linux
	Import-AzurePublishSettingsFile <PublishSettings-file>
	````

   For example:

	````Linux
	Import-AzurePublishSettingFile "C:\Users\JohnDole\Desktop\Azure-8-30-2013-credentials.publishsettings"
	````

1. Once the file is imported, you can use the following command to list your subscriptions:

	````Linux
	Get-AzureSubscription
	````

1. When you have multiple subscriptions, you can use the following command to make a subscription the current subscription:

	````Linux
	Select-AzureSubscription -SubscriptionName <SubscriptionName>
	````



---

<a name="Exercise2" />
### Exercise 2: Provision an HDInsight cluster ###
### Important: Skip this exercise! Please check your emails for the HDInsight cluster details to use for Exercise 3. ###

The HDInsight provision process requires a Windows Azure Storage account to be used as the default file system. The storage account must be located in the same data center as the HDInsight Service compute resources. Currently, you can only provision HDInsight clusters in the following data centers:

* US East
* US West
* Europe North

You must choose the __Europe North__ data centers for your Windows Azure Storage account.


<a name="Ex2Task1" />
#### To create a Windows Azure Storage account ####

1. Sign in to the Windows Azure Management Portal.

1. Click __NEW__ on the lower left corner, point to __DATA SERVICES__, point to __STORAGE__, and then click __QUICK CREATE__.


  ![Create Storage Account](Images/hdi.storageaccount.quickcreate.png?raw=true)

  _Create Storage Account_
  
1. Enter __URL__ and __LOCATION/AFFINITY GROUP__, and then click __CREATE STORAGE ACCOUNT__. You will see the new storage account in the storage list.

1. Wait until the __STATUS__ of the new storage account is changed to Online.

1. Click the new storage account from the list to select it.

1. Click __MANAGE ACCESS KEYS__ from the bottom of the page.

1. Make a note of the __STORAGE ACCOUNT NAME__ and the __PRIMARY ACCESS KEY__. You will need them later in the tutorial.

For the detailed instructions, see [How to Create a Storage Account](http://www.windowsazure.com/en-us/manage/services/storage/how-to-create-a-storage-account/) and [Using Windows Azure Blob Storage with HDInsight](http://www.windowsazure.com/en-us/manage/services/hdinsight/howto-blob-store/).

	

<a name="Ex2Task2" />
#### To provision an HDInsight cluster ####

1. Sign in to the Windows Azure Management Portal.

1. Click __HDInsight__ on the left to list the status of the clusters in your account. In the following screenshot, there is no existing HDInsight cluster.

  ![Create HDInsight](Images/hdi.clusterstatus.png?raw=true)

  _Create HDInsight_
  
1. Click __NEW__ on the lower left side, click Data Services, click __HDInsight__, and then click __Quick Create__.

  ![Quick Create HDInsight](Images/hdi.quickcreatecluster.png?raw=true)

  _Quick Create HDInsight_
  
1. Enter or select the following values:

   * __Cluster Name:__ Name of the cluster
   * __Cluster Size:__ Number of data nodes you want to deploy. The default value is 4. But 8, 16 and 32 data node clusters are also available on the dropdown menu. Any number of data nodes may be specified when using theCustom Createoption. Pricing details on the billing rates for various cluster sizes are available. Click the?symbol just above the dropdown box and follow the link on the pop up.
   * __Password (cluster admin):__ The password for the accountadmin. The cluster user name is specified to be "admin" by default when using the Quick Create option. This can only be changed by using the __Custom Create__ wizard. The password field must be at least 10 characters and must contain an uppercase letter, a lowercase letter, a number, and a special character.
   * __Storage Account:__ Select the storage account you created from the dropdown box. Once as Storage account is chosen, it cannot be changed. If the storage account is removed, the cluster will no longer be available for use. The HDInsight cluster location will be the same as the storage account.

   
1. Click __Create HDInsight Cluster__ on the lower right. The cluster is now provisioned and when it will be available when its status is listed as Running.

For information on using the __CUSTOM CREATE__ option, see Provision [HDInsight Clusters](http://www.windowsazure.com/en-us/manage/services/hdinsight/provision-hdinsight-clusters/).
  
---

<a name="Exercise3" />
### Exercise 3: Run a WordCount MapReduce job ###

Now you have an HDInsight cluster provisioned. The next step is to run a MapReduce job to count words in an input file. The following diagram illustrates how MapReduce works for the word count scenario:

  ![Word Count Diagram](Images/hdi.wordcountdiagram.gif?raw=true)

  _Word Count Diagram_

The output is a set of key-value pairs. The key is a string that specifies a word and the value is an integer that specifies the total number of occurrences of that word in the text. This is done in two stages. The mapper takes each line from the input text as an input and breaks it into words. It emits a key/value pair each time a work occurs of the word followed by a 1. The reducer then sums these individual counts for each word and emits a single key/value pair containing the word followed by the sum of its occurrences.

Running a MapReduce job requires the following elements:

* __A MapReduce program.__ In this tutorial, you will use the WordCount sample that comes with the HDInsight cluster distribution so you don't need to write your own. It is located on */example/jars/hadoop-examples.jar*. For instructions on writing your own MapReduce job, see [Using MapReduce with HDInsight](http://www.windowsazure.com/en-us/manage/services/hdinsight/using-mapreduce-with-hdinsight/).
* __An input file.__ You will use */example/data/gutenberg/davinci.txt* as the input file. For information on upload files, see [How to Upload Data to HDInsight](http://www.windowsazure.com/en-us/manage/services/hdinsight/howto-upload-data-to-hdinsight/).
* __An output file folder.__ You will use */example/data/WordCountOutput* as the output file folder. The system will create the folder if it doesn't exist.

The URI scheme for accessing files in Blob storage is:

    WASB[S]://<containername>@<storageaccountname>.blob.core.windows.net/<path>


The URI scheme provides both unencrypted access with the WASB: prefix, and SSL encrypted access with WASBS. We recommend using WASBS wherever possible, even when accessing data that lives inside the same Windows Azure data center.

Because HDInsight uses a Blob Storage container as the default file system, you can refer to files and directories inside the default file system using relative or absolute paths.

For example, to access the hadoop-examples.jar, you can use one of the following options:

    wasb://<conaintername>@<storageaccountname>.blob.core.windows.net/example/jars/hadoop-examples.jar
    wasb:///example/jars/hadoop-examples.jar
    /example/jars/hadoop-examples.jar


The use of the wasb:// prefix in the paths of these files. This is needed to indicate Azure Blob Storage is being used for input and output files. The output directory assumes a default path relative to the wasb:///user/ folder.

For more information, see [Using Windows Azure Blob Storage with HDInsight](http://www.windowsazure.com/en-us/manage/services/hdinsight/howto-blob-store/).


<a name="Ex3Task1" />
#### To run the WordCount sample ####

1. Open Windows Azure PowerShell. For instructions of opening Windows Azure PowerShell console window, see [Install and Configure PowerShell for HDInsight](http://www.windowsazure.com/en-us/manage/services/hdinsight/install-and-configure-powershell-for-hdinsight/).

1. Run the following commands to set the variables.

	````Linux
	$subscriptionName = "<SubscriptionName>" 
	$clusterName = "<HDInsightClusterName>"
	````
	
1. Run the following commands to create a MapReduce job definition:

	````Linux
	$wordCountJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/hadoop-examples.jar" -ClassName "wordcount" -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"
	````
	
   The hadoop-examples.jar file comes with the HDInsight cluster distribution. There are two arguments for the MapReduce job. The first one is the source file name, and the second is the output file path. The source file comes with the HDInsight cluster distribution, and the output file path will be created at the run-time.

1. Run the following command to submit the MapReduce job:

	````Linux
	$wordCountJob = Start-AzureHDInsightJob -Cluster $clusterName  -Subscription $subscriptionName -JobDefinition $wordCountJobDefinition
	````
	
   In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job.
   
1. Run the following command to check the completion of the MapReduce job:

	````Linux
	Wait-AzureHDInsightJob -Subscription $subscriptionName -Job $wordCountJob -WaitTimeoutInSeconds 3600
	````
	
1. Run the following command to check any errors with running the MapReduce job:

	````Linux
	Get-AzureHDInsightJobOutput -Cluster $clusterName -Subscription $subscriptionName -JobId $wordCountJob.JobId -StandardError
	````
	
   The following screenshot shows the output of a successful run. Otherwise, you will see some error messages.

  ![Run MapReduce Job](Images/hdi.gettingstarted.runmrjob.png?raw=true)

  _Run MapReduce Job_
  
  
<a name="Ex3Task2" />
#### To retrieve the results of the MapReduce job ####
	
1. Open __Windows Azure PowerShell__.

1. Set the three variables in the following commands, and then run them:

	````Linux
	$subscriptionName = "<SubscriptionName>"       
	$storageAccountName = "<StorageAccountName>"   
	$containerName = "<ContainerName>"
	````
	
   The Windows Azure Storage account is the one you created earlier in the tutorial. The storage account is used to host the Blob container that is used as the default HDInsight cluster file system. The Blob storage container name usually share the same name as the HDInsight cluster unless you specify a different name when you provision the cluster.

1. Run the following commands to create a Windows Azure storage context object:

	````Linux
	Select-AzureSubscription $subscriptionName
	$storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
	$storageContext = New-AzureStorageContext –StorageAccountName $storageAccountName –StorageAccountKey $storageAccountKey
	````
	
   The *Select-AzureSubscription* is used to set the current subscription in case you have multiple subscriptions, and the default subscription is not the one to use.

1. Run the following command to download the MapReduce job output from the Blob container to the workstation:

	````Linux
	Get-AzureStorageBlobContent -Container $ContainerName -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force
	````

   The *example/data/WordCountOutput* folder is the output folder specified when you run the MapReduce job. *part-r-00000* is the default file name for MapReduce job output. The file will be download to the same folder structure on the local folder. For example, in the following screenshot, the current folder is the C root folder. The file will be downloaded to the *C:\example\data\WordCountOutput* folder.
   
1. Run the following command to print the MapReduce job output file:

	````Linux
	cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
	````
    
  ![MapReduce Job Output](Images/hdi.gettingstarted.mrjoboutput.png?raw=true)

  _MapReduce Job Output_
  
   The MapReduce job produces a file named part-r-00000 with the words and the counts. The script uses the findstr command to list all of the words that contains "there".

> Note: If you open *./example/data/WordCountOutput/part-r-00000*, a multi-line output from a MapReduce job, in Notepad, you will notice the line breaks are not renter correctly. This is expected.


---

<a name='Shutdown' />
## Shutting down your HDInsight cluster ##

The HDInsight cluster you have created as part of this practical session comprises a number of very high-performance VM instances, and consequently is charged at a high hourly rate. As a business or individual using MapReduce on Windows Azure, you would provision your HDInsight cluster only when it is in use, and shut down (deprovision) the cluster when it is not in use. At the end of the practical session, you can shut down your HDInsight machine by pressing the **Delete** button in your cluster's **Dashboard**.

---


<a name='Summary' />
## Summary ##

In this practical session, you have learnt how to use the Windows Azure IaaS platform to provision Linux based Virtual Machines in the cloud and manage it remotely.

---

<a name='Acknowledgements' />
## Acknowledgements ##
Copyright 2013 Matthew Forshaw, Newcastle University (m.j.forshaw@ncl.ac.uk)

Copyright 2012 Microsoft. This course material is adapted from Microsoft training material licensed under the terms of the Apache License, Version 2.0. The terms of this license can be found in http://www.apache.org/licenses/LICENSE-2.0.
