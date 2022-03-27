# 虚假的安全题解_PB20051125关佳旺

## 手动按位异或

现场实验时看到flag只有25位，采用了手动按位异或数字，再查ASCii码表得到flag的“笨方法”。

## 利用数组转字符串更快求解

写实验报告时想到可以通过原加密的代码帮助我们进行破解。找到了python中**根据ASCii码将数组转换成字符串**的语句。例如，要将打印结果`[14, 13, 17, 55, 2, 35, 15, 64, 39, 38, 31, 82, 65, 60, 38, 9, 35, 31, 38, 13, 55, 57, 64, 2, 4]`转换成ASCii码对应字符串，有

```python
1.	arr =[14, 13, 17, 55, 2, 35, 15, 64, 39, 38, 31, 82, 65, 60, 38, 9, 35, 31, 38, 13, 55, 57, 64, 2, 4]  
2.	s = ''.join([chr(i) for i in arr])
```

由此，我们找到key和得到flag都可以更为快捷方便。在寻找key时，将`msg`改为已知打印结果，**将key改为`"flag{"`**，如下

```python
1.	msg = [14, 13, 17, 55, 2, 35, 15, 64, 39, 38, 31, 82, 65, 60, 38, 9, 35, 31, 38, 13, 55, 57, 64, 2, 4]#"flag{xxxxxxxx}"    
2.	msg = ''.join([chr(i) for i in msg]) #转换为根据ASCii码得到的字符串
3.	key = "flag{"    
4.	key = key*5    
5.	secret = []#存放生成的密文的asc码    
6.	for i in range(len(msg)):    
7.	    secret.append(ord(msg[i])^ord(key[i]))#对每一对字符求异或并放入secret列表中 ord函数用于求一个字符的ascii码，chr函数用于求一个ascii数字对应的字符    
8.	secret=''.join([chr(i) for i in secret]) #将原先secret输出的数字转换为根据ASCii码得到的字符串
9.	print(secret) 
```

输出为`hapPyEc!@]y> []oO~AvQU!e`，前五位即为我们想要的key



**对应地，**只要将源代码中key改为`“hapPy“`后再运行，即可直接得到flag