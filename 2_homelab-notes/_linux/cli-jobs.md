---
title:  "CLI Jobs & Processes"
intro: "Some CLI commands for moving processes into the background and back to foreground."
description: "How to move processes to background and back to foreground in the CLI."
tags: "linux,shell,bash,zsh,sh,rbash,dash,jobs,suspend,bg,fg,cli"
date: "2021-01-30"
---

### Jobs & Processes

| To | Command |
|-|-|
| Suspend currently running process | CTRL+Z (`^Z`)|
| [List jobs](#list-jobs) | `jobs` or `jobs -l`|
| [Resume last suspended process](#resume-last-suspended-process) | `fg` |
| [Resume specific suspended process](#resume-a-specific-suspended-process) | `fg %{job-id}` |
| [Send process to background](#send-process-to-background) | `bg %{job-id}` |
| [Suspend a background process](#suspend-a-background-process) | `kill -STOP %{job-id}` |

#### List Jobs

```bash
~ jobs
[1]  + running    bundle exec jekyll serve

~ jobs -l
[1]  + 36448 running    bundle exec jekyll serve
```

#### Resume Last Suspended Process

```bash
~ fg
[1]  + running    bundle exec jekyll serve
```

#### Resume a Specific Suspended Process

```bash
~ jobs
[1]  + suspended  bash
[2]  + suspended  bundle exec jekyll serve

~ fg %2
[2]  + continued  bundle exec jekyll serve
      Regenerating: 1 file(s) changed at 2021-01-30 12:50:19
                    _linux/2021-01-30-cli-commands.md
```

#### Send Process to Background

```bash
~ bundle exec jekyll serve
Configuration file: /path/_config.yml
            Source: /path
       Destination: /path/_site
    Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 1.774 seconds.
 Auto-regeneration: enabled for '/path'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
^Z
zsh: suspended  bundle exec jekyll serve
~ jobs
[1]  + suspended  bundle exec jekyll serve
~ bg %1
[1]  + continued  bundle exec jekyll serve
~
```

#### Suspend a Background Process

```bash
~ jobs
[1]  + running    bundle exec jekyll serve
~ kill -STOP %1
[1]  + suspended (signal)  bundle exec jekyll serve             
```