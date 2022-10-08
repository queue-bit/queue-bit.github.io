---
title:  "Github Pages Tricks"
excerpt: ""
tags: "gh-pages, github pages, github"
---

## Multiple Repos with Github Pages

If you have Github Pages set up with a domain (on your repo `/user/user.github.io/`) and you create another repository with pages, the second repository will be available as a path on the original domain.

**For example:**

[www.andreaswiebe.com](https://www.andreaswiebe.com) is configured with github pages on `queue-bit/queue-bit.github.io`, if you visit [www.andreaswiebe.com](https://www.andreaswiebe.com) you get my website.

If I then create another repository `queue-bit/test`, and deploy github pages to it, it will be available at `www.andreaswiebe.com/test/`