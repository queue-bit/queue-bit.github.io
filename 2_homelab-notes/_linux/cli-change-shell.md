---
title:  "Change Default CLI Shell"
intro: "bash, zsh, sh, oh my!"
description: "bash, zsh, sh, oh my!"
tags: "linux,shell,bash,zsh,sh,rbash,dash,cli"
date: "2020-03-16"
---

### Using chsh

From the manual:
>  __The _chsh_ command changes the user login shell.__ This determines the name of the user's initial login command. A normal user may only change the login shell for her own account; the superuser may change the login shell for any account.


```bash
chsh -s {/path/to/shell} {username}
```

#### Examples

##### Change the shell for current (logged in) user

```bash
chsh -s /bin/zsh
```

##### Change the shell for another user (logged in as root)

```bash
sudo chsh -s /bin/zsh hsimpson
```

Where _hsimpson_ is the user ID.

#### Check available shells
```bash
cat /etc/shells 

# /etc/shells: valid login shells
/bin/sh
/bin/bash
/bin/rbash
/bin/dash
/bin/zsh
```
