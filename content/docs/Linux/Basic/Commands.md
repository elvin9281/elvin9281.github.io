# Commands 

紀錄常用的指令

## `tar` for `.tar.gz`

- 壓縮：
```tpl
tar zcvf FileName.tar.gz DirName
```
- 解壓縮：
```tpl
tar zxvf FileName.tar.gz
```

---

## screen

- 開啟一個互動式的 Shell
```tpl
screen
```

- Detach 互動式的 Shell
```tpl
Crtl + A + d
```

- 列所有 互動式的 Shell(會列出 Session ID)
```tpl
screen -ls
```
![](https://i.imgur.com/Q3XqcjY.png)

- Attach 到互動式的 Shell 
```tpl
screen -r
screen -r + SessionID
```

- 結束 互動式的 Shell 
```tpl
exit
```

---

## uname - Get Kernel Version

```tpl
uname -a
```
![](https://i.imgur.com/QGyao5Q.png)

- 4 : Kernel version
- 19 : Major revision
- 0 : Minor revision
- 17 : Patch level or number
