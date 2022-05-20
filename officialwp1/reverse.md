<!--
 * @Date: 2022-05-20 14:30:33
 * @LastEditors: Wu Han
 * @LastEditTime: 2022-05-20 14:30:33
 * @FilePath: \writeup\officialwp1\reverse.md
-->
# Reverse 题解

不同同学下载的软件不一样，flag不同，但是基本思路是相同的。

## Hlo Wd

拖入ida，F5：

```cpp
int __cdecl main(int argc, const char **argv, const char **envp)
{
  int v3; // eax
  int i; // [esp+1Ch] [ebp-4h]

  __main();
  printf("Welcome! Here's your flag part1: %s\n", part1);
  if ( argc > 3 && atoi(argv[1]) == 101 && !strcmp(argv[2], "givemeflag") && !strcmp(argv[3], "0f53d2bd") )
  {
    printf("And part2: ");
    for ( i = 0; part2[i]; ++i )
    {
      v3 = i ^ part2[i];
      LOBYTE(v3) = v3 ^ 0xB1;
      putchar(v3);
    }
  }
  else
  {
    printf("Nope. I can't give you flag.");
  }
  putchar(10);
  return 0;
}
```

读代码，part1是直接给的，而part2需要if中的条件判断成立，其中argc和argv都是main的参数，表示运行时的命令行，argc为参数个数，argv为各个参数。在cmd或者powershell中运行：

```shell
C:\Users\???\Downloads>.\Ed40qYr3.exe 101 givemeflag 0f53d2bd
Welcome! Here's your flag part1: flag{we1c0m3_tO_R3V3rs
And part2: e_Englneer1Ng_c16bcdfd}
```

两部分拼接，`flag{we1c0m3_tO_R3V3rse_Englneer1Ng_c16bcdfd}`

## Easy Operation

F5，main中有一堆赋值，类型是`_DWORD[10]`，也就是`int[10]`，再到check函数中，三个参数都是`_BYTE*`类型，并且第二、第三个参数的下标索引到了41，所以回到main，将check函数调用的后两个参数类型（原来是`_DWORD[10]`和一个`__int16`）修改为`unsigned char[42]`：

```cpp
BOOL __cdecl check(_BYTE *a1, _BYTE *a2, _BYTE *a3)
{
  return a2[29] * a1[29] == a3[29]
      && (a2[12] ^ a1[12]) == a3[12]
      && a1[30] - a2[30] == a3[30]
      && a1[23] - a2[23] == a3[23]
      && a1[10] - a2[10] == a3[10]
      && a2[37] * a1[37] == a3[37]
      && a1[41] - a2[41] == a3[41]
      && (a2[4] ^ a1[4]) == a3[4]
      && a2[32] * a1[32] == a3[32]
      && a2[21] + a1[21] == a3[21]
      && a1[8] - a2[8] == a3[8]
      && (a2[3] ^ a1[3]) == a3[3]
      && a2[36] + a1[36] == a3[36]
      && (a2[2] ^ a1[2]) == a3[2]
      && *a1 - *a2 == *a3
      && a2[7] * a1[7] == a3[7]
      && a2[33] * a1[33] == a3[33]
      && (a2[22] ^ a1[22]) == a3[22]
      && a2[31] * a1[31] == a3[31]
      && (a2[17] ^ a1[17]) == a3[17]
      && a1[34] - a2[34] == a3[34]
      && a1[20] - a2[20] == a3[20]
      && a2[14] * a1[14] == a3[14]
      && a2[39] + a1[39] == a3[39]
      && a1[40] - a2[40] == a3[40]
      && a1[6] - a2[6] == a3[6]
      && a2[15] + a1[15] == a3[15]
      && a1[9] - a2[9] == a3[9]
      && (a2[1] ^ a1[1]) == a3[1]
      && a1[25] - a2[25] == a3[25]
      && (a2[16] ^ a1[16]) == a3[16]
      && a2[11] + a1[11] == a3[11]
      && a2[28] * a1[28] == a3[28]
      && a2[13] + a1[13] == a3[13]
      && a1[18] - a2[18] == a3[18]
      && a2[27] + a1[27] == a3[27]
      && a2[5] + a1[5] == a3[5]
      && a2[24] + a1[24] == a3[24]
      && a2[38] + a1[38] == a3[38]
      && (a2[26] ^ a1[26]) == a3[26]
      && a1[35] - a2[35] == a3[35]
      && (a2[19] ^ a1[19]) == a3[19]
      && !a1[42];
}

int __cdecl main(int argc, const char **argv, const char **envp)
{
  unsigned __int8 v4[42]; // [esp+1Ah] [ebp-86h] BYREF
  unsigned __int8 v5[42]; // [esp+44h] [ebp-5Ch] BYREF
  _BYTE v6[50]; // [esp+6Eh] [ebp-32h] BYREF

  __main();
  *(_DWORD *)v5 = 1836998475;
  *(_DWORD *)&v5[4] = 1063145240;
  *(_DWORD *)&v5[8] = 2051176313;
  *(_DWORD *)&v5[12] = 2082043954;
  *(_DWORD *)&v5[16] = 1494290549;
  *(_DWORD *)&v5[20] = 1195124813;
  *(_DWORD *)&v5[24] = 2119703332;
  *(_DWORD *)&v5[28] = 1295676213;
  *(_DWORD *)&v5[32] = 1364618579;
  *(_DWORD *)&v5[36] = 1879591692;
  *(_WORD *)&v5[40] = 1853;
  *(_DWORD *)v4 = 169816859;
  *(_DWORD *)&v4[4] = -754007453;
  *(_DWORD *)&v4[8] = -651969833;
  *(_DWORD *)&v4[12] = -287446915;
  *(_DWORD *)&v4[16] = 1763730497;
  *(_DWORD *)&v4[20] = 675841825;
  *(_DWORD *)&v4[24] = -734177405;
  *(_DWORD *)&v4[28] = 1643722473;
  *(_DWORD *)&v4[32] = -552917043;
  *(_DWORD *)&v4[36] = -1455547023;
  *(_WORD *)&v4[40] = 30454;
  printf("Input your flag: ");
  scanf("%50s", v6);
  if ( check(v6, v5, v4) )
    puts("Correct!");
  else
    puts("Wrong, try again.");
  return 0;
}
```

