---
description: Coming soon! (ver 4.4)
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
