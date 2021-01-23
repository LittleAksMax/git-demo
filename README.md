# git-demo

This is a short demo on using git!
Keep in mind that you should have a terminal open.
I will show terminal commands in this format:
> $ command<br>> output

If you don't have git installed simply run
> $ sudo apt install git

##### NOTE: I HAVE CONFIGURED MY GITHUB TO NAME MY DEFAULT BRANCH MASTER, SINCE IN OCTOBER 2020 THE DEFAULT BRANCH WAS RENAMED TO MAIN, ALL REFERENCES I MAKE TO MASTER BRANCH ARE NOW CALLED MAIN BRANCH
You can rename your default branch by clicking on your account in the top right, selecting settings, then on the tab on the left selecting 'Repositories'. Here you can also change what you want to call your default branch.

## Step 1. Creating your account
This step is very simple, simply go to github.com and click on the 'Sign Up' button.
If you already have an account then you can simply sign in

## Step 2. Creating an empty Github repo

##### NOTE: I DON'T ALWAYS REMEMBER EXACTLY WHAT EACH BUTTON SAYS, BUT YOU CAN GO OFF THE GIST OF WHAT I WRITE IN QUOTES

In the top right, click on that '+' icon and select 'New repository', give it a name (like git-demo), and leave the rest of the options untouched, as this is simply a demo, not an actual project

Instantly click on the 'creating a new file' and call it 'README.md'
This is a markdown file, that are often used because of how easily they can be converted to html.
I suggest you always make one of these, even if it is not used, as it will be your first commit (save).

Next, go to the bottom of the page, you will see a smaller box, and a larger box. These are used to give descriptions of changes made, you can leave these blank, as there is going to be a default message: 'Create README.md', in this case.

Now, click on the green button that says 'Commit changes' and you will be brought to a project view.

## Step 3. Getting and saving the SSH keys

##### NOTE: THIS ONLY NEEDS TO BE DONE ONCE, BUT YOU CAN MAKE SEPARATE KEYS FOR EACH REPO

### Generate key, rsa is the type, 4096 is the strength, the email is the email 
> $ ssh-keygen -t rsa -b 4096 -C "e.mail@example.com"

Upon being prompted, save the keys in the default file path given (usually something like 'home/<user>/.ssh/id_rsa')
You will get a public key (labelled with .pub extension) and a private key (without an extension).

### Add key to Github keys
Next, use the *cat* command to copy the contents of the public key into the terminal
> $ cat home/<user>/.ssh/id_rsa.pub

