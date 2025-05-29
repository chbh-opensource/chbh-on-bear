# Making a contribution

This page will teach you how to add contributions to the chbh-on-bear GitHub page. This page outlines the whole process, from installing Git to requesting your contribution to be added. We assume no knowledge of Git or GitHub.

## Installing Git

### Linux

You can install Git through your package manager in the terminal, this will depend on your particular distro.

For Debian : 

```shell
$ sudo apt install git-all
```

For Fedora :

```shell
$ sudo dnf install git-all
```

For other distros see [other distro installs](https://git-scm.com/download/linux).

### Windows

You can install git from a [windows installer](https://git-scm.com/download/win) or by using a package manager similar to linux.

Using Winget :

```shell
> winget install -e --id Git.Git
```

## Making a Github account

You will also need to have a GitHub account to be able to make a change request. Make an account on [GitHub](https://github.com/)

After making an account configure your git to use that account within your terminal.

```shell
$ git config --global user.email "Add GitHub Email address here within quotes"
$ git config --global user.name "Add GitHub Username here within quotes"
```

You may also need to generate a personal access token :

 - On GitHub click your profile picture
 - Settings
 - Developer Settings
 - Personal Access Tokens 
 - Tokens (Classic)
 - Generate New Token
 - Repo
 - Generate New Token
 - Place this token somewhere safe this will be used for your password

## Working with Git Locally

### Creating a Branch

A branch is a version of the project that is different from the main, this is made so that changes do not effect the main project.

Check what branch you are on :

```shell
$ git branch -l
```

Create your own branch :

```shell
$ git checkout -b tommy_changes
```
This will create a new branch called "tommy_changes" and switch to it. You can check what branch you are in again to make sure you have switched. 

### Making changes

Once you are on your own branch you can start making changes. To make changes add or edit the markdown files in the "Docs" folder, this can be done in your usual text editor. If you are unfamiliar with markdown check out this [guide](https://www.markdownguide.org/cheat-sheet) If you have created a new markdown file then this can be added to the website in the "mkdocs.yml" file.

Adding the page to mkdocs.yml : 

```shell
nav:
  - Python: software/python.md
```

### Adding your changes

To check the status of you changes use : 

```shell
$ git status
```

Use this whenever you're unsure as what is happening with your file changes.

If you've created a new file add it to git using it's filename.

Example file add :

```shell
$ git add docs/software/python.md
```

To see the differences you've made you can use git in your terminal.

```shell
$ git diff
```

Once you've made all the changes you would like to make, you can then save all these changes to your git branch. As good practice these changes should be similar in nature such as "Correcting spelling errors". 

Saving your changes to your branch :

```shell
$ git commit -m "Correcting spelling errors"
```
This will save all your changes with the messsage "Correcting spelling error". This will be visable publically later and be used to explain your changes to others. 

## Working with GitHub

### Pushing those changes to public branch

To put our changes on GitHub for the project so everyone can see. We must first make a public branch similar to how we created our local branch before. You will be prompted to enter your username for GitHub, use the username we set up before. It will then ask for a password, do not use your GitHub password, use your git token we generated before (Note when you type or copy this token in, it will not be shown in the terminal but it is registering inputs. This can be odd for users unfamiliar.). 

Creating GitHub branch : 

```shell
$ git push --set-upstream origin tommy_changes
Username for 'https://github.com': TommyTeapot
Password for 'https://github.com': {Your token here}
```

To then push those changes to this new branch use : 

```shell
$ git push origin tommy_changes
Username for 'https://github.com': TommyTeapot
Password for 'https://github.com': {Your token here}
```

This will then push these changes to the public branch that is viewable for everyone. If you wish to push another commit you can skip the creating a branch section.

### Making a request for your contribution
After doing all these previous steps the final thing you need to do is create a pull request. This lets the admins know that you want something merged into the main branch that will then be put automatically onto the chbh-on-bear page. 

 - In your browser go onto the chbh-on-bear GitHub page
 - Then on branches select the branch that you have created and made your commits to
 - Click "Make a pull request"
 - Type the title and description of your pull request
 - Check will be run automatically on your pull request and then will be reviewed by the admin team

If review is sucessesful your changes will be merged into the main branch. Otherwise there is a section to have a conversation about those changes and add more commits. Feel free to make any changes you feel are valuable and thank you for contributing!