只用写check的逆，都是很简单的运算，都可以直接逆，除了乘法溢出导致不能直接除，爆破一下就好，不过需要注意处理乘法的溢出。

编写C程序，直接从ida里抄，check改为solve就行，再定义一下相应的类型。

```cpp
#include <stdio.h>

#define _DWORD unsigned int
#define _BYTE unsigned char
#define _WORD unsigned short
 
void solve(_BYTE *a1, _BYTE *a2, _BYTE *a3)
{
	for (int i = 0; i < 256; i++) if ((a2[29] * i & 0xff) == a3[29]) a1[29] = i;
	a1[12] = a2[12] ^ a3[12];
	a1[30] = a3[30] + a2[30];
	a1[23] = a3[23] + a2[23];
	a1[10] = a3[10] + a2[10];
	for (int i = 0; i < 256; i++) if ((a2[37] * i & 0xff) == a3[37]) a1[37] = i;
	a1[41] = a3[41] + a2[41];
	a1[4] = a2[4] ^ a3[4];
	for (int i = 0; i < 256; i++) if ((a2[32] * i & 0xff) == a3[32]) a1[32] = i;
	a1[21] = a3[21] - a2[21];
	a1[8] = a3[8] + a2[8];
	a1[3] = a2[3] ^ a3[3];
	a1[36] = a3[36] - a2[36];
	a1[2] = a2[2] ^ a3[2];
	*a1 = *a3 + *a2;
	for (int i = 0; i < 256; i++) if ((a2[7] * i & 0xff) == a3[7]) a1[7] = i;
	for (int i = 0; i < 256; i++) if ((a2[33] * i & 0xff) == a3[33]) a1[33] = i;
	a1[22] = a2[22] ^ a3[22];
	for (int i = 0; i < 256; i++) if ((a2[31] * i & 0xff) == a3[31]) a1[31] = i;
	a1[17] = a2[17] ^ a3[17];
	a1[34] = a3[34] + a2[34];
	a1[20] = a3[20] + a2[20];
	for (int i = 0; i < 256; i++) if ((a2[14] * i & 0xff) == a3[14]) a1[14] = i;
	a1[39] = a3[39] - a2[39];
	a1[40] = a3[40] + a2[40];
	a1[6] = a3[6] + a2[6];
	a1[15] = a3[15] - a2[15];
	a1[9] = a3[9] + a2[9];
	a1[1] = a2[1] ^ a3[1];
	a1[25] = a3[25] + a2[25];
	a1[16] = a2[16] ^ a3[16];
	a1[11] = a3[11] - a2[11];
	for (int i = 0; i < 256; i++) if ((a2[28] * i & 0xff) == a3[28]) a1[28] = i;
	a1[13] = a3[13] - a2[13];
	a1[18] = a3[18] + a2[18];
	a1[27] = a3[27] - a2[27];
	a1[5] = a3[5] - a2[5];
	a1[24] = a3[24] - a2[24];
	a1[38] = a3[38] - a2[38];
	a1[26] = a2[26] ^ a3[26];
	a1[35] = a3[35] + a2[35];
	a1[19] = a2[19] ^ a3[19];
	a1[42] = 0;
}

int main(int argc, const char **argv, const char **envp)
{
  unsigned __int8 v4[42]; // [esp+1Ah] [ebp-86h] BYREF
  unsigned __int8 v5[42]; // [esp+44h] [ebp-5Ch] BYREF
  _BYTE v6[50]; // [esp+6Eh] [ebp-32h] BYREF

  *(_DWORD *)v5 = 1836998475;
  *(_DWORD *)&v5[4] = 1063145240;
  *(_DWORD *)&v5[8] = 2051176313;
  *(_DWORD *)&v5[12] = 2082043954;
  *(_DWORD *)&v5[16] = 1494290549;
  *(_DWORD *)&v5[20] = 1195124813;
  *(_DWORD *)&v5[24] = 2119703332;
  *(_DWORD *)&v5[28] = 1295676213;
  *(_DWORD *)&v5[32] = 1364618579;
  *(_DWORD *)&v5[36] = 1879591692;
  *(_WORD *)&v5[40] = 1853;
  *(_DWORD *)v4 = 169816859;
  *(_DWORD *)&v4[4] = -754007453;
  *(_DWORD *)&v4[8] = -651969833;
  *(_DWORD *)&v4[12] = -287446915;
  *(_DWORD *)&v4[16] = 1763730497;
  *(_DWORD *)&v4[20] = 675841825;
  *(_DWORD *)&v4[24] = -734177405;
  *(_DWORD *)&v4[28] = 1643722473;
  *(_DWORD *)&v4[32] = -552917043;
  *(_DWORD *)&v4[36] = -1455547023;
  *(_WORD *)&v4[40] = 30454;
  /*
  printf("Input your flag: ");
  scanf("%50s", v6);
  if ( check(v6, v5, v4) )
    puts("Correct!");
  else
    puts("Wrong, try again.");
  /**/
  solve(v6, v5, v4);
  puts((char*) v6);
  return 0;
}
```

