# Redirection (<, >, >>)

## [在 ShellScript 內 使用 ```exec ``` 做 「永久性 Redirection」](https://tw511.com/a/01/1931.html)

- 在 XXX.sh 中，所有`stdout` & `stderr` 都會導到 `/path/logfile`
- 使用 exec 命令可以永久性地重定向，後續命令的輸入輸出方向也被確定了，直到再次遇到 exec 命令才會改變重定向的方向；換句話說，一次重定向，永久有效。


```tpl
XXX.sh
#!/bin/bash -x
exec &>> /path/logfile
```

---

## Redirection 基本概念

Shell 提供「可以取得任一執行中的程式，再更改 `取得輸入` 或 `產生輸出` 的方式，而 `不必修改程式本身`」

### 執行handywork，輸入是名為「data.in」的檔案，輸出到名為「result.out」的檔案

```tpl
handywork < data.in > result.out
```

### 把執行handywork的錯誤導到名為 err.msgs 的檔案

檔案描述符：stdin：0, stdout：1, stderr：2 

```tpl
handywork < data.in > result.out 2> err.msgs
```

## 把「錯誤訊息(stderr：2)」和「正常輸出(stdout：1)」導到名為 result.out 的檔案」(如果沒有1, 錯誤訊息就只會被寫進 `一個名為1的檔案裡` )

```tpl
handywork < data.in > result.out 2>&1
```
or

```tpl
handywork < data.in &> result.out
```

## Bash - 解釋「echo "hey" >&2」

![](https://i.imgur.com/HE4WvxT.png)

Ref: https://stackoverflow.com/questions/23489934/echo-2-some-text-what-does-it-mean-in-shell-scripting

## Bash - 解釋 XXX > /dev/nell > 2>&1

- 將左邊程式的所有標準輸出 stdout, 及標準錯誤輸出 stderr 導向到 /dev/null, 即左邊的程式只會執行, 而不會輸出任何程式執行的結果

- &: 設定使用 fd 代號, 如果 “> dev/null 2>&1” 沒有加上 “&”, 會視後面的 “1” 為檔案名稱, 而不是 fd.(1: fd 的標準輸出 stdout.)

- Ref:[“> /dev/null 2>&1” 的意思](https://www.opencli.com/linux/dev-null-2-and-1-meanning)

## Bash - 如何只導standard error到 /dev/null ?

```tpl
command 2>/dev/null
```

(https://askubuntu.com/questions/68175/how-to-create-script-with-auto-complete)

![](https://i.imgur.com/HaFYFVj.png)
