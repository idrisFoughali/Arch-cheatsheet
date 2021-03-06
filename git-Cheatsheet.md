## enforce ssh instead of https for git cloning:
This will replace all the git clone commands url with ssh.

```console
 git config --global url."ssh://git@".insteadOf https://
 ```
 
 
## Github/Gitlab SSH-keys:
Generate a new certificate for the specific user:
For example, for ED25519:
1: 
``` console
$ ssh-keygen -t ed25519 -C " < username or email > "
```

For 2048-bit RSA:
2: 
``` console
ssh-keygen -t rsa -b 2048 -C
```

Bind it to the SSH engine on your host:
a. temporaraly:
``` console
$ eval `ssh-agent -s` && ssh-add /path/to/certificate
```

b. permanantly:
modifiy your ssh profile: 
vi ~/.ssh/config
``` console
host node_name
 User < username or email >
 IdentityFile /path/to/certificate
```

test your ssh key:
``` console
ssh -T git@<repo_or_project_url>
```

Feature branches:
Either a new feature from source, or an orphan branch without history.

How to create an orphan branch:
``` console
git switch --orphan features/< new-branch >
git rm -rf --cached .
git rm .gitignore
git add -A
git commit --allow-empty --message "Feat: new orphan branch"
git push --set-upstream origin features/< new-branch >
```


 
