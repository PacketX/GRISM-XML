---
description: stripping TCP/UDP payload
---

# Stripping Payload

```
<run>
    <output id="1">
        <port>P7</out>
        <stripping>payload</stripping>
    </output>
    <chain>
        <in>P6</in>
        <out>O1</out>
    </chain>
</run>
```
