---
title: Python code
author: Bymunije
date: '2019-04-19'
slug: python-code
categories:
  - Study
tags:
  - Python
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---

# <font color=orange size=6>Basic code</font>

## 1.split ['a;b'] to ['a'],['b']
```
split_target = open("Processing_target_nan_split.txt",'w')
with open('Processing_target_nan_withHeader.txt') as Processing_target:
	count = 0
	for line in Processing_target:
		count += 1
		try:
			line = line.replace('\n','')#去掉末尾换行符
			Target = line.split('\t')[7].split(";")[:]#split
			Index_drug = line.split("\t")[0]
			Index_cellLine = line.split("\t")[1]
			AUC = line.split("\t")[2]
			cellLine_name= line.split("\t")[5]
			DrugName = line.split("\t")[6]
			for t in Target:
				split_target.write(('\t').join([str(i) for i in [Index_drug,Index_cellLine,AUC,cellLine_name,DrugName,t]]) + '\n')#最后一定要加换行符
		except:
			with open('./Error.txt','a') as h:
				h.write('%s :%s have error! \n' % (str(count),line))
split_target.close()
```
## 2.Window和Linux文件中粘贴时末尾的换行符
```
os.system('paste {} {} | tr -d "\r" > {}'.format('a.txt','b.txt','a_b.txt'))
```
## 3.Python3和Python2
#### (1). 中文字符
```
# -*- coding: UTF-8 -*- 
```

- Python2

```
import sys
reload(sys)
sys.setdefaultencoding('utf-8')
```

- Python3

```
import sys
import importlib
importlib.reload(sys)
```

#### (2).写文件

- Python2

```
with open('file.txt','w') as g:
    for i in dict.keys():
        print >>g, ('\t').join([str(i) for i in dict[key])
```

- Python3

```
with open('file.txt','w') as g:
    for i in dict.keys():
        print(('\t').join([str(i) for i in [key] +dict[key]),file = g)
```

#### (3).字典

##### <1>.测试字典是否包含指定的键item

- python 2

```
if dict.has_key(item): #中间
```

- python 3

```
if item in dict: #最快
if item in dict.keys()： #最慢
```

##### <2>.查看字典中键和值

- python 2

```
print(dict.keys()[0:5])#键
print(dict.values()[0:5])#值
```

- python 3

```
print(list(dict.keys())[0:5])#键
print(list(dict.values())[0:5])#值
```

## 4.list和str转

#### <1>. list to str

```
list = ['www', 'google', 'com']
list_to_str = ";"join(list)
```

- 输出为：'www;google;com'

#### <2>. str to list

```
str = 'www.google.com'
str_to_list = str.split('.')
```

- 输出为：['www', 'google', 'com']

## 5.Pandas读取文件

+ `header=None`:不把第一行作为列属性

```
ata1=pd.read_csv=("test.csv")#自动把第一行作列属性，第一行不能用
data2pd.read_csv("test.csv",header=None)#不把第一行作列属性
```

## 6.DataFrame操作

#### 1. 创建空的dataframe

```
df = pd.DataFrame(columns = list())
```

#### 2.Series合并

`df=pd.concat([series1,series2],axis=1)`,默认情况按照`axis = 0`进行`行`连接，`axis = 1`为按照`列`连接，示例可参考[这里](https://blog.csdn.net/xiaodongxiexie/article/details/71774594)

#### 3.合并列数据为新列

- 如果某一列是非`str`类型的数据，需要用`map(str)`做转换
```
dataframe["newColumn"] = dataframe["age"].map(str) + dataframe["phone"] + dataframe["address"]
```
#### 4.Dataframe中按照某一列对dataframe重新排列

- 降序排列
```
df.reindex(df['col_1'].abs().sort_values(ascending=False).index)
```
- 升序排列
```
df.reindex(df['col_1'].abs().sort_values(ascending=True).index)
```

## 7. 循环存储图片

- 画图结束后要添加`plt.close()`,否则会在同一张图上反复画
- 不要`plt.show()`后再储存，因为`plt.show()`后会默认清空，储存的图片回事空白

## 8.选择列表中最长的字符串

`max(list,key = len)`

```
mylist = ['123','123456','1234']
print (max(mylist, key=len))
out:123456
```

## 9.字符串操作

1). `string.strip()`: 去除**头尾**字符和空白符（包括\n、\r、\t、' '，即：换行、回车、制表符、空格）
2). `string.lstrip()`: 去除**开头**字符和空白符（包括\n、\r、\t、' '，即：换行、回车、制表符、空格）
3). `string.rstrip()`: 去除**结尾**字符和空白符（包括\n、\r、\t、' '，即：换行、回车、制表符、空格）
- 这些函数只删除头尾的字符，中间的不会删除
- 返回的是去除字符的string副本，string本身不会发生改变

***
# Important Code
### 1.将文件分成10部分

