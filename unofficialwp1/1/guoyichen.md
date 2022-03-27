# Solution by Stēlla Caerulea ('21 Mar 21st)

> 郭奕辰 PB20151789

> 67:MEQCIDJqMca06BxL3buPL1Po3t5aAZ0F2500P+JoW8bTkxfwAiBfJS6WlodmeGIRMdciHecGqWdtchRRsJF0FQsfnMzpkg==

话说题解是不是不用带 token 来着？要是的话我下次就不带了。

---

## 进制十六——参上

~~股沟~~谷歌搜索 `picture to text`，找到这个网站 [Image to Text Converter](https://www.prepostseo.com/image-to-text)，截取 `0x70-0xA0` 行上传得到
> 20 61 20 62 79 74 65 2 20 66 60 61 67 73 59 30 55 5F 53 48 30 55 31 44 5F 6B 6E 30 77 5F 48 30 57 5F 74 30 5F 43 30 6E 76 33 72 74 5F 48 45 58 5F 74 6F 5F 54 65 78 54 70 20 46 6F 72 20 65 78

然后搜索 `hex to text`，找到这个网站 [Convert hexadecimal to text](http://www.unit-conversion.info/texttools/hexadecimal/)。将 `2` 补全为 `2E` 后得到
> a byte. f`agsY0U_SH0U1D_kn0w_H0W_t0_C0nv3rt_HEX_to_TexTp For ex

有少许错误，不过对于解题已经足够。

所以弗拉格是：`flag{Y0U_SH0U1D_kn0w_H0W_t0_C0nv3rt_HEX_to_TexT}`

## 2048

~~玩 2048 之后得到弗拉格。2048 教程：https://www.youtube.com/watch?v=kQhkkqjGkFA 。~~

根据讲义按部就班地操作。检查网页源代码，在 `html_actuator.js` 中 ~~114514(難視)~~ `145` 行起发现如下函数。
```javascript
HTMLActuator.prototype.message = function (won) {
  var type    = won ? "game-won" : "game-over";
  var message = won ? "FLXG 大成功！" : "FLXG 永不放弃！";

  var url;
  if (won) {
    url = "/getflxg?my_favorite_fruit=" + ('b'+'a'+ +'a'+'a').toLowerCase();
  } else {
    url = "/getflxg?my_favorite_fruit=";
  }

  let request = new XMLHttpRequest();
  request.open('GET', url);
  request.responseType = 'text';

  request.onload = function() {
    document.getElementById("game-message-extra").innerHTML = request.response;
  };

  request.send();

  this.messageContainer.classList.add(type);
  this.messageContainer.getElementsByTagName("p")[0].textContent = message;

  this.clearContainer(this.sharingContainer);
  this.sharingContainer.appendChild(this.scoreTweetButton());
  twttr.widgets.load();
};

```

这下子都好搞了。在控制台如下一通操作。
```javascript
>	let request = new XMLHttpRequest();
	request.open('GET', "/getflxg?my_favorite_fruit=" + ('b'+'a'+ +'a'+'a').toLowerCase());
	request.responseType = 'text';

	request.send();
<	undefined
> console.log(request.response);
< 'flxg{8G6so5g-FLXG-ac21c536de}'
```
~~就地现学 JS 了属于是~~

~~网安开了量子物理，废理兴工失败了，西区人落泪~~

## 虚假的安全

注意到按位异或是一可逆操作，如有 `p ^ k == c` 则必有 `c ^ k == p`。因为本人只学过 C 和 C艹，所以用 C艹 暴力解决。以下是代码。
```c++
/** 3.cpp **/
#include <string>
#include <iostream>

using namespace std;

int main(void)
{
	char cypher[] = {14, 13, 17, 55, 2, 35, 15, 64, 39, 38, 31, 82, 65, 60, 38, 9, 35, 31, 38, 13, 55, 57, 64, 2, 4};
	char plain[25] = "flag{";
	char key[5];

	for (int i = 0; i < 5; i++)
	{
		key[i] = cypher[i] ^ plain[i];
	}
	
	// cout << (string)key << endl;

	for (int i = 0; i < 25; i++)
	{
		plain[i] = cypher[i] ^ key[i%5];
	}

	cout << string(plain, 0, 25) << endl;	

	return 0;
}

```
得到的弗拉格：`flag{Kn0w_w31l_aBovt_X0R}`

## 你的名字

~~二次元 呕呕 什么 我也是二次元啊 那没事了~~

找到提交相关段落：
```javascript
$.ajax({
            url: "",//发送一个到当前网址的post请求
            type: "POST",
            data: { "name": name, "token": token },
            dataType: "text",
            success: function (data) {
              $("#msg").html(data);
            }
          });

```
随机选择一位幸运助教扔进控制台：
```javascript
$.ajax({
            url: "",//发送一个到当前网址的post请求
            type: "POST",
            data: { "name": "张广为", "token": "someToken" },
            dataType: "text",
            success: function (data) {
              $("#msg").html(data);
            }
          });

```
直接得到弗拉格：
```javascript
{readyState: 1, getResponseHeader: ƒ, getAllResponseHeaders: ƒ, setRequestHeader: ƒ, overrideMimeType: ƒ, …}abort: ƒ (e)always: ƒ ()catch: ƒ (e)done: ƒ ()fail: ƒ ()length: 0name: "add"prototype: {constructor: ƒ}arguments: (...)caller: (...)[[FunctionLocation]]: jquery.min.js:2[[Prototype]]: ƒ ()[[Scopes]]: Scopes[3]getAllResponseHeaders: ƒ ()getResponseHeader: ƒ (e)overrideMimeType: ƒ (e)pipe: ƒ ()progress: ƒ ()promise: ƒ (e)readyState: 4responseText: "flag{TA_1s_satlSfIed_something}"setRequestHeader: ƒ (e,t)state: ƒ ()status: 200statusCode: ƒ (e)statusText: "OK"then: ƒ (t,n,r)[[Prototype]]: Object

```

就酱，下次见 wwww
