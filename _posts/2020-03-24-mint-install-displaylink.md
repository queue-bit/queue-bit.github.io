---
layout: default
title:  "Linux Mint - Install DisplayLink Software"
---

# Linux Mint - Install DisplayLink Software

The [guide on displaylink.com](https://support.displaylink.com/knowledgebase/articles/684649-how-to-install-displaylink-software-on-ubuntu) for Ubuntu works on Mint, tested in Linux Mint 19.3 Tricia.

Download the latest driver from [https://www.displaylink.com/downloads/ubuntu](https://www.displaylink.com/downloads/ubuntu)

## Hiccups
The one snag I ran into was it got stuck on the `Building EVDI kernel module with DKMS` step. I didn't capture the output so this will be a bit sparse on details.

Since there's no easy way to kill the installer at this step (CTRL+C / Break will not work) I checked what DKMS processes were running:

```bash
ps aux | grep dkms
```

I then killed those processes that were related to the installer (should be obvious based on the process name)

```bash
sudo kill -HUP {process ID}
```

For example, if the process ID was 8088:

```bash
sudo kill -HUP 8088
```

Then I re-ran the run file as per the guide and all worked well.
