# | Philip Roberts | JSConf EU 心得
<br>
## JavaScript是什麼?
```
一種單執行緒的程式語言 單執行緒的Runtime
```
## JavaScript擁有那些功能?
```
* Call stack        (呼叫堆疊)
* Event Loop        (事件循環)
* Callback queue    (回調佇列)
* WebAPIs           (DOM、ajax、setTimeout)
```
## 小筆記
```
- Stack: 後進先出 (先進後出) First In Last Out (FILO)堆疊。
- JaveScript Runtime 一次只能做一件事。
- 作者將JaveScript Runtime視覺化
[Loupe](http://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)
```
## 心得
```
不可以將Stack堵塞，所以有了 Event Loop(事件循環) 幫我們解決這個問題。

- 非同步呼叫
假設Stack中有ajax，會先將ajax推置WebAPIs 讓Stack可以繼續執行，
Stack執行完畢後，ajax就會被推入佇列然後被Event Loop(事件循環)抓起來，
最後就會推回Stack，就完成了這次的非同步呼叫。

**檢視圖**
![](https://i.imgur.com/CDkxhLn.png)

```

## 感想
![](https://i.imgur.com/f8sk11z.jpg)
