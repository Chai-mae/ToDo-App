 **<h1  >ToDo App</h1>**





**<h2>Table of contents</h2>**

   [Introduction](#Introduction)
   
   [1-Experimenting with QHBOXLayout](#1-Experimenting-with-QHBOXLayout)
   
   [2-Nested Layouts](#2-Nested-Layouts)
    
   [3-Bug report Form](#3-Bug-report-Form)
   
   [4-Grid Layout](#4-Grid-Layout)
   
   [Conclusion](#Conclusion)
   

**<h2>Introduction</h2>**
 To create an application in Qt Designer we can work with 2 approches :the first one 'ItemBased model' which is a list widget provided by QListWidget.Those widgets can inherits anything  from the QListWidgetItem class.The second one  is MVC model or "pattern" which stands for Model View Controller  .It is an application design model used for developing modern user interfaces and  comprised of three interconnected parts. They include the model (data), the view (user interface), and the controller (processes that handle input).
 In our Tp we will work on ToDoApp which is an  application that  manage  and store an archive of all the pending and finished tasks . It includes all the features of main application : menues, actions and toolbar. This app is developed with both approaches.
 
 **<h2>ItemBased Model</h2>**
  The main application contains a menuBar that is composed of :File,Options and Help each one of the three has its own components .
  Here is a little preview:
  ![WhatsApp Image 2022-01-23 at 01 24 10 (3)](https://user-images.githubusercontent.com/93831197/150659978-00fd1e12-c87e-43f0-ac5a-46fde7901f58.jpeg)![WhatsApp Image 2022-01-23 at 01 24 10 (4)](https://user-images.githubusercontent.com/93831197/150659981-0000ca27-d016-4752-b17b-ca96206f3f10.jpeg)![WhatsApp Image 2022-01-23 at 01 24 10 (5)](https://user-images.githubusercontent.com/93831197/150659987-a212c232-be1d-410a-8396-9632ae63284a.jpeg)
  
  A toolBar that holda shortcut of some functionalities:
  
  ![Capture d’écran (811)](https://user-images.githubusercontent.com/93831197/150660043-b68bc32e-2a92-453b-8a4e-f60ed0beb9d2.png)
  
  And also a main window  where we can have a look on today ,pending   and finished tasks.
  When you click on the button of adding a task a dialog is displayed and it is composed of the description label  where we describe our tasks then the tag where we choose betwween Life ,Work and other ,also the due date which manage the place of the three list widgets but if we click on the checkbox button (finished )it s automatically setted to the place of finished tasks 
  
![WhatsApp Image 2022-01-23 at 01 46 02](https://user-images.githubusercontent.com/93831197/150660275-7ef54a01-3892-4e44-8d79-6e2d8da2c795.jpeg)

![WhatsApp Image 2022-01-23 at 01 24 10 (1)](https://user-images.githubusercontent.com/93831197/150660119-3011b330-1caa-4fd3-8dfd-1266fb5df81e.jpeg)![WhatsApp Image 2022-01-23 at 01 24 10](https://user-images.githubusercontent.com/93831197/150660121-045013ff-73a7-408c-98ff-08b3d77c7d6a.jpeg)![WhatsApp Image 2022-01-23 at 01 24 10 (2)](https://user-images.githubusercontent.com/93831197/150660125-39f0fd29-fb5b-44ac-b1e0-f4e37a535772.jpeg)
 

