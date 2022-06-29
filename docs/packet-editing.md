---
description: Edit packet header like Mac address, IP address and packet payload masking
---

# Packet Editing

### Modify IP address

```xml
<run>
    <filter id="1" >
    <or>
	<find name="udp.dstport" relation="==" content="53" />
    </or>
    </filter>
    <output id="1">
        <port>P7</port>
        <modify_dstip>8.8.8.8</modify_srcip>
    </output>
    <chain>
        <in>P6</in>
        <fid>F1</fid>
        <out>O1</out>
    </chain>
</run>
```
