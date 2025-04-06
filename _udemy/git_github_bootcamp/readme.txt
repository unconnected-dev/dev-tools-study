https://www.udemy.com/course/git-and-github-bootcamp/
https://git-scm.com/docs



Version Control System
Software that tracks and manages changes to files over time. Generally, it
allows users to revisit earlier versions of the files, compare changes between
versions, undo changes, etc.


Git Bash
Default shell for Linux and Mac. Git was designed to run on a Unix-based
interface (like Bash).

Windows comes with a different default command-line interface called Command
Prompt, which is not Unix-based.

Git Bash is a tool that emulates a Bash experience on a Windows machine.


Repository
A Git "Repo" is a workspace that tracks and manages files within a folder.


Staging Area
A place where changes are gathered before committing. It allows you to review
and organize changes before saving them in the repository.


Atomic Commits
When possible, a commit should encompass a single feature, or fix. In other
words try to keep each commit focused on a single thing.


Amending Commits
Use git commit --amend to modify the last commit. This lets you update the
commit message or include additional changes without creating a new commit.


Branches
Branches allow multiple versions of a project to exist simultaneously. They
help in developing new features or fixing bugs without affecting the main code.


The Master Branch
In git, we are always working on a branch. The default branch name is master.

It does not do anything special, it is just like any other branch.


HEAD
The pointer to the current commit in the active branch. It moves with each
new commit, always representing the latest snapshot of the branch.


Conflict Markers
When Git can't automatically merge changes, it adds conflict markers to show
conflicting sections in a file.

    <<<<<<< HEAD  
    your changes  
    =======  
    incoming changes  
    >>>>>>> feature-branch  
