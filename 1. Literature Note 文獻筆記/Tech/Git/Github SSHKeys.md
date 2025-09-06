---
tags: 
date: 2023-12-13-週三
time: 17:56
---
[來源](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278)

## SSH keypair setup for GitHub (or GitHub/GitLab/BitBucket, etc, etc)

### [](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278#create-a-repo)Create a repo.

Make sure there is at least one file in it (even just the README.md)

### [](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278#generate-a-ssh-key-pair-privatepublic)Generate a SSH key pair (private/public):

```
ssh-keygen -t rsa -C "your_email@example.com"
```

or even better:

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

It also possible to use ed25519. There are pros and cons, but personally I've had some issues and that is the reason I've chosen to stick to 4096 rsa for now.

### [](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278#copy-the-contents-of-the-public-ssh-key)Copy the contents of the public SSH key

macOS:

```
pbcopy < ~/.ssh/id_rsa.pub
```

GNU/Linux (requires the xclip package):

```
xclip -sel clip < ~/.ssh/id_rsa.pub
```

Windows Command Line:

```
type %userprofile%\.ssh\id_rsa.pub | clip
```

Git Bash on Windows / Windows PowerShell:

```
cat ~/.ssh/id_rsa.pub | clip
```

or ofcourse copy it via your favorite editor, cat, or whatever suits your needs :)

### [](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278#copy-the-public-ssh-key-to-github)Copy the public SSH key to GitHub

Copy the contents of the to your SSH keys to your GitHub account settings ([https://github.com/settings/keys](https://github.com/settings/keys)).

### [](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278#test-the-ssh-key)Test the SSH key:

```
ssh -T git@github.com
```

Change directory into the local clone of your repository (if you're not already there) and run:

```
git remote set-url origin git@github.com:username/your-repository.git
```

Now try editing a file (try the README) and then do:

```
git add -A
git commit -am "Update README.md"
git push
```

Add the key to the ssh-agent

```
ssh-add ~/.ssh/id_rsa
```

You should not be asked for a username or password. If it works, your SSH key is correctly configured.