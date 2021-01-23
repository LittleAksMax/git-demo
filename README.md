# git-demo

This is a short demo on using git!

## Step 1. Creating your account
This step is very simple, simply go to github.com and click on the 'Sign Up' button.
If you already have an account then you can simply sign in

## Step 2. Creating an empty Github repo
In the top right, click on that '+' icon and select 'New repository', give it a name (like git-demo), and leave the rest of the options untouched, as this is simply a demo, not an actual project

Instantly click on the 'creating a new file' and call it 'README.md'
This is a markdown file, that are often used because of how easily they can be converted to html.
I suggest you always make one of these, even if it is not used, as it will be your first commit (save).

Next, go to the bottom of the page, you will see a smaller box, and a larger box. These are used to give descriptions of changes made, you can leave these blank, as there is going to be a default message: 'Create README.md', in this case.

Now, click on the green button that says 'Commit changes' and you will be brought to a project view.

## Step 3. Getting and saving the SSH keys

#### NOTE: THIS ONLY NEEDS TO BE DONE ONCE, BUT YOU CAN MAKE SEPARATE KEYS FOR EACH REPO

#### Generate key, rsa is the type, 4096 is the strength, the email is the email 
> ssh-keygen -t rsa -b 4096 -C "e.mail@example.com"

Upon being prompted, save the keys in the default file path given (usually something like 'home/<user>/.ssh/id_rsa')
You will get a public key (labelled with .pub extension) and a private key (without an extension)
