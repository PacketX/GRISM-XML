---
description: Coming soon! (ver 4.3)
---

# Element \<script>

## Attribute

## Example

### print

```javascript
<script>
    print("<!-- hello -->");
</script>
```

```javascript
<script>
    function only_dns (inport,outport)
    {
        print ("<filter id=\"10\"><or><find name=\"udp.port\" relation=\"==\" content=\"53\"></or></filter>");
        print ("<chain><in>"+inport+"</in><fid>F10</fid><out>"+outport+"</out></chain>");
    }
    only_dns("P0","P1");
</script>
```

### common.js

#### port\_mirror (inports, outports)

#### port\_inline (porta, portb)

```javascript
<script src="common.js"></script>
<script>
    port_mirror("P0", "P1,P2");
</script>
```
