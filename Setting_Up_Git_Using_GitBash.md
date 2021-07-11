# HowTo: Setup Git on a Workstation (Windows/Linux)
- Below are some basic steps for the initial setup/configuration of git on a workstation.
- For a quick reference guide on Git, checkout this [cheatsheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet) from [Atlassian](https://www.atlassian.com).


## Windows 10 PC
The below steps assumed you have installed [GitBash](https://gitforwindows.org) on a Windows workstation, and that you are to use GitBash to execute all commands unless explicitly informed otherwise.

**NOTE:** _The GitBash installer also includes 'Git GUI' as part of the package however, I have not used it yet._
*The Atlassian has an [excellent guide](https://www.atlassian.com/git/tutorials/git-bash) for walking you through the installation of GitBash for Windows.*
<br>
<br>
<br>
### STEP-1: Open Git Bash, navigate to and create the directory where you'd like to store your project repository(ies), then create a test repo directory.
**-NOTE:** _During the Git installation, if your selections allowed for it, you can perform these steps in Git Bash or in PowerShell._
Example:
```
cd /c/Users/[username]/Documents/
mkdir MyRepos
mkdir MyRepos/Test_Repository
cd MyRepos/Test_Repository
```  
<br>
<br>

### STEP-2: Create an empty Git repository for tracking your first repo by initializing Git; and configure the created .gitconfig file for basic git functionality.
**-NOTE:** _If you plan on interacting with a centralized source code repo, such as GitHub/GitLab, ensure the name and email you define below satisfies what you'd like to see in any future git history logs._
<br><br>
! Initialize git. (*create a Git repository with the cwd as the root dir for subsequent files/folders*)

`git init`

! Configure the basic requirements for using git by editing the .gitconfig file.
```
git config user.name "[Name_to_be_associated_with_git_changes]"
git config user.email "[Email_to_be_associated_with_git_changes]"
```
<br>
<br>

### STEP-3: Generate a public/private keypair to use with SSH pushes/pulls, and ensure your workstation's ssh-agent knows where to find it.
**NOTE:** _Ensure you pick a modern algorithm to prevent having to recreate your keys in case remote code repos, like GitHub/GitLab, refuse to support keys containing too weak/small of a modulus due to industry standards recommendations. Suggestion: use ed25519 instead of a 1024-bit rsa key_
<br><br>
! Generate the ssh public and private keypair.
<br>**NOTE:** _Microsoft Docs has excellent documentation on [OpenSSH key management](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement)_

```ssh-keygen -t ed25519 -C [email_associated_with_Commercial-based_repo_account]```
  - The `-t` arg stands for type, and allows you to specify which algorithm type to use.
  - The `-C` arg stands for comment, and allows you to associate the key with a specific email. Such as the email associated with GitHub/GitLab.

You'll be prompted for 2 things:
1. The Absolute Path in which you will save the priv/pub keys (*include in the path the desired name of your keys*),
2. A passphrase required to be entered when the key is *initially* used or when the PC is shutdown/rebooted.

```
$ ssh-keygen -t ed25519 -C [GitHub_email@example.com]
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/[username]/.ssh/id_ed25519): /c/Users/[username]/.ssh/GitGub_ed25519
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/[username]/.ssh/GitGub_ed25519
Your public key has been saved in /c/Users/[username]/.ssh/GitGub_ed25519.pub
The key fingerprint is:
SHA256:Blah....Blah [GitHub_email@example.com]
The key's randomart image is:
...
some randomart image
...
```

<br>
<br>

Now...
<br>
! Evaluate if the ssh-agent is running on your workstation.

`Get-Service -Name ssh-agent` [MUST use Windows Powershell Running as Admin *NOT* GitBash]

`eval "$(ssh-agent -s)"` [Linux]

<br>

! Define the full path to your new SSH private key using Window's ssh-agent.
<br>**NOTE:** _This is important if you saved your SSH keys in a non-default location_

`ssh-add 'C:\Users\[Username]\path\to\my_priv_key` [Windows Powershell *NOT* GitBash]

*or you can use Git Bash*

`ssh-add /c/Users/[Username]/path/to/my_priv_key` [Windows GitBash]

`ssh-add ~/path/to/my_priv_key` [Linux]

<br>

! By default, Windows does not start the ssh daemon. To configure the behavior as such, perform the following in powershell with elevated(*admin*) priv.

**NOTE:** _You MUST use Windows Powershell Running as Admin *NOT* GitBash_

```
## To set the sshd service to be started automatically at boot-time.
Get-Service -Name ssh-agent | Set-Service -StartupType Automatic

## Now start the sshd service.
Start-Service sshd
```
**NOTE:** _If 'Start-Service sshd' presents an error, try 'Start-Service ssh-agent'._
<br>
<br>
<br>

### STEP-4(*optional*): Enable secure SSH communication to/from a remote Commercial-based source code repository by uploading the public ssh keypair to your remote Commercial account; Confirming ssh access and functionality afterwards. In this example, I'll use [GitHub.com](https://github.com)

! Login to Github.

! Under **Account Settings** select **SSH and GPG Keys**.

! In the **SSH Keys** section, select **New SSH Key**.

! In the **Title** field, enter a name you'll recognize for the key.
 -Example: *Home Desktop*
 -Example: *Work Travel Laptop*

! In the **Key** field, copy+paste the contents of your SSH publickey.pub.
  * In GitBash, you can do this via: `cat GitGub_ed25519.pub`

! Lastly, click `Add SSH Key`.

! Now, Test basic ssh connectivity to GitHub from your local workstation.

`ssh -vT git@github.com`

! Further test by performing a clone of an existing repo on your GitHub account.

`git clone git@github.com:[GitHub_acct_name]/[repo_name].git`
<br>
<br>
<br>

### STEP-5: Test git functionality on your local workstation.

! Ensure you are in the (master/main) repo by cd into the folder, Test_Repository.

`cd /c/Users/[username]/Documents/MyRepos/Test_Repository`

! Copy any files or folders you may currently have on your PC, and place them in your cwd.

```
cd /c/Users/[username]/Desktop/file1.txt ./
cd /c/Users/[username]/Desktop/file2.txt ./
```

! Inform git that you want to stage these files for the purpose of tracking changes during your next commit.

`git add file1.txt file2.txt`

! Inform git that you are done making changes(*in this case, the change was simply the addition of 2 files*) and want to commit any staged files to your repo as a 'formal submission'(*a.k.a commit*).

`git commit`

_**or**_

`git commit -m "Your message here. Briefly describe what this commit is providing(new files,changes-additions,changes-removals)"`

**NOTE:** git does not allow commits without supporting messages. If you submit a commit without a message flag, your env's default text editor will pop up with some commented out(*# symbols*) information giving you guidance on what you could include in a commit message. Add your commit msg at the top line. Once done, save and exit. This will automatically enter your msg contents as a commit msg, just as if you had provided the `-m` arg and submitted the msg.
<br>
<br>
<br>
<br>

## Linux PC
- Pending a future update...
