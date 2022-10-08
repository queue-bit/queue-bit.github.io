---
title:  "Gnome Seahorse"
excerpt: "You can use Gnome's Seahorse (Passwords and Keys) to handle SSH keys, this is particularly useful when working with GitHub."
tags: "gnome seahorse ssh keys github"
---

1. Open `Password and Keys` (this app is known as [_Seahorse_](https://wiki.gnome.org/Apps/Seahorse/))
2. Click `+`
3. Select `Secure Shell Key`
4. Enter a description of the key
5. Click `Advanced key options`
    - Set Encryption Type to RSA
    - Set Key Strength to 4096
6. Click `Just Create Key`
7. In a CLI (terminal)
   1. Install xclip:
       ```bash
       sudo apt install xclip
       ```
   2. Copy the key to your clipboard:
       ```bash
       cat ~/.ssh/{keyname}.pub | xclip -i -sel clip
       ```
8. In GitHub
   1. Open [SSH and GPG keys (https://github.com/settings/keys)](https://github.com/settings/keys)
   2. Click `New SSH key`
   3. Enter a title
   4. Paste the key 