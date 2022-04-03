#Writeup of Design and Practice of Information Security I：Week Ⅱ
### GET

解题思路1：直接在浏览器的URL处进行交互，需要注意的是*/get.php*表示访问的是当前服务器目录下的get.php文件，？告诉接收方，我以GET的方式传了一些变量名，若以GET方式需要传多个变量名，只需要一个？，不同变量之间用&隔开，例如本题为：？what=flag&token=**12345

![image-20220329120821163](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329120821163.png)

![image-20220329121210825](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329121210825.png)

上机实验时有的同学flag不对，是因为传参数时多传了？导致读取的token不对

解题思路2：直接以python的requests库函数执行代码：![image-20220329121531353](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329121531353.png)

### POST

解题思路1：在该页面进行抓包，修改参数后放包

![image-20220329121735689](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329121735689.png)

![image-20220329121857864](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329121857864.png)

![image-20220329121939050](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329121939050.png)

解题思路2：直接修改html元素将name="nebula"修改为name="what"，然后在方框中输入flag点击发送

![image-20220329122149088](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329122149088.png)

这样也可以成功拿到flag

解题思路3：python的requests库函数![image-20220329122345467](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329122345467.png)

### Agent

解题思路1：访问该页面后，得到提示，抓包修改user-agent为：HAHA![image-20220329122538229](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329122538229.png)

![image-20220329122551372](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329122551372.png)

解题思路2：python的requests库函数

![image-20220329123132537](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329123132537.png)

### Cookie

解题思路1：抓包，修改cookie中的login=guest为admin![image-20220329123306172](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329123306172.png)

![image-20220329123346566](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329123346566.png)

![image-20220329123405892](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329123405892.png)

解题思路2：python的requests库![image-20220329123551593](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220329123551593.png)

同样的，可以使用python自带的url解码函数，或者其他地方进行url解码

### Uncompleted

![image-20220403132027387](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403132027387.png)

拿到该题目进入场景如上图所示，根据题目描述，我们应该得到获胜条件时触发的事件，由于这是一道js前端可见的游戏程序，我们可以直接开始代码审计。ctrl+u 阅读源码

![image-20220403133020392](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403133020392.png)

我们点进去这个js文件开始阅读代码

![image-20220403133256257](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403133256257.png)

接下来我们有两种思路，可以直接将score变量赋值，或者输入none变量

![image-20220403133415510](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403133415510.png)

![image-20220403133428437](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403133428437.png)

## 4.3_On_sale

这道题争议比较大，可以好好讲讲~

先说结论：**题目确实没有任何的错误**；一开始的时候由于助教团队不是所有人都仔细阅读了源码，导致出现了判断失误，认为题目有问题，其实后来经过检查发现：刚开始认为的错误并不是题目出错了

首先拿到一道题目的第一步是仔细阅读题目，而不是直接开始做题；这道题需要我们做什么？我们做题的目的是什么？

![image-20220403143939819](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403143939819.png)

我们可以看到，题目的明文描述里说明了：***访问任何页面需要带 token，否则程序会出错***

同时题目还明文告诉我们了必须在8s内提交数据，否则我们就拿不到flag了

打开题目的页面![image-20220403134250965](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403134250965.png)

正确时间段的访问会自动携带token，如果我们访问的时候没有携带token会发生什么情况呢？

![image-20220403134343732](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403134343732.png)

页面会提示我们携带token正确访问

当然这些地方都不是重点，只是回答部分同学的疑惑：为什么我在不正确时间段访问buy.php或者check.php会返回这个页面并提示我没有携带token呢？因为***跳转的时候，并没有为大家携带 token***，需要告诉大家的是，前面的timer.php或者buy.php带不带token并不影响这道题，之所以设定带token的判断是为了提醒大家最后的页面应该带上自己的token！！！（现在看来还不如不提醒大家，提醒大家还会给大家造成 疑惑 sad  ）

倒计时结束后，我们刷新页面会跳转到一个新的页面buy.php下：![image-20220403135323061](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403135323061.png)

这里，如果我们老老实实的填表提交到check.php页面时，会提示大家：没有携带token，那么我们就需要回到该页面查看源

代码，经查看后发现：***这里的跳转的check.php？token=    是并没有为我们携带 token的***，![image-20220403135308327](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403135308327.png)

那么这里为什么没有为大家携带token值呢？

当时的考虑是***携带了token值的情况下会有同学直接点击访问了，而不是抓包或者写脚本，这样的解法与本节课所教授的内容不一致，所以这里故意留了一个坑，并没有为大家携带token，但是又怕大家没有发现原因，所以留了一个未赋值的token变量***

