
# About
**ExCheck** is a plugin for ATAK and WinTAK. It allows users to collaborate on the execution and monitoring of tasks based on templates. 
To use ExCheck, you need to have a server that supports it. FTS supports the plugin since version 1.3

## Wintak
in Wintak (since version 4.1) you can find the plugin as ExCheck under the plugin tab. 
On the top of the window you will see two buttons. a list of active checklists shows up below them.

with the buttons You can:
- create a new Template
- create a new template based on an existing one
- Join active checklist
- Start a new checklist

### create a new Template

You need to define a name , a description and at least a task, to be able to save the template. 

standard couloumns can be modified or deleted, 
- No: sequence of the task
- Description: name of the task
- Req. : this step is required to complete the checklist (???)
- Callsign: 
Net
From
To
Codeword: a code word for this task
- Due relative DTG:  the timing of the completition of the task required field

after that you have created a task you can press on the hanburger menu (the 3 lines) to the left to:
- Delete the task
- add some background color
- Toggle linebreak: allows to create a block of tasks

###  create a new template based on an existing one
Works like the previous, only you will start the template by modifying an existing one

###  Join active checklist

### Start a new checklist
When you start a new checklist, the current status is saved locally and on the server.

### Working with checklists
As soon a checklist is started you can click on an action and set it to be completed. You can also set back to pending a completed item.
It's also possible to add Notes (those are only visible opening the item
If another team member changes the status of a task, WinTAK you will get an update.


to delete a checklist you need to open it and pres the delete button

## ATAK
the plugin for ATAK is yet not available to the community (Dec 2020). 
Functionalities are similar to the WinTAK version.
Tests indicate that FTS has the same level of functional support 
