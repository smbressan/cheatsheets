# Git config for multiple accounts: 
 One SSH Keypair should be configured for one git config.

1. Generate the SSH key

```ssh-keygen -t ed25519 -C "personal_email@example.com" -f ~/.ssh/<personal_key> ```

2. Adding a passphrase
It's an optional step but it's useful if someone gain access to the computer. This way, the key's won't get compromised.

```ssh-keygen -p -f ~/.ssh/<personal_key>```

3. Tell ssh-agent
We will use ssh-agent to securely save your passphrase. Make sure the ssh-agent is running and add your key (the -K option is to store the passphrase in your keychain, macOS only).
```
eval "$(ssh-agent -s)" && \
ssh-add -K ~/.ssh/<personal_key> 
```
4. Edit your SSH config
```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/<created_key>
```
Here we are setting Host to * for every key because we will use Git configs to select the appropriate SSH key based on profiles, which will give us a bit more flexibility

5. Copy the SSH public key
```
xclip -sel clip < ~/.ssh/<created_key>.pub
```

6. Structure your workspace for different profiles
Now, for each key pair (aka profile or account), we will create a .conf file to make sure that your individual repositories have the user settings overridden accordingly.
Let’s suppose your home directory is like that:
```
/myhome/
    |__.gitconfig
    |__work/
    |__personal/
```
We are going to create two overriding .gitconfigs for each dir like this
```
/myhome/
|__.gitconfig
|__work/
     |_.gitconfig.work
|__personal/
    |_.gitconfig.pers
```
7. Set up your Git configs
```
# ~/personal/.gitconfig.pers
 
[user]
email = your_pers_email@example.com
name = Your Name
 
[github]
user = “mynickname”
 
[core]
sshCommand = “ssh -i ~/.ssh/<personal_key>”
```
```
# ~/work/.gitconfig.work
 
[user]
email = your_pro_email@google.com
name = Your Name
 
[github]
user = “pro_name”
 
[core]
sshCommand = “ssh -i ~/.ssh/<professional_key>”
```

#### reference: https://res.cloudinary.com/da8kiytlc/image/upload/v1647871440/Cheatsheets/GitGuardian_GitHub_Accounts_Cheatsheet.pdf