---
layout: post
title: Trouble using ssh to connect to GitHub
category: makers
tags: 
---

```
➜ ssh -v git@github.com
OpenSSH_7.9p1, OpenSSL 1.1.1a  20 Nov 2018
debug1: Reading configuration data /home/hives/.ssh/config
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Connecting to github.com [62.252.172.241] port 22.
debug1: connect to address 62.252.172.241 port 22: Connection timed out
ssh: connect to host github.com port 22: Connection timed out
```

Found this blog post
<https://bengsfort.github.io/articles/fixing-git-push-pull-timeout/>

Updated my ~/.ssh/config like it says, and did this:

```
➜ ssh -T git@github.com
The authenticity of host '[ssh.github.com]:443 ([192.30.253.123]:443)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[ssh.github.com]:443,[192.30.253.123]:443' (RSA) to the list of known hosts.
Hi Hives! You've successfully authenticated, but GitHub does not provide shell access.
```

... and after that `git push` worked...