```
import numpy as np 
import pandas as pd 
import sys
import os
import time

part_number = 10

reload(sys)
sys.setdefaultencoding('utf-8')

print('{}\t{}\n'.format(time.ctime(), 'start to analyze!'))

SL_ReDisease_score_withHeader = pd.read_csv('SL_ReDisease_score_withHeader.txt',sep='\t').values
os.system('head -n 1 {} > {}'.format('SL_ReDisease_score_withHeader.txt','SL_ReDisease_score_withHeader_header.txt'))
print(len(SL_ReDisease_score_withHeader))

a = len(SL_ReDisease_score_withHeader)

for i in range(part_number):
	if i < part_number - 1:
		SL_ReDisease_score_withHeader_part = SL_ReDisease_score_withHeader[int(i*(a/10)):int((i+1)*(a/10))].tolist()
	else:
		SL_ReDisease_score_withHeader_part = SL_ReDisease_score_withHeader[int(i*(a/10)):].tolist()

	filename = "SL_ReDisease_score_withHeader_{}_temp.txt".format(i+1)
	with open(filename,'w') as m:
		for j in SL_ReDisease_score_withHeader_part:
			print >>m, ('\t').join([str(x) for x in j])

	os.system('cat {} {} > {}'.format('SL_ReDisease_score_withHeader_header.txt', filename, "SL_ReDisease_score_withHeader_{}.txt".format(i+1)))
	os.system('rm -r *temp.txt')
```

### 2.添加Index和search以及多进程

