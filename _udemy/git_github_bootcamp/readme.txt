https://www.udemy.com/course/git-and-github-bootcamp/
https://git-scm.com/docs
https://git-scm.com/docs/git-config
https://markdown-it.github.io/



Version Control System
Software that tracks and manages file changes over time. It allows users to
revisit earlier versions, compare changes, undo changes, and more.


Git Bash
A Unix-like shell provided for Windows. Git was designed for Unix-based shells
(like Bash), so Git Bash offers that experience on Windows.

Windows’ default CLI (Command Prompt) is not Unix-based, which is why Git Bash
is used instead.


Repository
A Git repository ("repo") is a tracked folder. Git monitors files within it.


Staging Area
A place to prepare and review changes before committing them to the repository.


Atomic Commits
Each commit should represent a single feature or fix. Keep commits focused.


Amending Commits
Use git commit --amend to modify the last commit — either the message or the
contents — without creating a new commit.


Branches
Branches allow parallel development. They let you build features or fix bugs
without impacting the main codebase.


The Master Branch
The default Git branch is called master (or main in newer setups).
It behaves like any other branch — there’s nothing special about it.


HEAD
A reference to the current commit in the active branch. It updates with each
new commit.

If HEAD contains refs/heads/master, it's pointing to the master branch.
In a detached HEAD, it points to a commit hash directly instead of a branch.


Merge
Combines changes from one branch into another. If conflicts occur, Git prompts
you to resolve them.


Conflict Markers
Git marks conflict areas in files when it can't auto-merge:

    <<<<<<< HEAD  
    your changes  
    =======  
    incoming changes  
    >>>>>>> feature-branch  


Changes
Git shows diffs using + and -:

    Lines with - come from the original version.
    Lines with + are the new version.

    @@ -49,4 +49,9 @@ branches after they've been integrated.

    -49,4 means the original file had 4 lines starting at line 49
    +49,9 means the new file has 9 lines starting at line 49


Stashing
Temporarily save (stash) uncommitted changes without committing them.
Useful when switching tasks. Affects both staged and unstaged changes.

You can stash multiple times — Git maintains a stack of stashes.


Checkout
git checkout can be used to switch branches, restore files, or create new
branches. Its overloaded use led to the introduction of git switch and
git restore.


Detached HEAD 
Occurs when HEAD points to a specific commit, not a branch.
Commits made here are not part of any branch unless explicitly saved.

HEAD usually points to a branch reference, which in turn points to a commit.


Git Reset
Used to undo commits. Moves the branch pointer backward to a prior commit.
Removes the commits from history.

Useful when commits haven’t been shared with others. The commits are gone.


Git Revert
Undoes changes by creating a new commit that reverses a previous one.

Unlike reset, it preserves history. Ideal for undoing shared commits.

Use reset for private changes; revert for public ones.


Remote
A remote is a Git "destination" (URL) for syncing repositories — e.g., GitHub.
Before pushing, configure a remote with git remote add.


Origin
By convention, origin is the default name for a remote after cloning.
It’s just a label and can be renamed.


Remote Tracking Branches
Local references (like origin/master) to remote branches. These are updated
by fetch/pull/push but are read-only locally.


Fetching
Downloads remote updates, but doesn't merge them into your working branch.
Useful for reviewing changes without affecting your code.


Pulling
Fetches and integrates remote changes into your current branch.


GitHub Gists
Used to share code snippets or short scripts. Easier to create than full repos
but with fewer features.


GitHub Pages
Public webpages that are hosted and published via Github. (HTML/CSS/JS only).
No server-side code.

    1 user site
    username.github.io

    unlimited project sites
    username.github.io/repo-name


Centralized Workflow
Everyone commits directly to main/master. Simple but prone to conflicts in
larger teams.


Feature Branches
Rather than working on directly on the master, all new development should be 
done on separate branches.

Treats master branch as the official project history.
Allows for collaboration on a single feature to share code back and forth
without polluting the master branch.


Fork & Clone
Common in open-source. Each contributor forks the main repo, clones their fork,
works locally, then submits a pull request to the original repo.


Forking
Creates a copy of another user’s GitHub repo under your account.
Not a Git feature — it's GitHub-specific.


Pull Requests
A feature built in to products like Github & Bitbucket. NOT native to Git 
itself.

Allows developers to alert team-members to new work that needs to be reviewed.
Provides a mechanism to approve or reject the work on a given branch. Also 
helps facilitate discussion and feedback on the specified commits.


Rebasing
Rewrites commit history to produce a cleaner project history.

Instead of merging, rebasing moves the feature branch to begin at the latest
commit of the base branch, replaying changes one by one.

Warning: Never rebase commits that have been pushed/shared.


Git Tags
Tags are permanent labels pointing to specific commits (e.g. v1.0.0).

    Lightweight tags: simple labels
    Annotated tags: include metadata like author and message


Pushing Tags
By default, git push doesn't push tags to remote servers. Use git push --tags
to upload all tags at once.


Refs Folder
Contains pointers to branches and tags:

    refs/heads/: one file per branch
    refs/tags/: one file per tag

Each file holds the commit hash for that reference.


Objects Folder
Git’s object store. This is where Git stores the backups of files, the commits
in a repo, and more. Contains all data: blobs, trees, commits, and more.
Files are compressed and encrypted.


Git Database
Git is a key-value store. Content is stored with a SHA-1 hash as its key.


Blobs
Git blobs (binary large object) are the object type Git uses to store the 
contents of files in a given repository. Blobs don't include the filenames of
each file or any other data. They just store the contents of a file.


Trees
Trees are Git object used to store the contents of a directory. Each tree
contains pointers that can refer to blobs and to other trees.

Each entry includes the SHA-1, mode, type, and filename.


Commits
Store:
    A tree reference
    Parent commits
    Author & committer info
    Commit message


Reflogs
Tracks updates to references (branches, HEAD, etc.).

Only stored locally. Not shared. Old entries expire after ~30 days.


Reflog references
Use name@{n} or name@{date} to reference previous states.
Example: HEAD@{1} refers to the previous position of HEAD.

Can be passed to other commands including checkout, reset, and merge.


Global Git Config
Git looks in ~/.gitconfig or ~/.config/git/config for global settings.

Any confirguration variables changed in the file will be applied across all Git
repos.


Adding Aliases
Use Git aliases for custom commands.
Examples:

    git config --global alias.ci commit
    git config --global alias.lg "log --oneline --graph"