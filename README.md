CSC8110 Cloud Computing
=======
 
### Practical Sessions ###

[Practical One - Introduction to Windows Azure Virtual Machines (Linux)](PracticalOne.md)

[Practical Two - How to use Table Storage from Java](PracticalTwo.md)

---

In your implementation you have a choice of whether to make use of Azure Queue Storage (as part of the Storage technologies offered by Azure), or to use Service Bus queues. 

A comparison of each technology may be found at [Azure Queues and Service Bus Queues - Compared and Contrasted](http://msdn.microsoft.com/en-us/library/azure/hh767287.aspx). 

For Azure Queue storage, use Practical Three:

[Practical Three - How to use Queue Storage from Java](PracticalThree.md)

For Service Bus Queues follow Practicals Four and Five:

[Practical Four - How to Use Service Bus Queues](PracticalFour.md)

[Practical Five - How to Use Service Bus Topics/Subscriptions](PracticalFive.md)

__Important:__ There is a reported authentication issue with Service Bus Queues created within the Azure Management Portal website. Many of the SDKs only support 'ACS tokens' for authentication but this is a deprecated method for all newly created Service Bus Queues created in the Azure Management Portal website. 

__Workaround:__ Service Bus Queues created using the [Azure Cross-Platform Command-Line Interface](http://azure.microsoft.com/en-gb/documentation/articles/xplat-cli/) are compatible with ACS token authentication so will work for non-.Net Azure SDKs.

__Suggestion:__ Service Bus Queues offer a number of very useful features over normal Queue Storage (see [here](http://msdn.microsoft.com/en-us/library/azure/hh767287.aspx)). However, given the current state of the Azure technology and their supporting SDKs, I am more than happy for people to use whichever queue technology they prefer. If you manage to get Service Bus Queues working with your chosen programming language, great, but don't worry if you find yourself having to fall back to using Queue Storage. If you have any further questions about this aspect of the coursework please don't hesitate to contact me by email.

---

[Practical Six: How to run a compute-intensive task in Java on a virtual machine](PracticalSix.md) (Assumes use of Service Bus Queues)

[Practical Seven: How to Use Azure SQL Database in Java](PracticalSeven.md)

N.b. Additional practical materials will appear here shortly.

---
### Coursework Assignment ###

[Coursework Document](CSC8110%20Coursework%20Assignment%202014-15.pdf)

[Presentation Slides](CSC8110%20Presentation%20Slides%202014-15.pdf)

---

### Online Resources ###

A number of useful online resources which you may find helpful in completing this coursework assignment may be found at the following link.

[Online Resources](OnlineResources.md)

---

### Frequently Asked Questions ###

A live document containing Frequently Asked Quesitons (FAQs) will be maintained at the following link. If you are encountering difficulties completing the coursework assignment, please check the following link to see if your issue has already been answered.

[Frequently Asked Questions](FrequentlyAskedQuestions.md)
