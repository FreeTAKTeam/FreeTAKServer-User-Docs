
# Unix Console 
## how to edit the Config Files
The suggested way to edit Configuration files is by using [WinSCP](../Installation/Tools.md).
However, if you need to edit files in the console you need to use `vim`. 

 * Open a console
 * go to ```cd /opt/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/app```
 * type ```ls``` to see the list of files
 * type ```vim __init__.py```
   *  begin insert mode by typing 'i'.
   *  insert your edits
   *  leave insert mode by pressing the `Esc` key. 
   *  write and quit by entering either `:wq!`  or `:x!` (both do the same thing)
      * starting command mode is via `:`
      * hit ENTER (to save and exit)
