---
status: ood
---

# Unix Console 
## how to edit the Config Files
The suggested way to edit Configuration files is by using [WinSCP](../Installation/Tools.md).
However, if you need to edit files in the console you need to use `vim`. 

 * Open a console
 * go to ```cd /root/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/app```
 * type ```ls``` to see the list of files
 * type ```vim __init__.py```
   *  To go into write mode type 'i'.
   *  do your edits
   *  to exit from insert mode by pressing the Esc key. 
   *  To write a command type semicolon
      and then type the command `:wq!`  or `:x!` (both do the same thing) 
   *  hit ENTER (to save and exit).