要有耐心，中间一步错了就全错了。运行得到的字符串先用下载的程序运行试试，程序提示正确才能在答题平台上提交通过。

有人爆破答题平台（我不说是谁），但是平台上两次提交flag有等待时间，还有可能爆破到别人的flag，为什么不用给你的程序爆破呢，不需要等待也没有风险。

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b804.png)

当然，既然都提示错误了肯定是哪儿抄错了或算错了，为什么不检查一下自己的程序呢？

补充（题目考点）：

 - 耐心
 - main函数中`unsigned char[42]`变量类型的修改，题板上给了提示，不止`_DWORD[10]`的40字节，长度是更大的。至于`*(_DWORD *)&v5[4] = 1063145240;`这样的赋值什么意思，参见题板`关于 C 语言的一些表达式：`这里的提示，有不懂的请在群里问；为什么不能将前面的`*(_DWORD *)&`去掉，因为去掉后后面的数字将被截断到低8位，只对一个字节赋值，这里是要对连续四个字节赋值，当然不能去掉
 - 乘法的写逆（其实乘法是在模256的有限域乘，生成题目时乘法的a2一定是奇数，这样可以保证a1只有唯一解）

## RC4

这道题目上课时已经讲了，在两个RC4相关的函数里介绍ida的基本使用，不过这两个函数源码已经给了，其实只需要看main函数，提取出两个最重要的数组即可。简单分析一下RC4的加密方式就可以知道，它是流密码，加解密都是异或一段字节，跟加解密的数据没关系，所以加密和解密是相同的。

