---
status: ood
---

# Unix Console 
## hot to edit the Config Files
the suggested way to edit Configuration files is by using [WinSCP](../Installation/Tools.md),
however if you need to edit files in the console you need to use `vim`. 

 * Open a console
 * go to ```cd /usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI/app```
 * type ```ls``` to see the list of files
 * type ```vim __init__.py```
 *  To go into write mode type 'i'.
 *  do your edits
 *  to exit from insert mode by pressing the Esc key. 
 *  To write a command first type semicolon  (  :  )  and then type the command wq!  or x! (both do the same thing) 
 *  hit ENTER.
