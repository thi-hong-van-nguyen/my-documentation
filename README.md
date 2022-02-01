# When change to new computer and can't push new repo to new repo on GitHub
### ERROR: 
```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

1. What you can do is open Git Bash, type in `ssh-keygen`, hit enter until it's done. 
  ``ssh-keygen -t ed25519 -C "thinguyen.webdev@gmail.com"``
2. Then type `cat ~/.ssh/id_rsa.pub` or `cat ~/.ssh/id_dsa.pub`. copy the whole string including your email
3. open GitHub -> setting -> SSH key -> generate new SSH -> paste the string into SSH key section and save
4. git add. commit and push
