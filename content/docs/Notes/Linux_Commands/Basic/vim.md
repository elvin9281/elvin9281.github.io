## vim - Editor

## 一般指令模式 (command mode)

- <font color=blue>選取</font>
  - 單字：v
  - 整行：shift+v

- <font color=blue>複製</font>
選取後，按 y

- <font color=blue>貼上</font>
將剛剛複製的內容在想貼上的地方，按 p

- <font color=blue>刪除</font>
選取後，按 d

- <font color=blue>復原上一步</font>
按 u

- <font color=blue>重做上一步</font>
Ctrl + r

- <font color=blue>搜尋</font>
按 / ，若想繼續搜尋，按 n

- <font color=blue>移至檔尾（最後一行的第一個非空白字元處）</font>
按 G

- <font color=blue>移至檔首（第一行之第一個非空白字元處）</font>
按 gg

- <font color=blue>移至當行行首</font>
按 ```0```

- <font color=blue>移至當行行尾</font>
按 ```$```

- <font color=blue>前往特定行數</font>
: + 行數

- <font color=blue>前往成對的括號 ([{}])、/* */</font>
按 %

- <font color=blue>PageUp 翻頁</font>
Ctrl+b

- <font color=blue>PageDown 翻頁</font>
Ctrl+f 

- <font color=blue>多行註解</font>
在想加註解的最頂行 ctrl + v ，選到最底行
shift + i 加入要註解的字 ( e.g. // 或 #
然後按 esc 就會自動把剛剛選取的地方都加入

- <font color=blue>多行解註解</font>
到最頂行ctrl + v
把所有要刪的字用灰色覆蓋，像如果只有 # 就不用向右移
然後按d

### 「一般指令模式」切換到「編輯模式」

- <font color=blue>從目前游標所在處開始編輯</font>
按 i

- <font color=blue>在目前游標所在的下一列處插入新的一列</font>
按 o

### 「編輯模式」切換到「一般指令模式」

- <font color=blue>退出vim編輯模式</font>
Ctrl+Z 或 按 ESC

### 「一般指令模式」切換到「指令列模式」

- <font color=blue>離開vim</font>
輸入 :q

- <font color=blue>儲存檔案並離開</font>
輸入 :wq

- <font color=blue>強制儲存檔案並離開</font>
輸入 :wq!

- <font color=blue>強制離開不儲存檔案</font>
輸入 :q!

