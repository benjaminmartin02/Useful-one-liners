# Useful-one-liners
Miscellaneous one-liners. These are simple solutions I would repeatedly google, so putting them here for future reference. 


## AWK

### remove duplicates

Use *!seen* to remove lines with duplicates in specified column (in example, column 3)
```
awk '!seen[$3]++' filename
```