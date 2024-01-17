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
