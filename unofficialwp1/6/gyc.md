<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
# Solution by Stēlla Caerulea

## RSA Rarity Oracle

可以直接获知的信息有模数 $d$ (`modular`)、大整数 $n=pq$、密文 $c=m^e$。首先确定交互次数一个大概的界。每次交互给出一个满足 $0\leq k\leq d$ 的整数 $k$，理论上从中可获取的平均信息量是 $\log d$；而确定一个小于 $n$ 的整数需要的信息量是 $\log n$。需要的最小交互次数是 $\log n/\log d$，再由于交互的原子性 (?) 向上取整。之后会看到这个界也是可达的。

若在第 $l$ 次交互发送 $C\cdot d^{le}\equiv(d^lm)^e$，之后能从返回值 $r_l$ 构造 $k_l$，即模数 $d$ 进制下，$f/n$ 的第 $l$ 位小数，这样就能获取一系列 $f/n$ 的渐近值，当其精度高于 $1/n$ 时，即可将近似的 $f/n$ 唯一映射到整数 $f$。

从 $r_l$ 构造 $k_l$ 是可行的。$d^lm\not\equiv 0$，可以确定 $d^lm\in(k_ln,(k_l+1)n)$。$r_l\equiv d^lm-k_ln\equiv-k_ln\mod d$，注意到 $d$ 是一个小整数，有 $d<300<\min\{p,q\}$，$d$ 与 $n$ 没有公因子，穷举 $k_l$ 可以确定 $k_l$ 和 $s_l$ 的一一对应关系。用数组的性质可以方便地构造小整数上的反函数。

另需注意的是 $f/n$ 的存储方式。在这里任何种类的浮点数都没有足够的精度，需要用如类似分数的手段存储，这里分母固定为 $d$ 的幂次。

借助 [Pwntools](https://github.com/Gallopsled/pwntools) 编写题解代码。代码如下：

```py
import math
from pwn import remote
from Crypto.Util.number import long_to_bytes

class colors:
#    PURPLE = '\033[95m'
   CYAN = '\033[96m'
#    DARKCYAN = '\033[36m'
   BLUE = '\033[94m'
#    GREEN = '\033[92m'
#    YELLOW = '\033[93m'
#    RED = '\033[91m'
   BOLD = '\033[1m'
#    UNDERLINE = '\033[4m'
   END = '\033[0m'

cyanplus = '[' + colors.CYAN + colors.BOLD + '+' + colors.END + ']'
bluesubsc = '[' + colors.BLUE + colors.BOLD + '-' + colors.END + ']'

token_s = input(bluesubsc + ' ' + 'Your token: ')

e = 0x10001
token = int(token_s.split(":")[0])
modular = token + 2

p = remote('ctf.nbs.jonbgua.com', 32103)
p.recvuntil(b"Please input your token:")
p.sendline(token_s.encode())
p.recvuntil(b"cipher is ")
c = int(p.recvuntil(b"\n")[:-1])
p.recvuntil(b"n is ")
n = int(p.recvuntil(b"\n")[:-1])

#  ret[returnValue] == k
x = (-n) % modular
ret = [0] * modular
for i in range(modular):
    ret[x * i % modular] = i

times = math.ceil(math.log(n, modular))
times_half = math.ceil(math.log(n, modular) / 2)

p.recvuntil(b"The task you choose:")
p.sendline(b'0')
p.sendline(str(ret[1]).encode())
p.sendline(str(ret[2]).encode())
print(cyanplus, p.recvuntil(b"\n")[:-1].decode()) # flag 1

p.recvuntil(b"The task you choose:")
p.sendline(b'1')
p.recvuntil(b"input your times:")
p.sendline(str(times).encode())
print(cyanplus, p.recvuntil(b"\n")[:-1].decode()) # flag 2

p.recvuntil(b"The task you choose:")
p.sendline(b'2')
c1 = pow(modular, e, n) * c % n
p.recvuntil(b"input c1:")
p.sendline(str(c1).encode())
c2 = pow(pow(modular, e, n), 2, n) * c % n
p.recvuntil(b"input c2:")
p.sendline(str(c2).encode())
r1 = int(p.recvuntil(b"\n")[:-1])
r2 = int(p.recvuntil(b"\n")[:-1])
print(cyanplus, p.recvuntil(b"\n")[:-1].decode()) # flag 3

mem = 0

for i in range(times_half):
    p.recvuntil(b"The task you choose:")
    p.sendline(b'2')
    c1 = pow(pow(modular, e, n), 2 * i + 1, n) * c % n
    p.recvuntil(b"input c1:")
    p.sendline(str(c1).encode())
    c2 = pow(pow(modular, e, n), 2 * i + 2, n) * c % n
    p.recvuntil(b"input c2:")
    p.sendline(str(c2).encode())
    r1 = int(p.recvuntil(b"\n")[:-1])
    r2 = int(p.recvuntil(b"\n")[:-1])
    mem = mem * modular + ret[r1]
    mem = mem * modular + ret[r2]
    # print('i =', i) # just wait for a while

ss = n * mem // pow(modular * modular, times_half)
bts = long_to_bytes(ss)
print(cyanplus, bts[:-201].decode()) # flag 4

```
