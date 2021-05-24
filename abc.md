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
 Stack: 後進先出 (先進後出) First In Last Out (FILO)堆疊
 JaveScript Runtime 一次只能做一件事
```
## 心得
```
不可以將Stack堵塞，所以有了 Event Loop(事件循環) 幫我們解決這個問題。

**非同步呼叫**
假設Stack中有ajax，會先將ajax推置WebAPIs 讓Stack可以繼續執行，
等到ajax執行完畢就會被推入佇列然後被Event Loop(事件循環)抓起來，
最後就會推回Stack了。
```
**檢視圖**
![](https://i.imgur.com/CDkxhLn.png)



![](https://i.imgur.com/f8sk11z.jpg)
