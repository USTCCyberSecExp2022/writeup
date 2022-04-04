# 4.3_On_Salse题解

## **陈昕暄PB20061242**

## 实验思路：
~~利用单身20年手速直接输入~~
由于只有八秒的时间，一般人无法及时输入，因此在控制台使用代码完成更快的填写才能够抢到flag。

## 实验步骤：
1.先进入timer.php界面，在等待倒计时的时候将url编码时的token加在地址栏后面，倒计时完毕后刷新进入抢购页面，打开f12界面，按下快捷键CTRL+SHIFT+C打开选择工具，然后双击网页上“请输入你的姓名：”下面的文本框，或者直接右键单击文本框->检查，在右边元素中会定位该文本框位置，然后我们发现如下信息：  
`<input autocomplete="off" name="name" id="word5">`  
右键单击input，然后复制->复制完整的XPath，复制结果为  
`/html/body/form/center[2]/input`  
接着使用相同方法将剩下五个文本框的完整XPath路径复制，发现只有center后的索引数字不同（应该很正常）这时会有很帅的同学疑问索引为1的是什么，当然是亲测不需要填写即可抢到flag的选择4.3类型的文本框。  

2.手动上传token  
首先在这个网站的源代码中，我们在第48行发现了如下代码：  
`<form id='token' action="./check.php?token=" method="post">`  
可恶的出题人，这样代表着我们在前端输入的token完全起不到作用，因为token根本没有传到后端，~~20年单身狗落泪，手输完全不奏效~~，这时只能手动将自己的token传入，代码为：  
```
document.getElementById('token').action = './check.php?token=（）';
```
（）替换为自己token的url编码形式。  

3.编写代码将信息输入  
首先编写函数：  
```  
    function getElementByXpath(xpath){
    	var element = document.evaluate(xpath,document).iterateNext();
    	return element;
    }  
```
接着将信息输入，代码为：  
```
    getElementByXpath('/html/body/form/center[2]/input').value='*';
    getElementByXpath('/html/body/form/center[3]/input').value='*';
    getElementByXpath('/html/body/form/center[4]/input').value='*';
    getElementByXpath('/html/body/form/center[5]/input').value='*';
    getElementByXpath('/html/body/form/center[6]/input').value='*';
    getElementByXpath('/html/body/form/center[7]/input').value='*';
```
*替换为相应的信息。~~毕竟flag不一样，我的放出来也没用~~

4.tips
将上述三个代码块一起复制，在倒计时时粘贴到控制台中但是不要执行，然后将url编码过的token输入到地址栏里，接着在倒计时结束后，刷新页面出现填写界面，再快速在控制台输入回车执行代码，点击提交订单，即可获得flag。