用提供的RC4代码写C代码：

```cpp
#include <stdio.h>

// RC4
void RC4Init(unsigned char* RC4Box, unsigned char* key, unsigned int keylen) {
	for (int i = 0; i < 256; i++) {
		RC4Box[i] = i;
	}
	for (int i = 0, j = 0; i < 256; i++) {
		j = (j + RC4Box[i] + key[i % keylen]) & 0xff;
		int tmp = RC4Box[i];
		RC4Box[i] = RC4Box[j];
		RC4Box[j] = tmp;
	}
}

void RC4Crypt(unsigned char* RC4Box, char* data, unsigned int len) {
	for (int i = 0, j = 0, k = 0; k < len; k++) {
		i = (i + 1) & 0xff;
		j = (j + RC4Box[i]) & 0xff;
		int tmp = RC4Box[i];
		RC4Box[i] = RC4Box[j];
		RC4Box[j] = tmp;
		data[k] ^= RC4Box[(RC4Box[i] + RC4Box[j]) & 0xff];
	}
}

int main() {
	unsigned char RC4Box[256];
	unsigned char key[] = {
		0x12, 0x4E, 0x3F, 0xA6, 0x69, 0x62, 0x0B, 0xFF,
		0xEA, 0xD0, 0x62, 0x61, 0xE6, 0xE5, 0x0B, 0xCE
	};
	char data[] = {
		0xC5, 0xD2, 0xD7, 0x0F, 0x1D, 0x62, 0x52, 0x6E, 0x37, 0x6B, 
		0x3D, 0x80, 0xEE, 0x8C, 0x60, 0xDD, 0xF1, 0x6E, 0xD8, 0x4B, 
		0x70, 0x88, 0x50, 0x37, 0xCC, 0x2B, 0xF6, 0xF1, 0xFA, 0xB0, 
		0x31, 0x10, 0xC2, 0xBD, 0xF5, 0xCF, 0x17, 0x06, 0xB1, 0xA8, 
		0x65, 0xD0, 0x03, 0x00
	};

	RC4Init(RC4Box, key, 16);
	RC4Crypt(RC4Box, data, 43);
	puts(data);
	return 0;
}
```

其实加解密的长度只有43字节，最后的0是用来判断flag输入的结尾。不过解密时长度用44也没关系，可以看到完整flag。

```shell
C:\Users\???\Downloads>.\Hne1SNiv.exe
Input your flag: flag{S+4nDard_sTr3aM_c1pHeR_rrrc4_c196dda0}
Correct!
```

## Have a Cup of TEA

上一道题是标准RC4加解密，而且给了源码，非常简单，这道题使用了修改的tea（Tiny Encryption Algorithm）加密，需要自己写tea_encrypt函数的逆。

ida里查看，tea_encrypt函数直接恢复出来，并且观察到返回值是没用的，将返回值类型修改为空以精简代码结构：

```cpp
void __cdecl tea_encrypt(unsigned int *a1, _DWORD *a2)
{
  int i; // [esp+10h] [ebp-10h]
  int v3; // [esp+14h] [ebp-Ch]
  unsigned int v4; // [esp+18h] [ebp-8h]
  unsigned int v5; // [esp+1Ch] [ebp-4h]

  v5 = *a1;
  v4 = a1[1];
  v3 = 290053651;
  for ( i = 0; i <= 31; ++i )
  {
    v3 -= 1055605469;
    v5 += (v4 + v3) ^ (16 * v4 + *a2) ^ ((v4 >> 5) + a2[1]);
    v4 += (v5 + v3) ^ (16 * v5 + a2[2]) ^ ((v5 >> 5) + a2[3]);
  }
  *a1 = v5;
  a1[1] = v4;
}
```

2个unsigned int值，做32轮运算，每轮运算中的两个关键式子都是用其中一个usngiend int值更新另一个unsigned int值，也很容易写逆，不过要注意v3的值变化。

写逆如下：

