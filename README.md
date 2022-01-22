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
  
  A toolBar that holda shortcut of some functionalities:
  
  And also a main window  where we can have a look on today ,pending   and finished tasks.
  When you click on the button of adding a task a dialog is displayed and composed of the description label  where we describe our tasks then the tag where we chosose betwween Life ,Work and other ,also the due date which manage the place of the three list widgets but if we click on the checkbox button (finished )it s automatically setted to finished tasks 
 

