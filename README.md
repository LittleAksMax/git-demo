# git-demo

This is a short demo on using git!
Keep in mind that you should have a terminal open, commands in this format:
> $ command<br>> output

are done in the terminal.

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
Next, use the cat command to copy the contents of the public key into the terminal
> $ cat home/<user>/.ssh/id_rsa.pub

Now copy all of the contents of the file (keep in mind that Ctrl+C and Ctrl+V don't do what you think they do in a shell). I suggest you use Ctrl+Shift+C and Ctrl+Shift+V in the terminal, or even just right-click on the selected text and select 'Copy' to be safe.

Now go to your Github, click on your account in the top-right, and select 'Settings', on the tab on the left side of the screen, select 'SSH and GPG keys' and click on 'New Key' (make sure you are adding an SSH key). Simply paste the public key into the box.

The point of this is that the public key was generated with the private key, so by having the private key, you can prove that you are authorized to do what you are doing.

### Add key to git identities

First, start the ssh-agent in the background
> $ eval "$(ssh-agent -s)"<br>> Agent pid 59666

##### NOTE: number is probably going to be something other than 59666

If you're using macOS Sierra 10.12.2 or later, you will need to modify your ~/.ssh/config file to automatically load keys into the ssh-agent and store passphrases in your keychain.

##### NOTE: YOUR KEY MAY NOT BE CALLED id_rsa, DEPENDING ON WHETHER YOU CHANGED IT OR NOT WHEN GENERATING

{{{ Host *<br>AddKeysToAgent yes<br>UseKeychain yes<br>IdentityFile ~/.ssh/id_rsa }}}

Last, add your SSH private key to the ssh-agent and store your passphrase in the keychain.
> $ ssh-add -K ~/.ssh/id_rsa

##### NOTE: -K OPTION IS APPLE'S STANDARD VERSION OF ssh-add, WHICH STORES THE PASSPHRASES IN YOUR KEYCHAIN FOR YOU WHEN YOU ADD AN SSH KEY TO THE ssh-agent. IF YOU GET AN ERROR, SIMPLY REMOVE THE PARAMETER AND TRY AGAIN. 
