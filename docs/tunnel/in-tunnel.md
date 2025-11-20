---
description: In-Tunnel functions
---

# In-Tunnel

### Enable In-Tunnel

#### Config XML

```xml
<configSet reboot="no">
    <filters>
        <in-tunnels>
            <GTP>True</GTP>
            <GRE>True</GRE>
            <IPV4>True</IPV4>
            <VXLAN>True</VXLAN>
        </in-tunnels>
    </filters>
</configSet>
```

### In-Tunnel filter, de-tunnel and load balance Example

#### GRISM XML

```xml
<run>
    <filter id="1" sessionBase="no">
        <or>
	    <find name="ip.addr" relation="==" content="192.168.1.0/24" />
        </or>
    </filter>
    <output id="1">
        <port>P1</port>
        <stripping>gtp</stripping>
    </output>
    <output id="2">
        <port>P2</port>
        <stripping>gtp</stripping>
    </output>
    <chain>
        <in>P6</in>
        <fid>F1</fid>
        <out type="loadBalance" lbtype="5thash">O1,O2</out>
    </chain>
</run>
```
