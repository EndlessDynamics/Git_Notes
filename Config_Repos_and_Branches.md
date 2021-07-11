# Table of Contents
```diff
+ Syntax used in Markdown files
+ Git Config
+ Git Branches (Local)
+ Git Repositories (Local)
+ Git Branches (Remote)
+ Git Repositories (Remote)
+ To Be Continued...
```

<br>
<hr>

## Syntax used in Markdown files (filename.md)

* An execellent reference page for [Markdown language](https://www.markdownguide.org/basic-syntax/).
* Use 1-6 hash symbols (`#` - `######`) at the start of a line to signify section headers.
  * This is useful for creating **Subjects** or **Sections** in .md files.
  * The amount of symbols dictate the header size; with # marking the largest header and ###### marking the smallest header.
  * EXAMPLES:
    - `# Table of Contents`
    - `### Primary-Section`
    - `#### Sub-Section`
    - `###### STEP-1`
    - `###### STEP-2`
* Use `<br>` with an empty line before and after the br marking to ensure an empty line is shown between paragraphs or a section of text.
* Use `<hr>` to add a visible line break in the form of a straight bold line to separate between page content.
* Start and end code using three consequtive backtick marks to visually separate a block of text into a code block with a light gray background. 
* To add font color to text by leveraging the color coding of that in Git diffs. Prepend and Append a section of text(\*Can span multiple lines) with three consequtive backtick marks, in which each line must begin with either: `+`, `-`, `!`, `#`, or a `@@` symbol.
  - NOTE: The use of the `@@` symbol must have the subsequent text immediately followed by another `@@` symbol such as, `@@ Some Text @@`.
  - NOTE: The symbols are not *hidden* formatting notation. They **will** be visible in the output as if you intentionally typed them as part of your text, so use them smartly. This is because the symbols are actually executing text formatting from Git's system: Diff.
  - EXAMPLE:
    ```diff
    + new text added
    - previously tracked text is removed
    ! conflicted file/text
    # scheduled for deletion from repo
    @@ deleted by OS file system instead of Git @@
    ```
* TBC...

<br>

## Git Config (Configuring non-default behavior)

1. Define the author's name to be used for all commits in the current repository:
  * `git config user.name "[Name]"`
    - NOTE: Use the `--system` flag to specify the author's name to be used for all repositories of all users on the system.
    - NOTE: Use the `--global` flag to specify the author's name to be used for all repositories of the logged in user.
    - NOTE: Use the `--local` flag (this is the implied default behavior) to specify the author's name to be used in the current repository.
      - EXAMPLE:  `git config --system user.name "[John Doe]"`
      - EXAMPLE:  `git config --global user.name "[John Doe]"`
      - EXAMPLE:  `git config --local user.name "[John Doe]"`
    - NOTE: The `--system` flag will configure a git config file at `/etc/gitconfig` in which all of the System's users and their repos will inherit from.
      - **Can be over-ridden by a user's `~/.gitconfig` file _**or**_ an individual repo's `.git/config` file. Respectively: `git config --global user.name` and `git config --local user.name` commands.**
    - NOTE: The `--global` flag will configure a git config file at `~/.gitconfig` for the currently logged in user only, in which all of the user's repos will inherit from.
      - Can be over-ridden by the configuration of an individual repo's `.git/config` file. Respectively: `git config --local user.name`; while ensuring the CWD (current location of the CLI) is within the target Git-controlled repo.

<br>

2. Define the author's email to be used for all commits in the current repository:
  * `git config user.email "[example@example.com]"`
    - NOTE: Use the `--system` flag to specify the author's email to be used for all repositories of all users on the system.
    - NOTE: Use the `--global` flag to specify the author's email to be used for all repositories of the logged in user.
    - NOTE: Use the `--local` flag (this is the implied default behavior) to specify the author's email to be used in the current repository.
      - EXAMPLE:  `git config --system user.email "[example@example.com]"`
      - EXAMPLE:  `git config --global user.email "[example@example.com]"`
      - EXAMPLE:  `git config --local user.email "[example@example.com]"`
    - NOTE: The `--system` flag will configure a git config file at `/etc/gitconfig` in which all of the System's users and their repos will inherit from.
      - **Can be over-ridden by a user's `~/.gitconfig` file _**or**_ an individual repo's `.git/config` file. Respectively: `git config --global user.email` and `git config --local user.email` commands.**
    - NOTE: The `--global` flag will configure a git config file at `~/.gitconfig` for the currently logged in user only, in which all of the user's repos will inherit from.
      - Can be over-ridden by the configuration of an individual repo's `.git/config` file. Respectively: `git config --local user.email`; while ensuring the CWD (current location of the CLI) is within the target Git-controlled repo.

<br>

3. TBC...

<br>

## Git Branches (Local Branch Management)

1. To list branches in the local repository:
  * `git branch`
  * `git show-branch`

<br>

2. To delete a branch in a local repository:
  * `git branch --delete [branch_name]`
    - NOTE: Do not use `[origin/branch_name]`.

<br>

3. To remove any references to *stale* remote branches (remote branches that no longer exist):
  * `git fetch [remote_shorthand] --prune`
    - i.e. `git fetch origin --prune`

<br>

4. To create a new branch in a local repository:
  * `git branch [new_branch_name]`

<br>

5. To switch to a branch and be able to make changes within that branch:
  * `git checkout [branch_name]`

<br>

6. To track changes you've made to a file(s) (a.k.a. Staging a file):
  * `git add [filename]`
  * `git add [directory/filename]`
  * `git add .`
    - NOTE: This adds all files(not currently being tracked) in the CWD to the staging area.

<br>

7. To create a new file or edit an existing file:
  * `touch [filename]` *or* `touch [path/to/filename]`
    - NOTE: There is no `git touch` command to track the creation of a file using Git. You must use the `git add [filename]` command after creating a file to track it.
  * `nano|vim [filename]` *or* `nano|vim [path/to/filename]`
    - NOTE: There is no `git nano` or `git vim` command to track the editing of a file using Git. You simply edit the file using your preferred text editor, then use the `git add [filename]` command after editing to track the changes.

<br>

8. To remove a file that you no longer want, but need git's version control to be aware of the deletion:
  * `git rm [filename]`
  * `git rm [path/to/filename]`

<br>

9. To check the current status of what files/changes are being tracked:
  * `git status`

<br>

10. To submit tracked changes as commits, meaning to save the file in it's current state as a period in time(i.e. version controle):
  * `git add [target1_filename] [target2_filename]`
    - NOTE: Always ensure the latest changes are staged before performing a commit. (Unless you do not wish to commit any changes to a file since it was last staged/added)
  * `git commit -m "[notes_or_details_IRT_commit]"`
    - NOTE: A ProTip is to be short yet specific, and keep the char-length of the message summary fewer than 50 chars.

<br>

10. To view change logs for past commits:
  * `git log`
    - NOTE: Resulting log details are presented from most recent to oldest commits; and will contain the following:
      - commit ID (hash),
      - Author,
      - Date of commit (DoW MMM DD HH:MM:SS YYYY Timezone_offset_from_GMT),
        - EXAMPLE: Wednesday Jan 01 15:00:00 2021 -6:00
      - Commit message. 
  * `git log --graph`
    - NOTE: Uses command-line "art" to aid visually in assessing the commit history. 
  * `git log --graph --decorate`
    - NOTE: Further aids in visually assessing the commit history by adding color to the art.

<br>

11. TBC...

<br>

## Git Repositories (Local Repository Management)

1. To create an empty Git repository:
 * `git init`
   - NOTE: This initializes the CWD as a Git repo.
 * `git init [directory]`
   - NOTE: This initializes a specified directory, residing in the CWD, as a Git repo.
   - NOTE: Use this for creating a project named [directory] so Git doesn't recursively track the project [directory] since you may want to create other projects in your CWD.
   - EXAMPLE:
     - if CWD = ~/GitHub_Projects
     - if the desired Project folder with Git version control is:  Automating_With_Nornir
     - then the Command to execute is: `git init Automating_With_Nornir`
     - `cd Automating_With_Nornir`
     - `ls -la` ---> Output will show a `.git` dir exists; signifying the root of a dir structure whose versions are managed by Git.
2. TBC...

<br>

## Git Branches (Remote Branch Management)

1. To list branches in a remote repository:
  * `git branch -r`
    - NOTE: This command displays remote branches in the following format: `[remote_shorthand/remote_branch]`.
    - EXAMPLE: `git branch -r`
      - `origin/HEAD -> origin/main`
      - `origin/main`
      - `origin/MinorVersions`
      - `origin/Development`
  * `git branch -a`
    - NOTE: Displays the same output as `git branch -r` above however, the `-a` flag will include local branches as well in the output.
    - NOTE: The currently checked out branch will contain an asterisk before its name.
    - EXAMPLE: `git branch -a`
      - `*main`
      - `remotes/origin/HEAD -> origin/main`
      - `remotes/origin/main`

<br>

2. To add an existing branch from your local repo, to a remote repo:
  * `git push [remote_shorthand] [local_branch_name]`
    - i.e.  `git push origin Development`

<br>

3. To delete a remote branch that you no longer wish to have exist in a remote repository:
  * `git push [remote_shorthand] --delete [remote_branch_name]`
    - i.e.  `git push origin --delete Testing`

<br>

4. TBC...

<br>

## Git Repositories (Remote Repository Management)

1. To create a new, empty Git repository and add it to a remote repo such as GitHub or GitLab:
  * **STEP-1:**  `git init`
    - NOTE: Initialize the CWD with a Git repository.
    - NOTE: See notes on '(Local Repository Management)' above for additional details.

<br>

  * **STEP-1 ALT:**  `git init [directory]`
    - NOTE: Initialize a specific directory as a Git repo and not the CWD.

<br>

  * **STEP-2:**  `git add .`
    - NOTE: Stages all files residing in the CWD for tracking (*not* recursive).
    - NOTE: This may require at least one file to exist for tracking. If so, you can perform the below to satisfy the requirement:
      * `touch README.md`
      * `git add README.md`
<br>

  * **STEP-2 ALT:**  `cd [directory]`  *THEN*  `git add .`
    - NOTE: Stages the CWD for tracking.
    - NOTE: This may require at least one file to exist for tracking. If so, you can perform the below to satisfy the requirement:
      * `touch README.md`
      * `git add README.md`
<br>

  * **STEP-3:** `git commit -m "[notes_or_details_IRT_commit]"`
    - NOTE: Guidelines is to be short yet specific, and keep char-length of message below 70 chars.

<br>

  * **STEP-4:**  `git push [remote_shorthand]`

<br>

  * **STEP-5 (*optional*):**  `git push [remote_shorthand] --all`
    - NOTE: After STEP-4, if you create additional branches such as *Development* and *Testing*, and have commited their contents to your local repo, this pushes **all** of the branches that exist in your local repo to the remote repo.

<br><br>

2. To push an existing Git repository:
  **NOTE:** _This is useful if you have already started on a project on your local workstation and are wanting to add it to a remote server such as GitHub/GitLab for the first time where the project has never existed before._

  * **Before continuing, ensure the project/repo has no outstanding staged files requiring a commit.**
  * `cd  [/full/path/to/existing_local_repo]`
  * [OPTIONAL - Renaming a local branch before officially pushing to remote repo]
    - `git checkout [branch_to_rename]`
    - `git branch -m [new_branch_name]`
      - **NOTE:** _To simplify things, repeat this action for ALL your branches prior to pushing your project to a remote site._
  * Decide on the name you want to use to reference your remote repo(i.e. remote_shorthand). Example: origin, GitHub, or GitLab.
  * Now create a *non-initialized* project on your remote repo. I'll use GitHub for this example walk-through:
    - Login to your GitHub account; navigate to your repositories page.
    - Click 'New' to create a new repository.
    - Give it a name and optionally provide it a project description.
    - Change the repo type from the default 'Public' selection, to 'Private'.
    - Click 'Create a new Repository'.
    - Copy the SSH URL(*not HTTPS*) that is presented on your screen.
    - Now leave GitHub and go back to your GitBash window.
  * `git remote add [remote_shorthand] [remote_ssh_URL/project.git]`
    - NOTE: This associates the new remote repository to your preferred [remote_shorthand]
    - NOTE: [remote_ssh_URL/project.git] must be written in the following syntax:
      - git@github.com:[GitHub_Username]/[ProjectName].git
  * `git push -u [remote_shorthand] --all`
    - NOTE: Push everything to your [remote_shorthand]
  * `git push -u [remote_shorthand] --tags`
    - NOTE: This ensures any tags you have assigned get copied over as well.

<br>

3. To push an existing folder and its contents (that does NOT contain a Git repository yet) to a remote repo in which the Project HAS been created:
  * **NOTE:** _This action is currently being developed!_
  * `cd  [/full/path/to/existing_folder]`
  * `git init --initial-branch=main`
    - NOTE: Ensure the value of '--initial-branch' is the same branch name as your remote repo branch, replace 'main' with the remote name.
  * `git remote add [remote_shorthand] [remote_https_URL/existing_project.git]`
    - NOTE: Associate the new remote repository to your preferred [remote_shorthand]
  * `git add .`
    - NOTE: This stages the folder and its files in the CWD.
  * `git commit -m "Initial commit"`
    - NOTE: This commits all staged local files to your local repo.
  * `git push -u [remote_shorthand] [value_of_--initial-branch]`

<br>

4. TBC...
