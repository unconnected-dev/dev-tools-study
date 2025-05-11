## Linux Mastery: Master the Linux Command Line

---
#### Links
- [Ubuntu Packages](https://packages.ubuntu.com)
- [Crontab Guru](https://crontab.guru)

---
$PATH  

An environment variable listing directories the shell searches for executables. If a program isn't in `$PATH`, use its full path or add its directory to `$PATH`  

---
Paths

    // Absolute, full path from root
    /home/user/file.txt

    // Relative, based on current directory
    ../file.txt

---
Command Options  
    
    -<option>   // Short, a single character
    --<option>  // Long, words separated by hyphens

---
Standard Input / Output

    0<  // stdin, data the command reads from
    1>  // stdout, normal output of a command
    2>  // stderr, error messages from a command

---
Pipelines

    // Sends output of ls as input to less
    ls | less

---
Aliases

`~/.bash_aliases`, hidden file in your home directory where you can save custom aliases

    // Example
    alias ll='ls -l --color=auto'

    // Apply changes
    source ~/.bash_aliases

    // Ensure ~/.bashrc includes this line to load aliases
    [ -f ~/.bash_aliases ] && . ~/.bash_aliases

---
Brace Expansion

Generates string patterns quickly

    echo {a,b,c}                // a b c  
    echo {1..5}                 // 1 2 3 4 5  
    mkdir {jan,feb}_{23,24}     // jan_23, feb_23, jan_24, feb_24

    // Create many files
    // Directories must already exist or the command will fail
    touch {jan,feb,...,dec}_{2020..2025}/file{1..100}.txt

---
Wildcards & Globbing

Wildcards are used for pattern matching in file and directory names

    *       //  Matches any string
    ?       // Matches one character
    [abc]   // Matches one of a, b, or c
    [!0-9]  // Excludes digits

Globbing is filename expansion done by the shell, not the command. It doesn’t search recursively (use find for that)

    // echo *.txt  // Lists all .txt files

---
Find

 - Real-time search
 - Slower but accurate
 - Advanced filters: name, size, exec

Locate

 - Searches a database (updatedb)
 - Faster, but may be outdated if database isn’t refreshed
 - Limited filtering (name-based)
      
Use find for precision and live results, locate for quick name-based lookup

---
Nano

    Key commands
    ^O (Ctrl+O)  // Write/save file
    ^X (Ctrl+X)  // Exit nano
    ^K           // Cut line
    ^U           // Paste line    
    ^W           // Search
    ^G           // Help

    // Opens or creates notes.txt for editing
    nano notes.txt

---
Repository

Locations (local or remote) storing software packages

Types:
- Official: Maintained by distro
- Third-party: External sources
- Local: Internal / offline use

Used by package managers (apt, dnf, pacman, etc)

---
Package Managers

Tools to install, update, remove software with dependency handling

Handles:
- Dependency resolution
- Downloading from repositories
- Version control

Common package managers

    apt       // Debian/Ubuntu
    dnf       // Fedora
    yum       // CentOS/RHEL
    pacman    // Arch

---
Update / Upgrade

Prepares for apt upgrade / apt install by getting latest versions. It updates the local package which is a list of available packages and their versions

    sudo apt update              // Before
    sudo apt upgrade             // Or
    sudo apt install <package>

Without updating the cache:
- `apt upgrade` or `apt install` might install outdated versions
- The system won’t know about newly available packages or updates

---
Remove
    
    sudo apt-get remove firefox  // Remove a package, keeps config
    sudo apt-get purge firefox   // Remove with config

    sudo apt-get autoremove      // Clean up unused dependencies

    // Clear downloaded package cache
    // Deletes all cached package files in /var/cache/apt/archives
    sudo apt-get clean           

    // Remove only outdated cache files
    // Keeps current ones
    sudo apt-get autoclean