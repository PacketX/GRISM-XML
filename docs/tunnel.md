---
description: GRE/GTP/UDP Tunnel
---

# Tunnel

### GRE Tunnel

```xml
<run>
    <output id="1">
        <port>P7</port>
        <nvgre_dip>192.168.1.201</nvgre_dip>
    </output>
    <chain>
        <in>P6</in>
        <out>O1</out>
    </chain>
</run>
```
