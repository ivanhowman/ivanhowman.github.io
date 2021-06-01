# 5/29 - 5/30 的上課筆記與心得
<br>

## XML 與 JSON 的差別？
```xml=
<entry>
     <name>Peter Ju </name>
     <tel>04-23456789</tel>
     <email href="mailto:peter@hotmail.com"  />
     <comments> graduate student</comments>
<entry>
```

```json=
{
    name: "Peter Ju",
    tel: "04-23456789",
    email: "peter@hotmail.com",
    comments: "graduate student",
}
```

## .gitignore

https://www.toptal.com/developers/gitignore

.gitignore 要放進 git 裡，讓專案裡的其他人同步

例如:
*.txt 表示忽略所有txt檔
!lib.txt  !表示 除了lib.txt
/temp 表示不包括temp文件夾
build/  忽略build裡的文件
doc/.*txt  忽略 doc/text.txt 但不包括 doc/server/text.txt

## npm

"axios": "^0.21.1"

主版本.次版本.patch版 

主版本: 較大的更新，甚至可不相容前面的版本
次版本: 更新要相容前一個版本
patch版: 修bug,...


^: 只會執行不更改最左邊的非零數字的更新
Allows changes that do not modify the left-most non-zero element in the [major, minor, patch] tuple.

   ^1.2.3  < 2.0.0
   ^0.2.3  < 0.3.0 

cowsay@1.1.3
^1.1.3
1.5.0

npm install ==> package-lock.json
npm update ==> 更新版本，並且更新 package-lock.json


~: 只更新 patch
  ~0.13.1
      0.13.2

npm install
npm update

npm view cowsay versions (加上s檢視所有版本)
npm view cowsay version 檢視最新版
npm i cowsay@1.1.3 安裝特定版本

1. 加上 .gitignore -> node_modules
2. npm i cowsay@1.1.3
   移除 node_modules 
   npm i -> 觀察 package-lock 1.1.3
   npm update -> 觀察 package-lock 1.5.0
   npm i cowsay@1.3.0 -> 觀察 package-lock  1.3.0
3. package.json, package-lock.json push git


可執行的工具會放在node_modules/.bin
./node_modules/.bin/cowsay 
用npx cowsay可以快速使用工具類程式
例如：cowsay

npm i -g cowsay 把牛說話安裝在全域(global)

安裝到全域 
npm install -g cowsay 

npx cowsay Hi
```bash=
_____
< Hi >
-----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

npx:
    1. 輕鬆地執行本機的命令 （不管是全域的，或是專案底下的）
    2. 不用安裝命令，就能利用 npx 來執行 （偷偷幫你下載安裝，執行完後刪除）
    
## callback

https://github.com/azole/nodejs-mfee16/blob/master/basic/callback1.js

- 一定要刷完牙 > 吃早餐 > 寫功課
- 只能用 callback

callback hell
![](https://i.imgur.com/cuHysRx.png)

Solution: promise

## Promise

Promise 是一個表示非同步運算的**最終**完成或失敗的*物件*

https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise

狀態:
    pending -> 成功 fulfilled
            -> 失敗 rejected

```javascript=
new Promise(function(resolve, reject) {
    // 會判斷成功或失敗，決定要回哪一個
    // 成功
    resolve("回傳結果");
    // 失敗
    reject("回傳失敗")
})
```

non-blocking
JS -> callback
JS single thread -> WebAPI / Libuv... -> callback
效能好 <-- 非同步

刷完牙 -> 吃早餐

register
1. 查查看 db 這個 email 有沒有註冊過 
 
 Web Server -> DB server
 
 create network connection
 query 網路傳輸
 
2.1 如果有 -> return 你已經註冊過了
2.2 如果沒有 -> 新增這個會員資料

pseudo code
```javascript=
// 非同步
mysql.createConnection({db config}, function() {
    // 連線成功
    mysql.query('SQL 這個 email 在不在', function() {
        // 查詢回來了
        if(有) {
            // TODO
            return 你已註冊
        } else {
            // TODO
            mysql.insert(建立會員資料, function() {
                return 建立成功
            })
        }
    })
})
```

```javascript=
// promise
createConnPromise()
    .then((conn) {
        return conn.queryPromise();
    }).then((result) {
        if(result) {
            return 你已註冊
        } else {
            return conn.insertPromise()
        }
    }).then((result) {
        return 建立成功
    })
```

```php=
// 同步
// php multi-process
$conn = mysql.createConnection({db config});
$result = $conn.query('SQL 這個 email 在不在');
if($result) {
    return 你已註冊
} else {
    $conn.insert(建立會員資料)
    return 建立成功
}
```

https://github.com/azole/nodejs-mfee16/blob/master/crawler/app.js
1. 看一下 fs.readFile
2. 不可以用 fs 的 promise，自己把 fs.readFile 包成 promise
3. 要可以跟 axios 串接，做出 promise chain

// callback
fs.readFile(..., () => {
    // handle read data
    axios....
})

// Promise 
function readFilePromise() {
...
}

readFilePromise().then((result) => {
    return axios
}).then()

## Async / Await

JS -> single thread 
   -> 大量的非同步 
     --> 依賴 callback
     --> callback hell
     ----> Promise (resolve, reject)
       ---> then / catch
       ------> 「希望」可以把程式寫得像同步程式，但他又是非同步、不阻塞

async / await based on Promise

補充：
- EC2(server) + 排程 crontab -> 只要開著就要付錢
    - windows 的工作排程器
- serverless 無伺服器，以 AWS 為例，有一個服務 Lambda + cloudwatch(rule)
  cloudwatch(rule) ==> crontab


---
