---
title:  "Create a shortcut for connecting to your remote server through terminal" 
excerpt: "Instead of constantly writing out the SSH command to connect to remove servers, create an alias for it."
date: 2025-09-29
header:
  teaser: 
categories:
  - macOS
tags:
  - macOS
  - linux
  - tip
---

If you constantly have to SSH into a remote server (like if you are a researcher connecting to an HPC almost daily if not multiple times a day), it can get really tiring to type out the command each time. So, you can create an alias in your configuration file (usually a `.bashrc` or `.zshrc` file).

So instead of typing the full command like this:

![Screenshot of terminal with the full command to SSH into HPC](/assets/images/posts/2025-09-29-shortcut-ssh-through-terminal-1.png)

To writing a shortcut like this:

![Screenshot of terminal with the shortcut to SSH into HPC](/assets/images/posts/2025-09-29-shortcut-ssh-through-terminal-2.png)

---

To do this, add the following line to your `.bashrc` or `.zshrc` file in your home directory.

```bash
alias hpc="ssh user@hpc3.rcic.uci.edu"
```

Where `alias` creates the shortcut, `hpc` is the name of the shortcut and `="ssh user@hpc3.rcic.uci.edu"` is the command that will run when calling the shortcut `hpc`.

For example, I constantly log into the HPC and our local lab server, so I have two lines that look something like this:

```bash
alias hpc="ssh jsakr@hpc3.rcic.uci.edu"
alias labserver="ssh jsakr@labserver.uci.edu"
```
Make sure all the shortcut names are unique!

---

# Copy and Paste

You can copy and paste the following line and update it with your information!

```bash
alias hpc="ssh user@hpc3.rcic.uci.edu"
```