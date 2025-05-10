https://packages.ubuntu.com
https://crontab.guru



$PATH 
An environment variable listing directories the shell searches for executables.
If a program isn't in $PATH, use its full path or add its directory to $PATH.


Command Options
 -<option>  Short option, typically a single character.
--<option>  Long option, typically words separated by hyphens.


Command Arguments
Values passed after a command to modify its behavior.
ls -l /home: -l and /home are arguments.


Standard Streams
stdin (fd 0): (keyboard, pipe)
Data the command reads from.

Standard Output
stdout (fd 1): (screen)
Normal output of a command.

Standard Error
stderr (fd 2): Error output (screen)
Error messages from a command.


Pipelines
command1 | command2
Sends output of command1 as input to command2.


Aliases

~/.bash_aliases
A hidden file in your home directory where you can save custom aliases.

Example entry:
alias ll='ls -l --color=auto'

To apply changes:
Run `source ~/.bash_aliases` or restart the terminal.

Note:
Make sure your ~/.bashrc contains this line to load aliases:
[ -f ~/.bash_aliases ] && . ~/.bash_aliases




Absolute Path
A full path from the root (/) to the target file or directory.
Example: /home/user/documents/file.txt

Relative Path
A path based on the current directory (uses . or ..).
Example: ../documents/file.txt refers to a file one level up.



Brace Expansion {item1,item2,...}
Generates a list of strings by expanding each item in the braces.

Example:
echo {a,b,c}
Outputs: a b c

You can also use ranges:
echo {1..5}
Outputs: 1 2 3 4 5

Nested/combined use:
mkdir {jan,feb}_{2023,2024}
Creates: jan_2023 feb_2023 jan_2024 feb_2024

Works with any command, not just mkdir.
It’s a quick way to repeat patterns without typing each manually.



touch {jan,feb,mar,apr,may,jun,jul,aug,sep,oct,nov,dev}_{2020..2025}/file{1..100}.txt
Creates 100 text files (file1.txt to file100.txt) inside each of the 72 
directories named like jan_2020, feb_2021, ..., dev_2025.

Breakdown:
- {jan,...,dev} expands to 12 month-like names
- {2020..2025} expands to 6 years
- Combined: 12 × 6 = 72 directories
- file{1..100}.txt expands to 100 filenames per directory
- Total files created: 72 × 100 = 7,200

Note: Directories must already exist, or the command will fail.
Use mkdir first if needed.



Wildcards
*  (asterisk)
Matches zero or more characters.
Example: ls *.txt → lists all .txt files

?  (question mark)
Matches exactly one character.
Example: ls file?.txt → matches file1.txt, fileA.txt

[ ]  (square brackets)
Matches any one of the enclosed characters.
Example: ls file[1-3].txt → matches file1.txt, file2.txt, file3.txt

[! ] or [^ ]
Matches any character NOT listed.
Example: ls file[!0-9].txt → excludes digits

Wildcards are used for pattern matching in file and directory names.


Globbing
The shell’s process of expanding wildcard patterns (*, ?, [ ]) into matching 
filenames or paths before running the command.

Example:
echo *.txt
Expands to: file1.txt file2.txt (all .txt files in the directory)

Globbing is done **by the shell**, not by the command itself.

Common glob patterns:
*     Matches any string of characters
?     Matches a single character
[abc] Matches one character from the set a, b, or c

Globbing doesn’t search recursively (use find for that).


find vs locate

find
- Searches the filesystem in real time
- Slower, but always up to date
- Powerful filters: name, type, size, time, exec, etc.
- Syntax: find /path -name "file.txt"

locate
- Searches a pre-built database (from `updatedb`)
- Much faster, but may be outdated if database isn’t refreshed
- Limited filtering (mostly name-based)
- Syntax: locate file.txt

Use `find` for precision and live results, `locate` for quick name-based lookup.



nano <filename>
Opens a simple terminal-based text editor to create or edit files.

Basic controls (shown at bottom of screen):
^O (Ctrl+O)  Write/save file
^X (Ctrl+X)  Exit nano
^K           Cut line
^U           Paste line
^W           Search
^G           Help

Example:
nano notes.txt
Opens or creates notes.txt for editing



Repository
A storage location (local or remote) that contains software packages.

Types:
- Official: Maintained by distro (e.g. Ubuntu, Fedora)
- Third-party: External sources (e.g. PPAs, custom repos)
- Local: Used for offline or internal package management

Package managers (apt, yum, dnf, pacman) download from repositories.

Example:
sudo apt update
Refreshes package lists from configured repositories



Package Manager
A tool that automates installing, upgrading, configuring, and removing 
software packages on Linux.

It handles:
- Dependency resolution
- Downloading from repositories
- Version control

Common package managers:
apt     (Debian/Ubuntu)
dnf     (Fedora)
yum     (CentOS/RHEL)
pacman  (Arch)

Example:
sudo apt install curl
Installs the 'curl' package and its dependencies



sudo apt update
(or sudo apt-get update)

This updates the local package **cache**, which is a list of available 
packages and their versions from all configured repositories.

Without updating the cache:
- `apt upgrade` or `apt install` might install outdated versions
- The system won’t know about newly available packages or updates

Always run:
sudo apt update
before:
sudo apt upgrade
or
sudo apt install <package>



sudo apt-get remove <package>
Removes an installed package, but **keeps its configuration files**.

Example:
sudo apt-get remove firefox
Removes Firefox, but user settings and configs remain

To remove completely (including config files):
sudo apt-get purge firefox


sudo apt-get autoremove
Removes packages that were automatically installed to satisfy dependencies 
but are no longer needed.

Useful after removing large packages or desktops.

Example:
sudo apt-get autoremove
Frees up space by cleaning leftover dependencies


sudo apt-get clean
Deletes all cached package files in /var/cache/apt/archives

Frees disk space by removing downloaded .deb files that are no longer needed

Safe to run — doesn’t affect installed packages

Example:
sudo apt-get clean
Clears out the package cache completely


sudo apt-get autoclean
Removes **only outdated** .deb package files from the cache that can no 
longer be downloaded or installed.

Frees some disk space, safer and more selective than `clean`.

Example:
sudo apt-get autoclean
Removes obsolete package files but keeps current ones
