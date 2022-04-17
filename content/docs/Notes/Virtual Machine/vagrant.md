# **Vagrant** 

{{< hint info >}}
虛擬機器(virtual machine) 管理工具
{{< /hint >}}

### 啟動 VM
> ex: 新起一個 Debain 10 VM
```tpl
vagrant init generic/debian10
vagrant up
```
---

### [Vagrant Export & Import](https://www.jianshu.com/p/05197ab5b767)
> 打包 & 匯入 Box

- 確認目前在 Virtual Box 內的 Box 有哪些
```tpl
vboxmanage list vms
```

- 用 `vagrant package` 打包成 box
```tpl
nohup vagrant package --base $(vboxmanage list vms | grep "vagrant" | awk '{print $1}' | tr -d '"') –-output output.box
```

- 載入 box
```tpl
vagrant box add -name output output.box
```

- 以「output.box 為 base」初始化
```tpl
vagrant init output
```

- 啟動 VM
```tpl
vagrant up
```
---

### [Vagrant Scp](https://github.com/invernizzi/vagrant-scp)
> 傳檔到VM/從VM 拿檔

- 安裝 `vagrant-scp`
```tpl
vagrant plugin install vagrant-scp
```

- Transfer file from **Host OS 的 abc.txt** 到 **Guest OS 的 home 路徑下的 destFile.txt**
```tpl
vagrant scp abc.txt :destFile.txt
```

- Transfer file from **Gest OS 的 abc.txt** 到 **Host OS 的 當下路徑下的 destFile.txt**
```tpl
vagrant scp :abc.txt destFile.txt
```