---
description: Block SSL sni and ja3
---

# Block SSL Sample

```
        WAN
         |
         |P7 
  --------------- 
 |               |
 |     GRISM     |
 |               |
  --------------- 
         |P6
         |
        LAN
```

### Block sni

```xml
<run>
    <filter id="1" sessionBase="no">
        <or>
            <find name="ssl.server_name" relation="==" content="www.googleapi.com"/>
        </or>
    </filter>
    <chain>
        <in>P6</in>
        <fid>F1</fid>
        <out>0</out>
        <next type="notmatch">
            <out>P7</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <out>P6</out>
    </chain>
</run>
```

### Block ja3

```xml
<run>
    <filter id="1" sessionBase="no">
        <or>
            <find name="ssl.ja3_digest" relation="==" content="39e62db039deed96a9daf75dacdbd207"/>
        </or>
    </filter>
    <chain>
        <in>P6</in>
        <fid>F1</fid>
        <out>0</out>
        <next type="notmatch">
            <out>P7</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <out>P6</out>
    </chain>
</run>
```