```cpp
void tea_decrypt(unsigned int *a1, _DWORD *a2)
{
  int i; // [esp+10h] [ebp-10h]
  int v3; // [esp+14h] [ebp-Ch]
  unsigned int v4; // [esp+18h] [ebp-8h]
  unsigned int v5; // [esp+1Ch] [ebp-4h]

  v5 = *a1;
  v4 = a1[1];
  v3 = 290053651 - 1055605469 * 32;
  for ( i = 31; i >= 0; --i )
  {
    v4 -= (v5 + v3) ^ (16 * v5 + a2[2]) ^ ((v5 >> 5) + a2[3]);
    v5 -= (v4 + v3) ^ (16 * v4 + *a2) ^ ((v4 >> 5) + a2[1]);
    v3 += 1055605469;
  }
  *a1 = v5;
  a1[1] = v4;
}
```

由于tea_encrypt每次只加密8字节（两个unsigned int），所以main中用循环加密`tea_encrypt((unsigned int *)&Buf1[8 * i], &key);`，这样保证了输入都会被加密。

最后还是一样，提取出关键值，调用解密函数，输出：

```cpp
int main() {
	unsigned int key[4] = { 782911279, -700685164, -1610772519, -1981734078 };
	char data[] = {
		0xEA, 0xE4, 0xD8, 0x76, 0x4B, 0xA3, 0x49, 0x63, 0xC2, 0x97, 
		0x64, 0xD6, 0xD4, 0xF1, 0x60, 0x8A, 0x1C, 0x4F, 0xDA, 0x2F, 
		0x2F, 0x10, 0xBC, 0xA4, 0xE7, 0x82, 0x82, 0x35, 0x8E, 0xAA, 
		0x9C, 0xA2, 0xCB, 0x29, 0x7D, 0x98, 0x1A, 0x7C, 0x63, 0xD8, 
		0x64, 0x9A, 0xAA, 0xDF, 0x50, 0x7F, 0x83, 0x89
	};
	for (int i = 0; i <= 5; i++)
		tea_decrypt((unsigned int*) &data[8 * i], key);
	puts(data);
	return 0;
}
```

运行程序：

```shell
C:\Users\???\Downloads>.\yKGFyOrD.exe
Input your flag: flag{0h_th1s_cUp_0F_t34_1S_p01sOn!!_29e0cc9e}
Correct!
```

## Treasure Hunter

这是几道题里最有意思的一道题目吧。

F5，进入game函数，关键代码：

```cpp
  x = 3;
  y = 4;
  if ( maze[43] != 64 || maze[99] != 84 )
  {
    puts("Too bad, something unexpected.");
    puts("Please report this to your TA.");
    exit(-1);
  }
LABEL_22:
  while ( maze[10 * y + x] != 'T' )
  {
    switch ( (unsigned __int8)getchar() )
    {
      case 'a':
        if ( !x )
          lost();
        --x;
        v0 = step++;
        path[v0] = 97;
        goto LABEL_18;
      case 'd':
        if ( x == 9 )
          lost();
        ++x;
        v1 = step++;
        path[v1] = 100;
        goto LABEL_18;
      case 'q':
        puts("Quit.");
        exit(0);
      case 's':
        if ( y == 9 )
          lost();
        ++y;
        v3 = step++;
        path[v3] = 115;
        goto LABEL_18;
      case 'w':
        if ( !y )
          lost();
        --y;
        v2 = step++;
        path[v2] = 119;
LABEL_18:
        if ( maze[10 * y + x] == '#' )
        {
          puts("You tried to hit the wall with your head.");
          die();
        }
        if ( step > 49 )
        {
          puts("You run out of food.");
          die();
        }
        return result;
      default:
        goto LABEL_22;
    }
  }
```

也就是走迷宫，大小10x10，初始位置为(4, 3)，循环读取输入，输入了wasd后移动一步，直到死亡或者到达maze中的`T`时胜利。那么maze迷宫地图是关键，双击来到maze，有一个灰色的类型标识`char[99]`，但是并没有应用，需要手动右键array设置

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b805.png)

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b806.png)

再用shift+e导出，并且注意到选择string literal导出是直观的字符串：

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b807.png)

复制到文本文件，每10个字符换行一次（最好使用等宽字体，并且注意换行时是否有自动缩进将原字符串修改了）

（每个人的地图不一样）