Now copy all of the contents of the file (keep in mind that Ctrl+C and Ctrl+V don't do what you think they do in a shell). I suggest you use Ctrl+Shift+C and Ctrl+Shift+V in the terminal, or even just right-click on the selected text and select 'Copy' to be safe.

Now go to your Github, click on your account in the top-right, and select 'Settings', on the tab on the left side of the screen, select 'SSH and GPG keys' and click on 'New Key' (make sure you are adding an SSH key). Simply paste the public key into the box.

The point of this is that the public key was generated with the private key, so by having the private key, you can prove that you are authorized to do what you are doing.

### Add key to git identities

First, start the ssh-agent in the background
> $ eval "$(ssh-agent -s)"<br>> Agent pid 59666

##### NOTE: number is probably going to be something other than 59666

If you're using macOS Sierra 10.12.2 or later, you will need to modify your ~/.ssh/config file to automatically load keys into the ssh-agent and store passphrases in your keychain.
Keep in mind that your key may not be called id_rsa, but what you named it during generation.

```
Host *
  AddKeysToAgent yes
  UseKeychain yes<
  IdentityFile ~/.ssh/id_rsa
```

Last, add your SSH private key to the ssh-agent and store your passphrase in the keychain.
> $ ssh-add -K ~/.ssh/id_rsa

##### NOTE: -K OPTION IS APPLE'S STANDARD VERSION OF ssh-add, WHICH STORES THE PASSPHRASES IN YOUR KEYCHAIN FOR YOU WHEN YOU ADD AN SSH KEY TO THE ssh-agent. IF YOU GET AN ERROR, SIMPLY REMOVE THE PARAMETER AND TRY AGAIN. 

## Step 4. Cloning this repo down to your folder

Navigate to the directory in which you want to store your project (i.e. if you want to store it in ~/Documents/<name_of_repo>/, navigate to ~/Documents/).

Next, go to your project and click on the green 'Code' button, and select SSH, as this is what we just set up. Copy the link.
Next, execute this command
> $ git clone git@repo_domain

The files in your repo will magically appear. Now you can change directory to the repo directory using the *cd* command. You will now see some sort of indication that you are in a git repository from your terminal prompt.

## Step 5. Learning the commands

You should now be familiar with *git clone*. Let's get started with other commands.

### add
Let's get started by creating a file called file.txt (obviously this is applicable with other files).
Your terminal should have some sort of indication that there have been changes made, and you are not synced with your Github repository (usually something like '✗').

To add changed files you can do a few things.

To apply all changes you can do
> $ git add -A

or 
> $ git add .

To only add file.txt
> $ git add file.txt

Or add all files that end in .txt
> $ git add *.txt

etc.

To learn more about *git add* check out the docs: https://git-scm.com/docs/git-add

### status
To check all the different files, and their status run the command
> $ git status

You will see your files, they may be ready to be committed, or they haven't been added, etc.

### commit
Once all your files that you want to commit have been added, you should commit them.
However, you have a commit message accompanying your commit.

If you want a short message, you can simply do it like this:
> $ git commit -m "commit message"

However, if you want a more descriptive and complicated message, simply write:
> $ git commit

And you will be brought to a text editor where you can write your message.
If you want to change the editor you want to write the message in, you can change your .gitconfig file, or:
> $ git config --global core.editor "vim"

where 'vim' is your editor of choice (and I do recommend vim for this). 

To learn more about *git add* check out the docs: https://git-scm.com/docs/git-commit

### push
##### NOTE: YOU CAN ONLY PUSH IF YOUR LOCAL REPO IS SYNCED WITH THE ONLINE ONE
Let's now that the files are committed, you can push them to your Github repository.

Use the command
> $ git push origin master

As long as you cloned the repository, 'origin' will be set up by default, however, if you didn't clone and started from the local repo, you can simply add the origin of a repo.
> $ git remote add origin git@repo_domain

##### NOTE: YOU HAVE TO CREATE A GITHUB REPO TO REMOTELY CONNECT TO IT

Now origin will be set up for you.
But let's make one more small change. Let's say I don't want to write out the 'origin master' part every time I want to push; you can also set up the origin as the default place to push, to do this we set the upstream
> $ git push -u origin master

Now we only have to write *git push* and it will automatically push to origin.

To learn more about *git push* check out the docs: https://git-scm.com/docs/git-push

### pull
To start, create a file called pull.txt on the Github repository, and fill it with any text you want, make sure you commit.
Now we want to sync our local workspace with the Github repository. To do so, we want to use the same link we just used for git clone, and simply put it after *git pull*.
> $ git pull git@repo_domain master

or
> $ git pull origin master

Now you should see that your workspace is synced with the online repo.

You can also use the -u parameter to set the upstream for that branch, meaning you only have to write git pull from that branch from now on.
> $ git pull -u origin master

To learn more about *git pull* check out the docs: https://git-scm.com/docs/git-pull

## Step 6. branching

### Key ideas
The master branch is the main branch in your project. Typically, the master branch contains fully functional and working code that is finished.
So let's make a branch to work on a specific feature. Changes made on that branch will not change anything that happens on other branches, and vice versa. This is especially useful when your new feature will most likely break your code, and you don't want to mess up any work you already have done by attempting to implement the new feature directly into the project.

First, let's see all the branches we have currently. To do this let's use the *git branch* command.
> $ git branch

Here you should see the master branch, the star indicates which branch you are currently on. To exit this view, press 'q' on your keyboard.

##### NOTE: ALL REFERENCES TO 'feature' ARE REFERENCING A BRANCH THAT WAS CREATED 

### Creating checking out, and deleting branches
To look at a branch, you use the *git checkout* command.
> $ git checkout feature

You should see an indication of having changed branches in your terminal (usually the master turns to the branch name).

To create a new branch, we can do two things.
Either we create and checkout separately:
> $ git branch new-branch-name<br>$ git checkout feature

or we can combine the two into one line:
> $ git checkout -b feature

The -b parameter tells git that a new branch needs to be created.

Now let's say the new feature has been created and works, and we have merged the branch we were developing it on with the master branch. We no longer need that branch, and so we can just delete it. We can just do this:
> $ git branch -d feature

### Merging branches, pull requests, and the diff command

Let's say we have finished writing our feature, and we want to merge it with the master branch.

But before that, we want to see the changes between the two branches (i.e. what was changed on the feature branch), we can do this by using the *git diff* command:
> $ git diff feature

Press 'q' to exit the view.
Great! Now that we see the changes made, and we are fine with the result, we can merge the two branches.
Before we do that, however, we should push our committed changes on the feature branch to our Github repo. But this time, instead of master, we want to push it to the branch's name:
> $ git checkout feature<br>$ git push -u origin feature

Again, when we push on this branch, it will automatically now push to that branch in the online repository.

Now we need to make a pull request.
A pull request is a request to have the changes made on one branch, pulled into another branch; in this case, we want to pull the changes from the feature branch, to the master branch.

##### NOTE: GENERALLY PEOPLE MAKE CHANGES/ADD FEATURES IN DIFFERENT BRANCHES THAN MAKE A PULL REQUEST TO MERGE WITH THE MASTER BRANCH

Now we can go to Github, and it has picked up on our pull request. Click on the green button 'Compare & pull request'.
Now you can add to the description box, usually the whats and whys of your changes. After you are done, you can press the 'Create pull request' button.
Once we have made a pull request anyone can review the changes, make comments to them and tell you to make changes.
If people make comments, you may have to resolve conversations (i.e. reply to their comments) before you can merge, depending on your permissions.

You can now click on the green button saying 'Merge pull request', and confirm!
You can also use the *git merge* command:
> $ git checkout master<br>$ git merge feature

If you go to the code tab, and select to the master branch, you will see the changes have been made. However, the changes are not on your local repository, to get the changes locally, you need to execute a *git pull*.

### Merge collisions
In real life you are not always going to have such an easy time merging, sometimes there are merge collisions. Since in a real project there are multiple people working on the same project, there are situations when the same files get changed, and git has a hard time deciding which changes should go through. You always have to resolve these issues manually. 

@49:05
