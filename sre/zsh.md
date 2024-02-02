### History
`Up Arrow` : Recall the previous command in history  
`Down Arrow` : Recall the next command in history  
`CTRL + R` : Search the command history  
`CTRL + G` : Escape from command search mode  
`!!` : Execute the last typed command  
`!pw` : Execute the last command in history that begins with pw
### Auto-completion
`TAB` : Auto-complete the typed command  
`TAB TAB` : Show list of commands  
`TAB TAB TAB ...` : Cycle through matched commands
### List all Keyboard Shortcuts
` bindkey`


### How to find out the process id using a specific port :

```shell
lsof -nP -iTCP:80 -sTCP:ESTABLISHED

lsof -PiTCP -sTCP:LISTEN

ps -ef
```

### How to add ssh key to keychain:

```shell
ssh-add --apple-use-keychain your_private_key_name

```
### .zprofile
    .zlogin and .zprofile do the same thing. They set the environment for login shells. 
    The only difference is they just get loaded at different times (see below). 
    I would use .zprofile at all times for consistence.

### .zshrc
    .zshrc sets the environment for interactive shells. .zshrc gets loaded after .zprofile.
    It is a place where you “set and forget” things.
    Since it’s loaded after .zprofile, in interactive shells, it will override anything you set in .zprofile. 
    Like the $PATH variable. It’s a good place to define aliases and functions that you would like to
    have both in login and interactive shells (see the sidenote below).
### .zshenv
    This is read first and read every time, regardless of the shell being login, interactive, or none.

    This is the recommended place to set environment variables, though I still prefer to set my environment variables in .zprofile
    
    Why would you need it? Because, for example, if you have a script that gets called by launchd, it will run under non-interactive non-login shell,
    so neither .zshrc nor .zprofile will get loaded.
    
    I’ve never needed to use this file so far, but it’s there if you need it, and there is nothing wrong with using it to define envinronment variables.

### .zlogout
    This file is read when you log out of a session. Useful for cleaning things up.
### File Load Order
    Here’s the order these profile files are processed, without getting into too much detail:
    .zshenv → .zprofile → .zshrc → .zlogin → .zlogout
