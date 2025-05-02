https://www.udemy.com/course/git-and-github-bootcamp/
https://git-scm.com/docs
https://markdown-it.github.io/



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

HEAD is usally a pointer to the current branch reference. The branch reference 
is a pointer to the last commit made on a particular branch.

When we make a new commit, the branch pointer is updated to reflect the new 
commit. The HEAD remains the same, because it's pointing at the branch 
reference.

HEAD points to master, not the commit hash.


Remote
Before pushing to Github, we need to tell Git about the remote repository on
Github. A "destination" needs to be setup to push to.

In Git these "destinations" are referred to as remotes. Each remote is simply a
URL where the hosted repository is.


Origin
This is a conventional Git remote name, but it is not at all special. It is
just a name for a URL. 

When we clone a Github repo, the default remote name setup is called origin.
It can be canged but most people leave it.


Remote Tracking Branch Reference
A reference to the state of the master branch on the remote. Like a bookmark
pointing to the last known commit on the master branch on origin.

These references are read-only for the local repository and cannot be moved or
changed directly; they only update when you interact with the remote repository,
typically via commands like git fetch, git pull, or git push.


Fetching
Allows us to download changes from a remote repository, BUT those changes will 
not be automatically integrated into our working files.

It lets you see what others have bene working on, without having to merge those
changes into your local repo.

Think of it as "please go and get the latest information from Github, but don't
screw up my working directory."


Pulling
Like fetch but updates the HEAD branch with whatever changes are retrieved from
the remote.

Think of as "go and download data from Github AND immediately update my local 
repo with those changes"


Github Gists
A simple way to share code snippets and useful fragments with others. Gists are
much easier to create, but offer far fewer features than a typical repository.


Github Pages
Public webpages that are hosted and published via Github. It does not support
server-side code like Python, Ruby, or Node. Just HTML/CSS/JS.


User Site
There is one user site per Github account. This is where you could host a 
portfolio site or some form of personal website. The default url is based on
your Github username, following this pattern: username.github.io though you 
can change this.


Project Sites
You get unlimited project sites, each Github repo can have a corresponding
hosted website. It's as simple as telling Github which specific branch 
contains the web content. The default urls follow this pattern:
username.github.io/repo-name


Centralized Workflow
Everyone works on master / main. AKA The most basic workflow possible.

The simplest collaborative workflow is to have everyone work on a single
branch. It is straightforward and can work for small teams, but it has quite a
few shortcomings.


Feature Branches
Rather than working on directly on the master, all new development should be 
done on separate branches.

Treats master branch as the official project history.
Multiple teamsmates can collaborate on a single feature and share code back and
forth without polluting the master branch.
Master branch won't contain broken code (unless someone messes it up)


Fork & Clone
This workflow is different from the previous two. Instead of just one
centralized Github repository, every developer has their own Github repository
in addition to the "main" repo. Developers make changes and push to their own
forks before making pull requests.

It's commonly used on large open-source projects where there may be thousands
of contributors with only a couple maintainers.


Forking
Github (and similar tools) allow us to create personal copies of other peoples'
repositories. We call those copes a "fork" of the original.

When we fork a repo, we're making a copy of the repo via Github.

Like pull requests, forking is not a Git feature. The ability to fork is 
implemented by Github.


Pull Requests
These are a feature built in to products like Github & Bitbucket. They are NOT
native to Git itself.

They allow developers to alert team-members to new work that needs to be 
reviewed. They provide a mechanism to approve or reject the work on a given
branch. They also help facilitate discussion and feedback on the specified
commits.
