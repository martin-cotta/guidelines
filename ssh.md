## SSH Identities (OS X)

SSH keys are a way to identify trusted computers without involving passwords. They are based on the SSH cryptographic network protocol, which is responsible for the encryption of the information stream between you and the remote machine.
Since OS X Leopard (10.5.1), `ssh-agent` runs automatically for you. It will also integrate with the keychain, so you can unlock your keys with it.

```sh
$ ls -al ~/.ssh            # checking for existing keys
$ ssh-add -l               # lists fingerprints of all identities loaded
$ wwh-add -D               # deletes all identities from the agent
$ ps -e | grep [s]sh-agent # running agent(s)
```

#### Quick version (TL;DR)

```sh
$ ssh-keygen -t rsa -b 4096 -f ~/.ssh/github_rsa -C "user@domain.com" 
$ /usr/bin/ssh-add -K ~/.ssh/github_rsa 
$ pbcopy < ~/.ssh/github_rsa.pub # copy public key to use it at github.com
$ ssh -T git@github.com
```
--- 

#### Generating public/private rsa key pairs

```sh
$ ssh-keygen -t rsa -b 4096 -f ~/.ssh/github_rsa -C "github@example.com"
$ ssh-keygen -t rsa -b 4096 -f ~/.ssh/bitbucket_rsa -C "bitbucket@example.com"
$ ssh-keygen -t rsa -b 4096 -f ~/.ssh/personalid -C "personalid"
```

#### Changing the passphrase of a private key file

```sh
$ ssh-keygen -p -f ~/.ssh/personalid
# If the selected key already has a passphrase, 
# you will be prompted to enter it before you can change to a new passphrase
```

#### Adding private key identities to the ssh-agent (and system's keychain)

The `-K` option will integrate with system's keychain, make sure you're using the default OS X `/usr/bin/ssh-add` command, and not one installed by macports, homebrew, or some other external source.

```sh
$ ssh-add -K # default keys (id_rsa, id_dsa, & identity)
$ ssh-add -K ~/.ssh/github_rsa
$ ssh-add -K ~/.ssh/bitbucket_rsa
```

#### Add Public keys to GitHub/BitBucket

```sh
$ pbcopy < ~/.ssh/github_rsa.pub	# paste in https://github.com/settings/ssh
$ pbcopy < ~/.ssh/bitbucket_rsa.pub # paste in https://bitbucket.org/account/user/USERNAME/ssh-keys/
```	

#### SSH Config file (Optional)

Create or edit the SSH config file at: `~/.ssh/config`

```text
# GitHub
Host github.com
 HostName github.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/github_rsa

# BitBucket
Host bitbucket.com
 HostName bitbucket.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/bitbucket_rsa
```
	 
#### Testing SSH connection

```sh
$ ssh -T git@github.com
$ ssh -Tv git@bitbucket.org

$ ssh -Tv git@github.com
$ ssh -Tv git@bitbucket.org

$ ssh -T -ai ~/.ssh/github_rsa git@github.com # connect to GitHub using a specific ssh key
$ ssh -T -ai ~/.ssh/bitbucket_rsa git@bitbucket.com # connect to BitBucket using a specific ssh key
```

#### Switching remote URLs from HTTPS to SSH

```sh
$ git remote -v
# origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
# origin  https://github.com/USERNAME/REPOSITORY.git (push)
$ git remote set-url origin git@github.com:USERNAME/OTHERREPOSITORY.git
$ git remote -v
# origin  git@github.com:USERNAME/OTHERREPOSITORY.git (fetch)
# origin  git@github.com:USERNAME/OTHERREPOSITORY.git (push)
```

The permissions of the ~/.ssh and its files can be properly set with:

```sh
chmod go-w ~/
chmod 700 ~/.ssh
chmod 600 ~/.ssh/*
chmod 644 ~/.ssh/*.pub
```	

[0]:https://help.github.com/categories/ssh/
[1]:http://stackoverflow.com/questions/29331153/git-bitbucket-private-submodule-ssh-alias-issues
