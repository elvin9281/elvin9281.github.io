# brctl   
{{< hint info >}}
Ethernet Bridge Administration
{{< /hint >}}

- <font color=red>Create New Ethernet Bridge</font>
```bash
brctl addbr br0
```

- Display Available Bridge
```tpl
brctl show
```

- Delete Existing Bridge
```tpl
brctl delbr br0
```

-  Add an Interface/Multiple Interfaces to Existing Bridge
```tpl
brctl addif br0 eth0 eth1
```

- Tracking MAC address of a Bridge
```tpl
brctl showmacs br0
```

- Enable/Disable Spanning Tree on Ethernet Bridge
```tpl
# Enable
brctl stp br0 on
# Disable
brctl stp br0 off
```

- Display STP Parameter Values of a Bridge
```tpl
brctl showstp br0
```

