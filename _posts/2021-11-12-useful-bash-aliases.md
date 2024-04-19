---
title: 10 Useful BASH Aliases
categories:
  - Help File
tags:
  - Linux
  - Bash
---

BASH aliases are a handy way to create shortcuts for commands you use frequently or may otherwise be long and tedious to remember. I'll briefly explain how to create BASH aliases and then show you a few of the ones I use everyday.

## How to Write a BASH Alias

The syntax for an aliases is pretty straightforward:

```sh
    alias alias_name='command_to_run'
```

An alias declaration starts with the `alias` command followed by the alias name, an equal sign, and the command you want to run when you type the alias. The command needs to be enclosed in quotes and with no space around the equal sign, and each alias needs to be declared on a new line in the `~/.bash_aliases` file.

You can use gedit to edit the `~/.bash_aliases` file:

```sh
    gedit ~/.bash_aliases
```

Let's look at a quick example. The `ls` command is probably one of the most used commands in Linux. When executed, it will list the contents of a directory. I frequently use it with the `-la` flags to list hidden files and file properties. Rather than typing `ls -la` every time, we can create an alias called `ll`.

```sh
    alias ll='ls -la'
```

Now, to execute `ls -la`, we only need to type `ll` at the command line. Note that if you added that alias to the `~/.bash_aliases` file, you need to reload BASH before it will work:

```sh
    source ~/.bashrc
```

If you just typed the alias into the terminal, you will need to add it to the `~/.bash_aliases` file to make it persistent, otherwise the alias will only work in the current terminal session.

You can name your aliases just about anything you want, but it is a good practice to make them something memorable and related to the command you are aliasing.

## 10 Useful BASH Aliases

To add one of these aliases to your `~/.bash_aliases` file, simply copy and paste the command into a terminal beginning with `echo`. And don't forget to reload your `.bashrc` file.

### 1
Normally, to navigate up one directory in the terminal, you have to type `cd ..`, this alias shortens that command to just `..` :

```sh
    echo "alias ..='cd ..'" >> /home/$USER/.bash_aliases
```

### 2
Similar to the above alias, this alias will change your current working directory to your user home folder by simply typing `~` :

```sh
    echo "alias ~='cd ~/'" >> /home/$USER/.bash_aliases
```

### 3
This is a quick way to get your public internet IP address by simply typing `myip` :

```sh
    echo "alias myip='curl checkip.amazonaws.com'" >> /home/$USER/.bash_aliases
```

### 4
Here's a fun one. Get the current weather for your location right in the terminal:

```sh
    echo "alias weather='curl wttr.in'" >> /home/$USER/.bash_aliases
```

### 5
Run a full update of your Linux system with one command, `update` :

```sh
    echo "alias update='sudo apt update && sudo apt -y upgrade && sudo apt -y autoremove'" >> /home/$USER/.bash_aliases
```

### 6
Sometimes you just want a list of what updates are available before you install them. You can find out by typing `whichupdates` :

```sh
    echo "alias whichupdates='sudo apt update && apt list --upgradeable'" >> /home/$USER/.bash_aliases
```

### 7
This is one of my favorites. It tells you the size of files and directories in your current working directory. This makes it easy to track down large files:

```sh
    echo "alias size='pwd && find ./ -type f -exec du -Sh {} + | sort -rh | head -n 15'" >> /home/$USER/.bash_aliases
```

### 8
Untaring a file should be easy. Now it is:

```sh
    echo "alias untar='tar -zxvf '" >> /home/$USER/.bash_aliases
```

### 9
This will quickly tell you what ports on your machine are open and what applications are using them.

```sh
    echo "alias ports='sudo netstat -tulanp'" >> /home/$USER/.bash_aliases
```

### 10
Everything you type in the terminal is saved and discoverable. Sometimes you might want to clear it all out:

```sh
    echo "alias clearall='clear && history -c && history -w'" >> /home/$USER/.bash_aliases
```
