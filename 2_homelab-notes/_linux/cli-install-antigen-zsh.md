---
title:  "Install Antigen for ZSH"
intro: "At the time of writing (March 2020), the version of ZSH Antigen included in Mint's apt was not up-to-date, here's how to install it directly."
description: "How to manually install ZSH Antigen."
tags: "ubuntu,debian,mint,zsh,antigen"
date: "2020-03-17"
---

Seems the version of [zsh-antigen](https://github.com/zsh-users/antigen) that's included in _apt_ isn't up to date and can cause errors when opening a new session in Mint.

### Remove Antigen installed via apt

If you've installed Antigen via apt, remove it:

```bash
sudo apt remove zsh-antigen
```

### Download Antigen

1. Create a directory:

    ```bash
    sudo mkdir /usr/share/zsh-antigen
    ```

2. Download `antigen.zsh` directly:

    - Before you do this next step, verify that [git.io/antigen](git.io/antigen) takes you to https://raw.githubusercontent.com/zsh-users/antigen/master/bin/antigen.zsh (trust no one), then:

        ```bash
        sudo curl -o /usr/share/zsh-antigen/antigen.zsh -sL git.io/antigen
        ```

### Configure

3. Edit `.zshrc` in your favorite text editor
    - Add the following near the top:

        ```bash
        source /usr/share/zsh-antigen/antigen.zsh
        ```
    - Near the bottom:

        ```bash
        antigen apply
        ```

    - Any antigen theme you want to install would go somewhere between those two lines... something like:

        ```bash
        source /usr/share/zsh-antigen/antigen.zsh
        # A bunch of other config stuff here
        # and maybe more stuff here
        antigen theme romkatv/powerlevel10k
        # That previous line is the theme I'm using
        antigen apply
        ```

### Finish it

4. Restart the CLI sessions (close and open the terminal)
5. Follow the prompts (if any)