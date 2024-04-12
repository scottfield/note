### install package
```shell

python -m pip install SomePackage   # latest version
python -m pip install SomePackage==1.0.4    # specific version
python -m pip install "SomePackage>=1.0.4"  # minimum version
```
### upgrade package
```shell
python -m pip install --upgrade SomePackage
```

### create virtual environment
```shell
python -m venv /path/to/new/virtual/environment
python -m venv venv
```

### activate the virtual environment
```shell
source <venv>/bin/activate

#after activation you can deactivate via below command
deactivate
```