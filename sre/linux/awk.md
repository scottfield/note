###convert multiple line into one line
```
cat test.txt | awk NF=NF RS= OFS= > test.txt
```

###print substring
```
 grep -i "completed" rawlogs.log| awk -F "COMPLETED] in " '{print substr($2,1,6);}'
```
