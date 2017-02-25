---
title: "Get Root Access through emacs"
categories: Blog
type: post
---

Let's say you are on the command line as a group user and not root and you want to access ~/.emacs.d/.

Open emacs with root privileges (i.e. sudo), type ALT-x shell. This opens a new buffer representing a shell with user privileges (you are using 
emacs with user privilege after all).

Now you can access ~/.emacs.d/. I haven't tried executing anything else requiring root privileges, but I assume it will work as well.
