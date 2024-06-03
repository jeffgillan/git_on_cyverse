# Using Git and Github with Cyverse Vice Apps

Git and Github are essential tools for software version control 

Every time a CyVerse Jupyter App is launched, users need to create git credentials and an ssh key for a GitHub handshake.

Here are steps to work around this issue.

### The first handshake

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
