###use jcmd to diagnose jvm
- get available commands of java process
```
jcmd java_pid help
```
- get jvm version
```
jcmd 31492 VM.version
```
- get system properties of jvm
```
jcmd 31492 VM.system_properties
```

- get flags of jvm
```
jcmd 31492 VM.flags
```

- get commandline arguments of jvm
```
jcmd 31492 VM.command_line
```

