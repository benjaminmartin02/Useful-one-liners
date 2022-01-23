# Useful-one-liners
Miscellaneous one-liners. These are simple solutions I would repeatedly google, so putting them here for future reference. 


## AWK

### remove duplicates

Use *!seen* to remove lines with duplicates in specified column (in example, column 3)
```
awk '!seen[$3]++' filename
```

### get TSS from TSS-TES BED
Take a TSS to TES BED file and get the TSS coordinates, sorts the output BED file by position
```
awk '{if($6=="+"){OFS="\t";print($1,$2,$2+1,$4,$5,$6)} else if($6=="-"){OFS="\t";print($1,$3-1,$3,$4,$5,$6)}}' TSS_TES.bed | sort -k 1,1 -k 2,2n > TSS.bed
```

### get TES from TSS-TES BED
Take a TES to TES BED file and get the TSS coordinates, sorts the output BED file by position
```
awk '{if($6=="+"){OFS="\t";print($1,$3-1,$3,$4,$5,$6)} else if($6=="-"){OFS="\t";print($1,$2,$2+1,$4,$5,$6)}}' TSS_TES.bed | sort -k 1,1 -k 2,2n > TSS.bed
```