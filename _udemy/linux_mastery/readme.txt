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

Example:
alias ll='ls -l --color=auto'

Apply changes with:
source ~/.bash_aliases or restart the terminal.

Ensure ~/.bashrc includes line below to load aliases:
[ -f ~/.bash_aliases ] && . ~/.bash_aliases


Paths
Absolute: Full path from root:
/home/user/file.txt

Relative: Based on current directory:
../file.txt


Brace Expansion
Generate string patterns quickly. Works with any command, not just mkdir.

Example:
echo {a,b,c}                # a b c  
echo {1..5}                 # 1 2 3 4 5  
mkdir {jan,feb}_{23,24}     # jan_23, feb_23, jan_24, feb_24

Create many files:
touch {jan,feb,...,dec}_{2020..2025}/file{1..100}.txt

Directories must already exist, or the command will fail.

It’s a quick way to repeat patterns without typing each manually.


Wildcards & Globbing
Wildcards are used for pattern matching in file and directory names.

*:      Matches any string
?:      Matches one character
[abc]:  Matches one of a, b, or c
[!0-9]: Excludes digits


Globbing is filename expansion done by the shell, not the command.

Example:
echo *.txt  # Lists all .txt files

Globbing doesn’t search recursively (use find for that).


find vs locate

Find
    Real-time search
    Slower but accurate
    Advanced filters: name, size, exec
    
    find /path -name "file.txt"

locate
    Searches a database (updatedb)
    Faster, but may be outdated if database isn’t refreshed
    Limited filtering (name-based)
    
    locate file.txt

Use find for precision and live results, locate for quick name-based lookup.


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
