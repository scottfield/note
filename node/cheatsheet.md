###use chrome dev tool to analyze node application
```
step 1:
start node application which following node parameters:
--expose-gc --inspect

step 2:
open chrome and visit chrome://inspect
click the on remote target item to view detail of application.
```
#### add symbol link to test local npm module
```
this command line will create a symbol link in module "another-module"'s node_modules folder
which reference "test-module"
mklink /D "C:\projects\another-module\node_modules\test-module" "C:\projects\test-module"
```