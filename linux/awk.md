###convert multiple line into one line
```
cat test.txt | awk NF=NF RS= OFS= > test.txt
```