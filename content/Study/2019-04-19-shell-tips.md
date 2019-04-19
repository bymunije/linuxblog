---
title: shell tips
author: Bymunije
date: '2019-04-19'
slug: shell-tips
categories:
  - Study
tags: 
  - Shell
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---
## 1.add header
```
#!/bin/bash
for file in /home/byzhang/data/Drug_combination/header/*.txt
do
	file_name_txt=`basename $file`
	file_name=${file_name_txt%.*}
	add_header=${file_name}_header.txt
	echo $add_header
	head -n 1 ${file} > ./header/add_header/${add_header}
done


cd /home/byzhang/data/Drug_combination/header/add_header
paste SL_score_first_modify_header.txt Cancer_Mutation_Score_Modify_header.txt cancer_gene_sensus_TSG_header.txt Drug_Target_inhibitor_all_deduplication_header.txt | tr -d "\r" > add_header.txt 
```
```
#!/bin/bash
for file in ./no_header_wt/*.txt
do
	 file_name=${file##.*/}
	 #split_mut_wild_wt_PTGS2+TP53_Valdecoxib-341.txt
	 before=${file_name%-*}
	 #split_mut_wild_wt_TOP1+TP53_Topotecan
	 Index_txt=${file_name##s*-}
	 #split_mut_wild_wt_TOP1+TP53_Topotecan-
	 Index=_${Index_txt%.*t}
	 #number
	 withHeader="_withHeader.txt"
	 add_withHeader="$before$Index$withHeader"
	 # echo ${file_name} , ${before} , ${Index} , ${add_withHeader}
	cat split_mut_wild_selected_GDSC_header.txt ${file} > ./split_every_drug_wt_withHeader/${add_withHeader}
done
```