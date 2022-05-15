<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
# 信安实践第3次题解

## 自己发明一个RSA

- 查看源代码以及根据提示可以发现,该题为一个RSA加密+Paillier加密.查阅资料发现Paillier为加法同态,即$E_2(m1+m2)=E_2(m1)\*E_2(m2)$;而RSA为乘法同态,即$E_1(m1\*m2)=E_1(m1)\*E_2(m2)$

- 因此有 $D_1(D_2(c1\*c2))=D_1(D_2(c1)+D_2(c2))$,希望找到c2,使得$D_2(c2)=0$,从而可以有$m=D_1(D_2(c1\*c2))=D_1(D_2(c1))$

- 对于RSA,E_1(0)=0,因此想找的$c2=E_2(E_1(0))$.

- 通过上述分析,先选择明文0x0,得到c2=$c2=E_2(E_1(0))$,然后将$c1*c2^{-1}\mod{n^2}$作为新密文,解密即得到原来的明文m。