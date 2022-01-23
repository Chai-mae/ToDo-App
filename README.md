 **<h1  >ToDo App</h1>**





**<h2>Table of contents</h2>**

   [Introduction](#Introduction)
   [ItemBased Model](#ItemBased Model)
   [MVC Model](#MVC Model)
   [Conclusion](#Conclusion)
   

**<h2>Introduction</h2>**
 To create an application in Qt Designer we can work with 2 approches :the first one 'ItemBased model' which is a list widget provided by QListWidget.Those widgets can inherits anything  from the QListWidgetItem class.The second one  is MVC model or "pattern" which stands for Model View Controller  .It is an application design model used for developing modern user interfaces and  comprised of three interconnected parts. They include the model (data), the view (user interface), and the controller (processes that handle input).
 In our Tp we will work on ToDoApp which is an  application that  manage  and store an archive of all the pending and finished tasks . It includes all the features of main application : menues, actions and toolbar. This app is developed with both approaches.
 
 **<h2>ItemBased Model</h2>**
  The main application contains a menuBar that is composed of :File,Options and Help each one of the three has its own components .
  Here is a little preview:
  ![WhatsApp Image 2022-01-23 at 01 24 10 (3)](https://user-images.githubusercontent.com/93831197/150659978-00fd1e12-c87e-43f0-ac5a-46fde7901f58.jpeg)![WhatsApp Image 2022-01-23 at 01 24 10 (4)](https://user-images.githubusercontent.com/93831197/150659981-0000ca27-d016-4752-b17b-ca96206f3f10.jpeg)![WhatsApp Image 2022-01-23 at 01 24 10 (5)](https://user-images.githubusercontent.com/93831197/150659987-a212c232-be1d-410a-8396-9632ae63284a.jpeg)
  
  A toolBar that hold a shortcut of some functionalities:
  
  ![Capture d’écran (811)](https://user-images.githubusercontent.com/93831197/150660043-b68bc32e-2a92-453b-8a4e-f60ed0beb9d2.png)
  
  And also a main window  where we can have a look on today ,pending   and finished tasks.
  When you click on the button of adding a task a dialog is displayed and it is composed of the description label  where we describe our tasks, then the tag where we choose between Life ,Work and other ,also the due date which sets the date of the task. and finally a checkbox (finished ) that determines whether the task is finished or not. 
  
![WhatsApp Image 2022-01-23 at 01 46 02](https://user-images.githubusercontent.com/93831197/150681014-37f006f4-7ac1-4b85-a59a-efe5350654ba.jpeg)




 **<h3>Functionality</h3>**
 
 **<h4>Adding a task</h4>**
 

To add a task to the list we  need to get the desciption ,the tag and the date the thing that is done through  the following getters :
 ```javascript
 QString addTaskDialog::getTask(){
    return ui->lineEdit->text()+ " Due: "+ui->dateEdit->text() + " Tag: " +ui->comboBox->currentText();
}
QDate addTaskDialog::getDate(){
    return ui->dateEdit->date();
}
bool addTaskDialog::get_if_is_a_FinishedTask(){
    return ui->checkBox->isChecked();
}
QString addTaskDialog::getTag(){
    return ui->comboBox->currentText();
  ```

Here is the code of the Add slot :
 ```javascript
 void ToDoApp::on_action_Add_task_triggered()
{

    addTaskDialog dialog;
    auto reply=dialog.exec();
    if (reply==addTaskDialog::Accepted)
    {
        if (dialog.get_if_is_a_FinishedTask())
        {

           ui->finishedT->addItem(dialog.getTask());


        }
     else if (QDate::currentDate() == dialog.getDate())
         ui->listWidget->addItem(dialog.getTask());
     else
         ui->pendingT->addItem(dialog.getTask());


}
}
  ```
  Actually in this method if the checkBox finished is checked the task is automatically added to the finished task ListWidget .But if the getter of the due date is equal to the current day the task is added to today task ListWidget .If not it is tranfered to pending tasks.
  
**<h4>View today,pending or finished tasks</h4>**

To view a specific task we use setVisible(bool) method
    
Here is the code:

```javascript
     void ToDoApp::on_action_View_pending_tasks_toggled(bool arg1)
{
    if(arg1)
        ui->pendingT->setVisible(true);
    else
        ui->pendingT->setVisible(false);
 }
        
 ```
 
![WhatsApp Image 2022-01-23 at 01 24 10 (1)](https://user-images.githubusercontent.com/93831197/150681036-7ca39dc5-2d37-404a-8d97-13c4ebb57296.jpeg)

 
 ```javascript
        void ToDoApp::on_action_View_today_tasks_toggled(bool arg1)
{
    if(arg1)
        ui->listWidget->setVisible(true);
    else
        ui->listWidget->setVisible(false);
}
}
```
 ![WhatsApp Image 2022-01-23 at 01 24 10](https://user-images.githubusercontent.com/93831197/150681030-d12ba133-5c62-4156-9da7-e8057f184b41.jpeg)

```javascript
void ToDoApp::on_action_View_finished_tasks_toggled(bool arg1)
{
    if(arg1)
        ui->finishedT->setVisible(true);
    else
        ui->finishedT->setVisible(false);
}
```
 
![WhatsApp Image 2022-01-23 at 01 24 10 (2)](https://user-images.githubusercontent.com/93831197/150681039-11d73703-187c-4072-97fc-494794a14381.jpeg)


**<h4>Adding a new file</h4>**

Once the new button is triggered, a Message Box appears informing the user whether he wants to open a new file without saving the previous one or he wants to save before opening a new file. 

Here is the code:


 ```javascript
 
 voidToDoApp::on_action_New_triggered()
{
QMessageBoxmsgBox;
msgBox.setText("Opening a new file.");
msgBox.setInformativeText("Do you want to save this file before opening a new one?");
msgBox.setStandardButtons(QMessageBox::Yes|QMessageBox::No|QMessageBox::Cancel);
msgBox.setDefaultButton(QMessageBox::Yes);
intret=msgBox.exec();
switch(ret){
caseQMessageBox::Yes:
on_action_Save_triggered();
ui->listWidget->clear();
ui->pendingT->clear();
ui->finishedT->clear();
break;
caseQMessageBox::No:
ui->listWidget->clear();
ui->pendingT->clear();
ui->finishedT->clear();
break;
caseQMessageBox::Cancel:

break;
default:

break;
}
}
  ```

**<h4>Remove a task </h4>**
To remove a task we use the method selectedItems() that Returns a list of all selected items in the list widget. After that we delete the selected items usingtakeItem ()
 Method that takes the row as a parameter. This public function removes and returns the item from the given row in the list widget; otherwise returns 0.

Here is the code:

 ```javascript
voidToDoApp::on_action_Remove_task_triggered()
{
QList<QListWidgetItem*>items=ui->listWidget->selectedItems();
foreach(QListWidgetItem*item,items)
{
deleteui->listWidget->takeItem(ui->listWidget->row(item));
}
QList<QListWidgetItem*>items2=ui->pendingT->selectedItems();
foreach(QListWidgetItem*item,items2)
{
deleteui->pendingT->takeItem(ui->pendingT->row(item));
}
QList<QListWidgetItem*>items3=ui->finishedT->selectedItems();
foreach(QListWidgetItem*item,items3)
{
deleteui->finishedT->takeItem(ui->finishedT->row(item));
}

}
```

**<h4>Save files </h4>**

We save the tasks in a file like following :

```javascript
voidToDoApp::saveTasks(QStringfilename){
QFilefile(filename);
if(file.open(QIODevice::WriteOnly|QIODevice::Text)){

QTextStreamstream(&file);
stream<<"List of Today's tasks :"<<Qt::endl;
for(inti=0;i<ui->listWidget->count();i++){
QListWidgetItem*item=ui->listWidget->item(i);
stream<<item->text()<<Qt::endl;
}
stream<<"List of pending tasks :"<<Qt::endl;
for(inti=0;i<ui->pendingT->count();i++){
QListWidgetItem*item=ui->pendingT->item(i);
stream<<item->text()<<Qt::endl;
}
stream<<"List of finished tasks :"<<Qt::endl;
for(inti=0;i<ui->finishedT->count();i++){
QListWidgetItem*item=ui->finishedT->item(i);
stream<<item->text()<<Qt::endl;
}


file.close();
}

}
voidToDoApp::on_action_Save_triggered()
{
if(currentFile=="")
{

QFileDialogd;
autofilename=d.getSaveFileName();
currentFile=filename;
setWindowTitle(currentFile);

}

saveTasks(currentFile);

}

}
```
**<h4>Open a file </h4>**

```javascript
voidToDoApp::loadTasks(QStringfilename){

QFilefile(filename);
if(file.open(QIODevice::ReadOnly|QIODevice::Text)){

QTextStreamin(&file);
QVector<QString>tasks;
while(!in.atEnd()){
QStringline=in.readLine();
tasks.append(line);

}
intt=tasks.indexOf("List of pending tasks :");
intp=tasks.indexOf("List of finished tasks :");
for(autoi=1;i<t;i++)
ui->listWidget->addItem(tasks[i]);
for(autoi=t+1;i<p;i++)
ui->pendingT->addItem(tasks[i]);
for(autoi=p+1;i<tasks.size();i++)
ui->finishedT->addItem(tasks[i]);


file.close();
}
}


voidToDoApp::on_action_Open_triggered()
{
QFileDialogd;
autofilename=d.getOpenFileName();
currentFile=filename;
setWindowTitle(currentFile);

loadTasks(currentFile);


}
```

**<h4>Exit the application </h4>**

Before exiting the application, we call the file that we want to save in the tasks so that when we reopen the application when can find all the tasks that we added previously.

```javascript
voidToDoApp::on_action_Exit_triggered()
{
QFilefile("CurrentFile.txt");
if(file.open(QIODevice::ReadWrite|QIODevice::Text)){
QTextStreamstream(&file);
stream<<currentFile;
file.close();
}

this->close();
}
```

**<h4>Edit tasks </h4>**
To edit the tasks, we need to double click the item that we want to modify. Once the item is clicked, the dialog pops up. We use the following setters to set the values in the dialog:

```javascript
voidaddTaskDialog::setDescription(QStringdescription){
ui->lineEdit->setText(description);

}
voidaddTaskDialog::setDate(QStringdate){
QStringListdatelist=date.split("/");
QDated(datelist[2].toInt(),datelist[1].toInt(),datelist[0].toInt());
ui->dateEdit->setDate(d);
}
voidaddTaskDialog::setTag(QStringtag){
ui->comboBox->setCurrentText(tag);
}
voidaddTaskDialog::setFinished(boolfinished){
ui->checkBox->setChecked(finished);
}
```

Here is the code of editing tasks for:

*	Today list widget:
 ```javascript
  voidToDoApp::on_listWidget_itemDoubleClicked(QListWidgetItem*item)
{

addTaskDialogdialog;
autotask=item->text();
QStringListlist=task.split(" ");
autoi=0;
QStringdes{""};
while(list[i]!="Due:"){


des+=" "+list[i];
i++;
}

qDebug()<<i;
dialog.setDescription(des);
dialog.setDate(list[i+1]);
dialog.setTag(list[i+3]);

autoreply=dialog.exec();

if(reply==addTaskDialog::Accepted)
{
if(dialog.get_if_is_a_FinishedTask())
{

ui->finishedT->addItem(dialog.getTask());

}
elseif(QDate::currentDate()==dialog.getDate())
ui->listWidget->addItem(dialog.getTask());
else
ui->pendingT->addItem(dialog.getTask());
}



deleteitem;
}
 ```
 
*	Pending list widget:

 ```javascript
voidToDoApp::on_pendingT_itemDoubleClicked(QListWidgetItem*item)
{
addTaskDialogdialog;
autotask=item->text();
QStringListlist=task.split(" ");
autoi=0;
QStringdes{""};
while(list[i]!="Due:"){


des+=" "+list[i];
i++;
}

qDebug()<<i;
dialog.setDescription(des);
dialog.setDate(list[i+1]);
dialog.setTag(list[i+3]);
i=0;
autoreply=dialog.exec();
if(reply==addTaskDialog::Accepted)
{
if(dialog.get_if_is_a_FinishedTask())
{

ui->finishedT->addItem(dialog.getTask());

}
elseif(QDate::currentDate()==dialog.getDate())
ui->listWidget->addItem(dialog.getTask());
else
ui->pendingT->addItem(dialog.getTask());
}

deleteitem;
}

```
*	Finished list widget:

 ```javascript
 voidToDoApp::on_finishedT_itemDoubleClicked(QListWidgetItem*item)
{
addTaskDialogdialog;
autotask=item->text();
QStringListlist=task.split(" ");
autoi=0;
QStringdes{""};
while(list[i]!="Due:"){


des+=" "+list[i];
i++;
}

qDebug()<<i;
dialog.setDescription(des);
dialog.setDate(list[i+1]);
dialog.setTag(list[i+3]);
dialog.setFinished(true);
i=0;
autoreply=dialog.exec();
if(reply==addTaskDialog::Accepted)
{
if(dialog.get_if_is_a_FinishedTask())
{

ui->finishedT->addItem(dialog.getTask());

}
elseif(QDate::currentDate()==dialog.getDate())
ui->listWidget->addItem(dialog.getTask());
else
ui->pendingT->addItem(dialog.getTask());
}


deleteitem;
}
```
In the constructor we  add the following code so that when we open the application we can find the tasks that were added previously :

```javascript
QFilefile("CurrentFile.txt");
if(file.open(QIODevice::ReadOnly|QIODevice::Text)){
QStringpath=file.readLine();
loadTasks(path);
}
```
**<h4>Drag and drop </h4>**

We write the following code in the constructor so that we enable the drag and drop actions between the 3 lists widget

```javascript
ui->listWidget->setDragEnabled(true);
ui->pendingT->setDragEnabled(true);
ui->finishedT->setDragEnabled(true);

ui->listWidget->setAcceptDrops(true);
ui->pendingT->setAcceptDrops(true);
ui->finishedT->setAcceptDrops(true);

ui->listWidget->setDropIndicatorShown(true);
ui->pendingT->setDropIndicatorShown(true);
ui->finishedT->setDropIndicatorShown(true);

ui->listWidget->setDefaultDropAction(Qt::MoveAction);
ui->pendingT->setDefaultDropAction(Qt::MoveAction);
ui->finishedT->setDefaultDropAction(Qt::MoveAction);

```

**<h2>MVC Model</h2>**

Now we will implement the functionality of our application using the MVC model : 
 * QListView as a view : The QListView class implements a list/tree view. It can display and control a hierarchy of multi-column items, and provides the ability to add new items at any time. Among others the user may select one or many items and sort the list in increasing or decreasing order by any column.

*	QStringListModel as a model : The QStringListModel class provides a model that supplies strings to views. QStringListModel is an editable model that can be used for simple cases where you need to display a number of strings in a view widget, such as a QListView or a QComboBox. The model provides all the standard functions of an editable model, representing the data in the string list as a model with one column and a number of rows equal to the number of items in the list.

Here is a video that visualizes the functioning of our application.

https://user-images.githubusercontent.com/93831197/150682966-15405b5b-9be1-4900-9a08-b57e23e3625e.mp4


**<h2>Conclusion</h2>**

In this homework we have worked with two different approaches to implement our application. The result is the same but the MVC model remains more flexible and a Faster Development Process.

**<h2>Made by:</h2>**
<h3>Ikram Belmadani</h3>
<h3>Biyaye Chaimae</h3>
