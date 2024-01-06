###use scope to limit library files
```
e.g. only dispaly files in spring framework core,beans and context packages.
lib:org.springframework.core..*
lib:org.springframework.beans..*
lib:org.springframework.context..*
```
https://www.jetbrains.com/help/idea/2020.2/scope-language-syntax-reference.html

###cannot start up due to Address already in use: bind
```
run cmd as admin

net stop winnat
net start winnat
```
