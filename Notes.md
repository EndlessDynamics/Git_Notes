# Table of Contents
- Markdown Syntax
- Git Config
- Git Branches (Local)
- Git Repositories (Local)
- Git Branches (Remote)
- Git Repositories (Remote)
- To Be Continued..
<br>
<hr>

## Markdown Syntax

* Use '#' symbols prepended to a line to change font sizes.
  * This is useful for creating **Subjects** *or* **Sections** in files that are of a.md filetype.
  * Use # - ###### to modify the size of text for a line.
  * Up to six '#' symbols can be used.
  * A single '#' allows for the largest size font, and 6 '#' being the smallest.
* Use '<br>' to add an empty line to buffer between paragraphs.
* Use '<hr>' to add a visible line break in the form of a straight bold line to separate between page content.
* TBC...

<br>

## Git Config

1. Define the author name to be used for all commits in the current repository:
  * git config user.name "[Name]"
    - NOTE: Use the **--system** flag to specify the author name to be used in all repositories for all users of the system.
    - NOTE: Use the **--global** flag to specify the author name to be used in all repositories for the logged in user.
    - NOTE: Use the **--local** flag (this is the default behavior) to specify the author name to be used in the current repository.
      - EXAMPLE:  git config --system user.name "[Name]"
      - EXAMPLE:  git config --global user.name "[Name]"
      - EXAMPLE:  git config --local user.name "[Name]"
    - NOTE: **--system** will supply a git config file in all users' home dirs in which all users' repos will inherit from (*unless a repo has been configured with a **--local user.name** or **--global user.name** command.*).
    - NOTE: **--global** will supply a git config file in the home dir for the logged in user in which all repos will inherit from (*unless a repo has been configured with a **--local** user.name command.*).

<br>

2. TBC...

<br>

## Git Branches (Local Branch Management)

1. To list branches in the local repository:
  * git branch
  * git show-branch

<br>

2. To delete a branch in a local repository:
  * git branch --delete [branch_name]
    - NOTE: Do not use [origin/branch_name].

<br>

3. To remove any references to *stale* remote branches (remote branches that no longer exist):
  * git fetch [remote_shorthand] --prune
    - i.e. git fetch origin --prune

<br>

4. To create a new branch in a local repository:
  * git branch [new_branch_name]

<br>

5. To switch to a branch and be able to make changes within that branch:
  * git checkout [branch_name]

<br>

6. To track changes you've made to a file(s) (a.k.a. Staging a file):
  * git add [filename]
  * git add [directory/filename]
  * git add .
    - NOTE: This adds all files(not currently being tracked) in the CWD to the staging area.
    - NOTE: This does not include sub-directories.
  * git add -A
    - NOTE: This recursively adds all files(not dirs) in the CWD and below to the staging area.
    - NOTE: This does not include empty sub-directories. Only if files exist in a sub-dir will a sub-dir be included in the staging. However, it's *files* that are the focus of the tracking, **not** the sub-dir itself.

<br>

7. To remove a file that you no longer want, but need git's version control to be aware of the deletion:
  * git rm [filename]
  * git rm [path/to/filename]

<br>

8. To check the current status of what changes are being tracked:
  * git status

<br>

9. To submit tracked changes as commits, meaning to save the file in it's current state as a period in time(i.e. version controle):
  * git add [target1_filename] [target2_filename]
    - NOTE: Always ensure the latest changes are staged before commiting. (Unless you only wish to commit the changes as they were in your last 'git add' command)
  * git commit -m "[notes_or_details_IRT_commit]"
    - NOTE: Guidelines is to be short yet specific, and keep char-length of message below 70 chars.

<br>

10. To view change logs for past commits:
  * git log
    - NOTE: Resulting log details are presented from most recent to oldest commits; and will contain the following:
      - commit ID (hash),
      - Author,
      - Date of commit (DoW MMM DD HH:MM:SS YYYY Timezone_offset_from_GMT),
      - Commit message. 
  * git log --graph
    - NOTE: Uses command-line "art" to aid visually in assessing the commit history. 
  * git log --graph --decorate
    - NOTE: Further aids in visually assessing the commit history by adding color.

<br>

11. TBC...

<br>

## Git Repositories (Local Repository Management)

1. To create an empty Git repository:
 * git init
   - NOTE: This initializes the CWD as a Git repo.
 * git init [directory]
   - NOTE: This initializes a specified directory, residing in the CWD, as a Git repo.
   - NOTE: Use this for creating a project named [directory] so Git doesn't recursively track the project [directory] since you may want to create other projects in your CWD.
   - EXAMPLE:
     - if CWD = ~/GitHub_Projects
     - if the desired Project folder with Git version control is:  Automating_With_Nornir
     - then the Command to execute is:  git init Automating_With_Nornir
     - cd Automating_With_Nornir
     - ls -la ---> contains the .git directory
2. TBC...

<br>

## Git Branches (Remote Branch Management)

1. To list branches in a remote repository:
  * git branch -r
    - NOTE: Displays remote branches in the following format: [remote_shorthand/remote_branch].
  * git branch -a
    - NOTE: Displays the same output as 'git branch -r' above however, output will also include all local branches.
    - NOTE: The currently checked out branch will contain an asterisk before its name.

<br>

2. To add an existing branch from your local repo, to a remote repo:
  * git push [remote_shorthand] [local_branch_name]
    - i.e.  git push origin Development

<br>

3. To delete a remote branch that you no longer wish to have exist in a remote repository:
  * git push [remote_shorthand] --delete [remote_branch_name]
    - i.e.  git push origin --delete Testing

<br>

4. TBC...

<br>

## Git Repositories (Remote Repository Management)

1. To create an empty Git repository:
  * **STEP-1:**  git init
    - NOTE: See '(Local Repository Management)' above for details.
  * **STEP-1 ALT:**  git init [directory]
  * **STEP-2:**  git add .
    - NOTE: Stages the CWD for tracking.
    - NOTE: This may require at least one file to exist for tracking. If so, you can perform the below to satisfy the requirement:
      * touch README.md
      * git add README.md
  * **STEP-2 ALT:**  cd [directory]  *THEN*  git add .
    - NOTE: Stages the CWD for tracking.
    - NOTE: This may require at least one file to exist for tracking. If so, you can perform the below to satisfy the requirement:
      * touch README.md
      * git add README.md
  * **STEP-3:** git commit -m "[notes_or_details_IRT_commit]"
    - NOTE: Guidelines is to be short yet specific, and keep char-length of message below 70 chars.
  * **STEP-4:**  git push [remote_shorthand]
  * **STEP-5 (*optional*):**  git push [remote_shorthand] --all
    - NOTE: After STEP-4, if you create additional branches such as *Development* and *Testing*, and have commited their contents to your local repo, this pushes **all** of the branches that exist in your local repo to the remote repo.

<br>

2. TBC...
