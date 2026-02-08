---
title:  "Subset large BED file for testing code (Bash)" 
excerpt: "Simple bash command to subset a large BED file to use for quickly testing newly written code."
date: 2026-02-07
header:
  teaser: 
categories:
  - bioinformatics
tags:
  - bioinformatics
  - coding
  - bash
---


You want to test some code you wrote that manipulates or processes a BED file, here is how you can subset a large BED file that includes rows from each chromosome using bash (can be done as a one liner on the command line too). 

# Subset a BED file

Let's say you want to subset 1,000,000 rows per chromosome, you can run:
```bash
zcat ${file}.bed.gz | awk -F'\t' -v OFS='\t' '$1 ~ /^chr/ { chr=$1; if (count[chr] < 1000000) { print; count[chr]++ } }' | bgzip -c > ${file}_subset.bed.gz
```

This will decompress the file, set field separator to the tab character for the input and output, checks if first field starts with "chr", grabs up to 1,000,000 rows per chromosome before compressing to output file.

If you want to set the number of rows as a variable, it would look something like this:

```bash
limit=1000000
zcat ${file}.bed.gz | awk -F'\t' -v OFS='\t' '$1 ~ /^chr/ { chr=$1; if (count[chr] < '"$limit"') { print; count[chr]++ } }' | bgzip -c > ${file}_subset.bed.gz
```

If you are using an uncompressed BED file, you can run:
```bash
awk -F'\t' -v OFS='\t' '$1 ~ /^chr/ { chr=$1; if (count[chr] < '"$limit"') { print; count[chr]++ } }' ${file}.bed > ${file}_subset.bed
```

Happy code testing!