```
#!/usr/bin/env python
import numpy as np 
import pandas as pd 
import sys
import os
import time
import re
# from re_module import re_module_search
reload(sys)
sys.setdefaultencoding('utf-8')

print('{}\t{}\n'.format(time.ctime(), 'start to analyze!'))


'''
add arguement
'''
import argparse
parser = argparse.ArgumentParser()  
parser.add_argument("-i", "--input", help="input file for analysis", required=True)
#parser.add_argument("-o", "--output", help="output file for analysis", required=True)  
args = parser.parse_args()  


SL_ReDisease_score_withHeader = pd.read_csv('{}'.format(args.input),sep='\t').values
# os.system('head -n 1 {} > {}'.format('SL_ReDisease_score_withHeader.txt','SL_ReDisease_score_withHeader_header.txt'))

ReDisease_MutationGene_Score = pd.read_csv('ReDisease_MutationGene_Score.txt',sep='\t').values

print(len(SL_ReDisease_score_withHeader))
print(len(ReDisease_MutationGene_Score))
# print('Step1 has been completed!')

SL_ReDisease_score = {}
ReDisease_MutationGene = {}

for i in range(len(SL_ReDisease_score_withHeader)):
	_key = str(SL_ReDisease_score_withHeader[i][0]).lower()+"#"+str(SL_ReDisease_score_withHeader[i][1]).lower()+"#"+str(SL_ReDisease_score_withHeader[i][2]).lower()+"#"+str(SL_ReDisease_score_withHeader[i][3]).lower()+"#"+str(SL_ReDisease_score_withHeader[i][4]).lower()+"#"+str(SL_ReDisease_score_withHeader[i][5]).lower()
	_value = np.array(SL_ReDisease_score_withHeader[i][0:],dtype = str).tolist()
	SL_ReDisease_score[_key] = _value

print(len(SL_ReDisease_score))
# print('Step2 has been completed!')

for i in range(len(ReDisease_MutationGene_Score)):
	_key = str(ReDisease_MutationGene_Score[i][0]).lower()+"#"+str(ReDisease_MutationGene_Score[i][4]).lower()+"#"+str(ReDisease_MutationGene_Score[i][1]).lower()
	_value = [str (i) for i in [str(ReDisease_MutationGene_Score[i][1])]+[str(ReDisease_MutationGene_Score[i][4])]+[str(ReDisease_MutationGene_Score[i][5])]]
	ReDisease_MutationGene[_key] = _value

print(len(ReDisease_MutationGene))
# print('Step3 has been completed!')
# print('Dictionary has been made! Start to search!')
#print(SL_ReDisease_score['10018#lymphoma;large-cell;follicular#bcl2'])
#print(ReDisease_MutationGene['10018#lymphoma;large-cell;follicular#bcl2'])
ReDisease_MutationGene_Score={}

ReDisease_MutationGene_index = {}
for _key in ReDisease_MutationGene.keys():
    id_3 = _key.split('#')[1]
    id_4 = _key.split('#')[2]
    new_key = id_3 + '#' + id_4
    _index = ReDisease_MutationGene.keys().index(_key)

    if ReDisease_MutationGene_index.has_key(new_key):
        ReDisease_MutationGene_index[new_key].append(_index)
    else:
        ReDisease_MutationGene_index[new_key] = [_index]
# print(ReDisease_MutationGene_index['lymphoma, follicular#mtor'])
def re_module_search(input1, input2):
    char = ''
    # for key1 in input1.keys():
    #     char += key1 + '\n'
    
    # n = re.findall('.*' + 'ki-1+ anaplastic large cell lymphoma' + '.*', char, re.MULTILINE)
    # if len(n) > 0:
    # 	print(n)
    # 	sys.exit(0)
    # else:
    # 	pass

    # sys.exit(0)

    for key2 in input2.keys():
        id_1 = key2.split('#')[2]
        id_2 = key2.split('#')[5]

        key3 = id_1 + '#' + id_2

        if ReDisease_MutationGene_index.has_key(key3):
            key3_index = ReDisease_MutationGene_index[key3]

            choosed_keys = np.array(input1.keys())[key3_index].tolist()

            for item in choosed_keys:
                char += str(item) + '\n'

            m = re.findall('.*' + id_1 + '#' + id_2 + '.*', char, re.MULTILINE)
            # m = re.findall('.*' + id_1 + '.*' + '#' + id_2 + '.*', char, re.MULTILINE)

            # if len(re.findall('.*' + id_1 + '#' + id_2 + '.*', char, re.MULTILINE)) > 0:
            #     m = re.findall('.*' + id_1 + '#' + id_2 + '.*', char, re.MULTILINE)
            # elif len(re.findall('.*' + id_1 + '#' + id_2 + '.*', char, re.MULTILINE)) == 0 and len(re.findall('.*' + id_1 + '.*' + '#' + id_2 + '.*', char, re.MULTILINE)) > 0:
            #     m = re.findall('.*' + id_1 + '.*' + '#' + id_2 + '.*', char, re.MULTILINE)
            # else:
            #     m = []

            # n = re.findall('.*anaplastic large cell lymphoma.*', key2)

            # if len(n) > 0:
            #     #print([key2]+[m[0]]+ReDisease_MutationGene[m[0]])
            #     print([n, id_1 + "#" + id_2, m])
            #     # print(m)
            #     #print(n)
            #     sys.exit(0)
            # else:
            #     pass

            #sys.exit(0)

            if len(m) > 0:            
                for i in range(len(m)):
                    id_3 = m[i].split('#')[1]
                    id_4 = m[i].split('#')[2]
                    if id_1 == id_3 and id_2 == id_4:
                        #print([key2,m[i]])
                        if ReDisease_MutationGene_Score.has_key(key2):
                            ReDisease_MutationGene_Score[key2].append(SL_ReDisease_score[key2] +ReDisease_MutationGene[m[i]])
                        else:
                            ReDisease_MutationGene_Score[key2] = [SL_ReDisease_score[key2] + ReDisease_MutationGene[m[i]]]
                    else:
                        ReDisease_MutationGene_Score[key2]= [SL_ReDisease_score[key2] +['&&']]
            else:
                ReDisease_MutationGene_Score[key2]= [SL_ReDisease_score[key2] +['%']]
                #print([key2,])
        else:
            #pass
            print([key2, key3])
        # print(ReDisease_MutationGene_Score.values()[0:5])
    return ReDisease_MutationGene_Score

re_module_search(ReDisease_MutationGene, SL_ReDisease_score)
print(len(ReDisease_MutationGene_Score))

with open('./ReDiseaseScore.txt','w') as f:
    f.write('MutationGene\tRepositionDisease\tReDiseaseScore\n')
f.close()

'''
SL_ReDisease_score_withHeader.txt
SL_ReDisease_MutationGene_score.txt
'''
prefix = args.input.split('.')[0]
with open('{}_MutationGene_score.txt'.format(prefix),'w') as g:
    for key in ReDisease_MutationGene_Score.keys():
        for j in range(len(ReDisease_MutationGene_Score[key])):
            print >>g, ('\t').join([str(i) for i in ReDisease_MutationGene_Score[key][j]])
        

os.system('paste {} {} | tr -d "\r" > {}'.format('SL_ReDisease_score_withHeader_header.txt','ReDiseaseScore.txt','add_ReDiseasescore_header.txt'))
# 'SL_ReDisease_MutationGene_score_withHeader.txt'
os.system('sort {} | uniq > {}'.format('{}_MutationGene_score.txt'.format(prefix), '{}_MutationGene_score.temp.txt'.format(prefix)))
os.system('cat {} {} > {}'.format('add_ReDiseasescore_header.txt','{}_MutationGene_score.temp.txt'.format(prefix),'{}_MutationGene_score_withHeader.txt'.format(prefix)))
os.system('rm {}'.format('{}_MutationGene_score.temp.txt'.format(prefix)))

print('{}\t{}\n'.format(time.ctime(), 'end to analyze!'))
```
### 3.主函数

```
from multiprocessing import Pool
import os

os.system('python2.7 divide_ten.py')

def sh(*args):
	os.system('python2.7 search.py -i {}'.format(*args))

pool = Pool(processes=10)
for i in range(1,11):
	infile = '{}_{}.txt'.format('SL_ReDisease_score_withHeader',i)
	pool.apply_async(sh, (infile,))
	#sh(infile)
pool.close()
pool.join()
```
### 4. defaultdict

- 一键多值
```
from collections import defaultdict
# mutation mapping A
multi_mutGene_A = defaultdict(list)
for key_sl in sl_pair:
    mutGene_sl = key_sl.split("+")[0]
    new_key_A = ('\t').join(sl_pair[key_sl])
    for key_mutGene in select_TSG:
        mutGene_TSG = key_mutGene.split("-")[0]
        if mutGene_sl == mutGene_TSG:
            multi_mutGene_A[new_key_A].append(select_TSG[key_mutGene])
        else:
            pass
```