看到这里，如果上课学懂了的同学应该知道为什么自己直接访问的时候会出错，当然他也会知道题目并没有出错。但由于token的交互是无感的，对于不明白携带token或者不注意细节的同学就会认为题目有问题了。CTF并不是给你一个完整的程序运行，我可以给你一个不能直接运行的程序，需要的是你去发现题目中为什么不能运行代码的点。

现在让我们再理一理题目的逻辑流程：

1、倒计时页面，倒计时结束，开始抢购（timer.php）

2、填表页面填完表，需要手动发送token（buy.php）

3、检查验证页面，检查验证成功，则可能会直接返回token（check.php）

那么现在我们就有3种思路可以解出这道题目：

思路一：直接写python脚本![image-20220403140546681](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403140546681.png)

在倒计时块结束时，开始运行![image-20220403140811316](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403140811316.png)

思路二：抓包，并注意附上自己的token值，在倒计时快结束时反复发送

![image-20220403141112075](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403141112075.png)

![image-20220403141211242](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403141211242.png)

思路三：修改html中token变量，在倒计时结束时直接发送

![image-20220403141625988](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403141625988.png)



## 报告撰写的时间为2022.4.3，截止到目前为止，从题目发布到现在并未进行任何的题目更改，所以题目到现在为止是没有变化的，也没有问题的~~

可是为什么有的同学提交时老是会提示flag出错了呢？？？

这里只有两种可能，token携带错误，并没有按照要求携带，要么就是前面的flag带错了![image-20220403141802804](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403141802804.png)

至于为什么提前开抢会提示你抢完了：这是因为这里的**抢完了**，是提示的上一轮的flag已经被抢光了。总之正确操作下来，是不会有任何问题的~~~

### 选做题

这次的选做题难度并不大，首先打开题目页面提示我们有文件可以下载

![image-20220403142123128](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403142123128.png)

我们先下载附件，发现是一个zip文件，想要打开解压却发现解压错误，于是我们查看数据格式

![image-20220403142227442](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403142227442.png)

发现这里的文件头数据错误了，修改文件头数据为 50 4B![image-20220403142310623](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403142310623.png)

之后就可以正常解压文件了，我们打开解压的文件

![image-20220403142347331](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403142347331.png)

发现做了细微的过滤，按照题目的过滤描述，我们抓包修改信息进入该网站

![image-20220403143551381](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403143551381.png)

发送后，查看response，发现了该目录下有一个额外的网站

![image-20220403142807671](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403142807671.png)

我们访问该目录下的该网页，同样地查看其js文件

![image-20220403142909854](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403142909854.png)

发现了这一串的代码十分的可疑，于是经过搜索后发现，这是一段JSfuck

我们复制这一段代码，粘贴到控制台执行，即可获得flag![image-20220403143033678](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403143033678.png)

## 思考题

这两道问题皆为开放性回答的问题并没有明确的标准答案，言之有理即可，但对于GET/POST传数据的方式判断不能出错。

提示：cookie的运用场景很多，例如游客访问某一个网页临时保存访问的信息又或者识别某一用户是合法用户，再或者在进行账号登录时的默认登录状态等等。

本来不打算放GET/POST抓包的情况，但考虑同学们仍存在找不到这些数据传输网站的情况，所以这里列举一些案例

### GET：

我们随便打开一个浏览器，随便搜索

![image-20220403171327569](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403171327569.png)

这里就是一处GET传数据的地方其中的？与&皆是标志，这两个 符号所具体代表的含义可以参考之前我在群里的聊天记录

GET传数据的方式，***？***后面的就是变量名称以及对应的赋值，***&***表示不同变量之间的分隔符号

当然我们这节课是学习了谷歌语法的，更高明的方式是使用谷歌语法 *** inurl: ?=***

![image-20220403171830062](%E4%BF%A1%E6%81%AF%E5%AE%89%E5%85%A8%E4%B8%80%E7%BA%A7%E5%AE%9E%E8%B7%B5%E7%AC%AC%E4%BA%8C%E5%91%A8wp.assets/image-20220403171830062.png)

这样搜索出来的全是GET方式的数据传输

### POST：

post的表单也很多，常见的网站需要输入并提交的数据几乎全是POST，例如登录、搜索框、网页邮箱、论坛留言等等

页面的数据要上传几乎都是使用POST方式。此处不再举例。
