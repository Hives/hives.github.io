---
layout: post
title: Trouble using SSH to connect to GitHub
date: 2019-02-13 18:56 +0000
category: makers
tags: [git, github, ssh]
---

Today I was working at a friend's house, and when I tried pushing a repo to
GitHub, the command seemed to hang. Google suggested the problem might be
something to do with the SSH connection, so I tested it like this:

```shell_session
$ ssh -v -T git@github.com
OpenSSH_7.9p1, OpenSSL 1.1.1a  20 Nov 2018
debug1: Reading configuration data /home/hives/.ssh/config
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Connecting to github.com [62.252.172.241] port 22.
debug1: connect to address 62.252.172.241 port 22: Connection timed out
ssh: connect to host github.com port 22: Connection timed out
```

i.e. the connection was timing out.

Then I found this blog post:
<https://bengsfort.github.io/articles/fixing-git-push-pull-timeout/>

I tried what he was suggesting, and added this to my ~/.ssh/config:

```
Host github.com
  Hostname ssh.github.com
  Port 443
```

Then I tested my GitHub SSH connection again:

```shell_session
$ ssh -T git@github.com
The authenticity of host '[ssh.github.com]:443 ([192.30.253.123]:443)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[ssh.github.com]:443,[192.30.253.123]:443' (RSA) to the list of known hosts.
Hi Hives! You've successfully authenticated, but GitHub does not provide shell access.
```

... and after that `git push` worked.

In the evening, when I was back on my home network, I commented out those extra
lines from my ~/.ssh/config and found I now had no problem SSH-ing to GitHub.

So what was happening? And what did the solution do?

According to [this GitHub
help page][using-ssh-over-the-https-port]:

> Sometimes, firewalls refuse to allow SSH connections entirely. If using HTTPS
> cloning with credential caching is not an option, you can attempt to clone
> using an SSH connection made over the HTTPS port. Most firewall rules should
> allow this, but proxy servers may interfere.

It's talking about cloning there, but I guess it applied to SSH-ing to GitHub in
general?  So I think my friend's internet connection was preventing me
connecting to GitHub's SSH port (22), but it was happy for me to connect to the
HTTPS port (443).  ¯\\\_(ツ)\_/¯

I've left those lines commented out in my ~/.ssh/config in case I ever need them
again.

This has also reminded me of something I've been meaning to read up on -
understanding properly how SSH public key authentication works.

[using-ssh-over-the-https-port]:https://help.github.com/articles/using-ssh-over-the-https-port/

