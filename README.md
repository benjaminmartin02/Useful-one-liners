# Useful-one-liners
Miscellaneous one-liners. These are simple solutions I would repeatedly google, so putting them here for future reference. 


## AWK

### remove duplicates

Use *!seen* to remove lines with duplicates in specified column (in example, column 3)
```
awk '!seen[$3]++' filename
```

### grep on a column

pull out lines matching "string" in a specific column (like grep on a column):
```
awk '$6 ~ /string/' 
```

### pull out lines matching input list
eg. gene ids... this would pull out rows with gene IDs in 1st column matching *gene_ids.txt*
```
awk 'NR==FNR{a[$1];next}{if ($1 in a) {print $0}}' gene_ids.txt inputfile.txt
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




## R

### get file paths to read in a loop

Give path to directory (here: __Liver_cancer/*/*/*__) and then pattern in file name to match (here: __"htseq.counts.gz"__)
```
matFiles <- dir(Sys.glob(file.path("Liver_cancer/*/*/*")), pattern = "htseq.counts.gz", full.names = T)
```
Then can derive simplified names to match each file using gsub and basename functions
```
matNames <- gsub(".htseq.counts.gz","",basename(matFiles),fixed=T)
```
Then can read samples in with a loop
```

```
