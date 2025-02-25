---
title: Github ssh
date: 2024/1/5 12:00:00 -500
categories: [github, ssh]
tags: [github, ssh]    # tags should allways be lowercase
---

```bash
sudo su
ssh-keygen
cd /root/.ssh
chmod 600 ~/.ssh/id_ed25519.pub
ssh-add
eval "$(ssh-agent -s)" 
git remote -v		
ssh-add id_ed25519.pub		
ssh -T GITHUB-username@github.com		
ssh -vT git@github.com	
```

# Connecting to GitHub with SSH


* we will make a new ssh key
* add the pub key to github 
* to enable safer uploads 


```bash
sudo su
ssh-keygen
```

------------------------------------------------------------------------------------

directory

* the default directory were the keys will be saved

* you may change the directory if you want or change the key name

* and remember to use a strong passwrord

```bash
/home/username/.ssh/id_ed25519
```

------------------------------------------------------------------------------------

permissions

* cd into the directory

* and elive the permissions

* change the id_ed25519.pub name to fit the one you have

```bash
chmod 600 ~/.ssh/id_ed25519.pub
```

------------------------------------------------------------------------------------
Add the specified private  



```bash
ssh-add
```

------------------------------------------------------------------------------------
config

* Starts a new SSH agent in the background

*  sets environment variables to allow other programs

* (like Git) to communicate with it



```bash
eval "$(ssh-agent -s)" 
```

------------------------------------------------------------------------------------
Git remotes

* (repositories), along with their URLs and associated fetch and push protocols.


```bash
egit remote -v
```

------------------------------------------------------------------------------------

Initiates an SSH

* It establishes a secure connection to the GitHub server using the SSH protocol.

* change the user-name to your github user-name

* Does not execute a command: The -T flag instructs ssh to only test the authentication.

```bash
ssh -T GITHUB-user-name@github.com
```

------------------------------------------------------------------------------------
conecting

* SSH connectivity and authentication with GitHub



```bash
ssh -vT git@github.com
```

------------------------------------------------------------------------------------
