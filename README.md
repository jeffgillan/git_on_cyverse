# Using Git and Github with Cyverse Vice Apps

Git and Github are essential tools for software version control. The following documentation show how to use Git and Github with the Cyverse Discovery Environment and specifically with Visual Interactive Computing Environement (VICE) apps (e.g, Jupyter Lab). 

## The Problem

Your personal datastore directory (ie, `~/data-store/home/<cyverse user name>`) would seem like the most logical place to clone git repositories, work in them, then push changes back up to Github. Unforntunately, git repositories are not compatable with Integrated Rule Oriented Data System (IRODS) which is the underlying technology of the Cyverese Datastore. So to use git and github with Cyverse, we need a different solution. 

## The Solution

Instead of doing git commands from your personal datastore, we can do git from the home directories of JupyterLab or Cloudshell containers. When you first launch a JupyterLab terminal, you will probably be in the directory `~/` or `~/data-store`. From these directories, git commands work perfectly fine. To do git commands with Github, we need to have `.gitconfig` and `.ssh` files stored in our container. A problem with this is that Cyverse containers are ephemeral and disappear when the App is shutdown. That means every time a CyVerse Jupyter App is launched, users need to create git credentials and an ssh key for a GitHub handshake. Quite annoying! 

We can work around this issue by creating `.config` and `.ssh` files one time in the container and then store them in your personal Datastore directory. Each time you start a new JupyterLab container we need to copy the `.config` and `.ssh` files from your personal Datastore directory back to the container. 

### Step 1: Set up the authentication handshake with Github

- Launch a VICE App with Jupyter (e.g., [JupyterLab Data Science](https://de.cyverse.org/apps/de/c2227314-1995-11ed-986c-008cfa5ae621))
- Once the App is running, open the App's terminal.
- `ssh`:
  1. Create your ssh key with `ssh-keygen`. Use whichever encryption you prefer.
  2. Copy your `ssh` folder to your own private CyVerse Data Store folder (`cp -r ~/.ssh/ ~/data-store/home/<username>/`)
  3. Copy your publish `ssh` key to GitHub (print key with `cat ~/.ssh/id_rsa.pub`, copy the key, go to https://github.com/settings/keys and add your key)
- `git` credentials:
  1. Create your `git` credentials with `git config --global user.name "<GitHub username>"` and `git config --global user.email "<GitHub email>"`
  2. Copy your `git`credentials to your own private CyVerse Data Store folder (`cp ~/.gitconfig ~/data-store/home/<username>/`)

You can now work on your cloned GitHub repositories and push changes.

### Reproducing the handshake

Likely, once done with work on the launched App, you will terminate it and therefore lose the `ssh` and `git` credentials.
Since we have copied the necessary files to our own private Data Store folders, we can reproduce this handshake by just copying these files to any newely launched App.

1. Copy the `ssh` files with `cp -r ~/data-store/home/<username>/.ssh ~/`
2. Copy the `git` credentials with `cp ~/data-store/home/<username>/.gitconfig ~/`

You should now be able to work on your cloned GitHub repositories and push changes without having to recreate the `ssh` key or your `git` credentials.
