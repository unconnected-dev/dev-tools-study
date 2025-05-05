


$PATH 
An environment variable that tells the shell where to look for executable 
files when you run a command. It contains a colon-separated list of 
directories.

If you install a program but its location isn’t in $PATH, the terminal won’t
find it unless you use the full path or add its directory to $PATH.


-<option>
Short option, typically a single character, used for quick commands.
Example: `-l` for listing details in `ls`.

--<option>
Long option, more descriptive, typically words separated by hyphens.
Example: `--all` to show all files in `ls`.


Pipelines
command1 | command2
Sends the output of command1 as input to command2. Useful for chaining
commands together to process data step by step.
