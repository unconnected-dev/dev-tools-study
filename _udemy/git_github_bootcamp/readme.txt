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


Merge
Combines the history of both branches, integrating their changes into a single
branch. If there are conflicts, Git will prompt you to resolve them.


Conflict Markers
When Git can't automatically merge changes, it adds conflict markers to show
conflicting sections in a file.

    <<<<<<< HEAD  
    your changes  
    =======  
    incoming changes  
    >>>>>>> feature-branch  


Changes
Every line that changed between the two files is marked with either a + or 
- symbol. 

Lines that begin with - come from file A
Lines that begin with + come from file B

    @@ -49,4 +49,9 @@ branches after they've been integrated.

    -49,4 means the original file had 4 lines starting at line 49
    +49,9 means the new file has 9 lines starting at line 49


Stashing
Git provides an easy way of stashing uncommmited changes so that we can return
to them later, without having to make unnecessary commits. This affects staged
and unstaged changes.

You can add multiple stashes onto the stack of stashes. They will all be 
stashed in the order you added them.


Checkout
The git checkout command is thought to be overloaded, which is what lead to the
addition of the git switch and git restore commands. We can use checkout to 
create branches, switch to new branches, restore files, and undo history.


Detached HEAD  
A state where HEAD points to a specific commit, not a branch. Changes made here
won’t belong to any branch unless explicitly saved.