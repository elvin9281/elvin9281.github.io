# **Iptables** 

{{< hint info >}}
Administration tool for IPv4 packet filtering and NAT
{{< /hint >}}

### 列出 Log 並顯示行數(`--line-numbers`)
```tpl
sudo iptables -vnL --line-numbers
```
---

### [結合 "ACCEPT/DROP" & "LOG"](https://stackoverflow.com/questions/21771684/iptables-log-and-drop-in-one-rule)

- DROP + LOG
```tpl
# Create a Chain to log and drop
sudo iptables -N LOG_DROP
# populate its rules:
sudo iptables -A LOG_DROP -j LOG --log-prefix "INPUT:DROP: " --log-level 6
sudo iptables -A LOG_DROP -j DROP
```