# SSH Tunnel 
> SSH Tunnel for Local/Remote Port Forwarding 

## Ref
> [A Visual Guide to SSH Tunnels: Local and Remote Port Forwarding (iximiuz.com)](https://iximiuz.com/en/posts/ssh-tunnels/)

### SSH Tunnel 如何實現 「Local Port Forwarding」？
{{< hint info >}}
與「WSL or MacOS 要 access VM 內的服務場景一致」
```tpl
# Redirec MacOS Port(1313) to Hugo Server in VM(localhost:1313)
ssh -L 1313:localhost:1313 -fN garlic@garlic
```
{{< /hint>}}
-    -L ：Local port forwarding，`ssh` client 開 extra port 要聽存取 「`sshd` server 機器上的服務」或「`sshd` server 機器同LAN上的服務」
- "ssh **-L** **l**ocal:remote"

![](https://i.imgur.com/FMXSWHb.png)


### SSH Tunnel 如何實現 「Local Port Forwarding with a Bastion Host」？
-   -L ：Local port forwarding，`ssh` client 開 extra port 要聽存取 「`sshd` server 機器上的服務」或「`sshd` server 機器同LAN上的服務」
- "ssh **-L** **l**ocal:remote"
![](https://i.imgur.com/qWa6VnK.png)


### SSH Tunnel 如何實現 「Remote Port Forwarding」？
- -R ：Remote port forwarding，`sshd` server 開 extra port 要聽存取 「`ssh` client 機器上的服務」或「`ssh` client 機器同LAN上的服務」
- "ssh **-R** **r**emote:local"
![](https://i.imgur.com/l9yX0ez.png)


### SSH Tunnel 如何實現 「Remote Port Forwarding from a Home/Private Network」？
-   -R ：Remote port forwarding，`sshd` server 開 extra port 要聽存取 「`ssh` client 機器上的服務」或「`ssh` client 機器同LAN上的服務」
- "ssh **-R** **r**emote:local"
![](https://i.imgur.com/J8dya5y.png)