```cpp
######    
#   #  ## 
# #   ##  
   ### # #
 # @#  # #
## #  #  #
 # # ## ##
 # #      
 # # #### 
   #    #
```

其中`@`是起始位置，没有`T`，但是在ida里可以看到maze后一个字节就是`T`，所以maze其实大小是100（10x10），最右下角的是终点，坐标为(9, 9)。看着图走迷宫即可。

```shell
C:\Users\???\Downloads>.\scBFIHCx.exe
Tired of reversing? Let's have a game and try to find the path to the treasure chest!
awawwddsddwdwdddssasssassddss
Congrats! You found the treasure chest!
Opening...
You found a flag!
flag{fUn_m4z3_1s_rE4lIy_Re1ax1nG_06d8cb89}
```

补充：

地图也就是一个字符串，IDA VIEW中在_maze处按`a`，确定，转成可视字符串，可以直接得到地图：

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b808.png)


## Stripped

ida进入时无法识别到main函数，停在start，直接F5是看不到有用信息的。

给了提示，网上搜索`ida 交叉引用`，很容易找到要用代码或者数据的交叉引用。在ida里，打开交叉引用列表按`x`。但是首先要有一个代码中被引用的数据，运行时会输出`Where am I?`，是一个字符串，网上搜索`ida 查找字符串`，得到shift+f12打开字符串窗口，找到输出的这句话

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b809.png)

双击来到IDA View中的位置，再`x`找到使用此字符串的位置：

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b80a.png)

双击进入该处，可以F5了：

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b80b.png)

有一条提示，找这个函数的引用，在函数名sub_40160C处按`x`：

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b80c.png)

继续进入，就来到主函数了：

```cpp
int sub_401A48()
{
  char v1[4]; // [esp+10h] [ebp-C4h] BYREF
  char v2[124]; // [esp+14h] [ebp-C0h] BYREF
  char v3[64]; // [esp+90h] [ebp-44h] BYREF

  sub_401B70();
  *(_DWORD *)v1 = 0;
  memset(v2, 0, sizeof(v2));
  sub_40160C(v3);
  sub_401681(v3);
  sub_4019BD(v3, (int)v1);
  if ( sub_401A25(v1) )
    sub_40169D();
  else
    sub_4016B2();
  return 0;
}
```

下一个调用的函数是sub_401681，进入查看：

![](https://md.nb.jonbgua.com/uploads/e84ced599483a2eecc4b6b80d.png)

这里可以合理猜测这是调用scanf函数输入。如果继续进入这个函数，里面很复杂，很难看出来在做什么。不用跟进去，看到`%s`这种格式化的要么是输入scanf要么是输出printf。

再main的下一个函数：

```cpp
int __cdecl sub_4019BD(char *Str, int a2)
{
  signed int v3; // [esp+18h] [ebp-10h]
  signed int i; // [esp+1Ch] [ebp-Ch]

  v3 = strlen(Str);
  for ( i = 0; i < v3; ++i )
    Str[i] ^= i - 12;
  return sub_4016C7(Str, v3, a2);
}
```

先做异或，再传给后面的函数。后面的函数进入后比较复杂，但是看到`"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"`这个字符串，猜测是做base64（这是标准base64的编码表，这里是合理猜测，先按照这种思路解题，如果能解出flag说明猜测正确，否则还需要继续分析此函数）。

再main的下一个函数：

```cpp
BOOL __cdecl sub_401A25(char *Str1)
{
  return strcmp(Str1, "kpmXkIOflpXIzLeGXzBdZTRwaENXb19lZyZnP35Of3p1e0lyL3t/LCopf2I=") == 0;
}
```

做字符串比较。

为了减少工作量，不用自己编写base64编解码，这里使用python求解。

```python
from base64 import b64decode

dst = "kpmXkIOflpXIzLeGXzBdZTRwaENXb19lZyZnP35Of3p1e0lyL3t/LCopf2I="

decoded = b64decode(dst.encode())

decrypted = ''

for i in range(len(decoded)):
	decrypted += chr(decoded[i] ^ (i - 12) & 0xff)

print(decrypted)
```

运行即可得到flag。

## Final Trial

题目比较困难，也基本没人做，萌新懒得写题解了。有兴趣学习这道题目的同学可随时找萌新交流。

