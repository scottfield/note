###setup GOPATH
```
the default GOPATH is $userhome/go which contains three directories src pkg and bin
but you could setup to other DIR

```

###use go mod to copy modules into vendor folder
```
go mod vendor 
the above command will automatically discover and copy the depencies to vendor folder
```