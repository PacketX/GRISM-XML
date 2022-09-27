---
description: Coming soon! (ver 4.3)
---

# Element \<script>

## Attribute

| Attribute | Description                      | Type   | Default (\* must have) |
| --------- | -------------------------------- | ------ | ---------------------- |
| src       | Specifies js filepath to include | String |                        |

## Functions

### print()

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

### grism\_heartbeat\_id\_get()

```javascript
var heartbeat_id = grism_heartbeat_id_get(lantoport, wantoport);
```

### common.js

#### port\_mirror (inports, outports)

```javascript
<script src="common.js"></script>
<script>
    port_mirror("P0", "P1,P2");
</script>
```

#### port\_inline (porta, portb)

```javascript
<script src="common.js"></script>
<script>
    port_inline ("P6", "P7");
</script>
```

#### port\_loadbalance (inports, outports, lbtype="5thash")

```javascript
<script src="common.js"></script>
<script>
    port_loadbalance ("P0", "P1,P2,P3,P4");
</script>
```

#### port\_inline\_bypass (lantoport, wantoport, lanport, wanport)

```javascript
<script src="common.js"></script>
<script>
    port_inline_bypass ("P4","P5","P6","P7");
</script>
```

#### port\_chain (inports, match, filter="", notmatch="", fid\_type="")

```javascript
<script src="common.js"></script>
<script>
    port_chain ("P0", "<out>P1</out>", "F1", "<out>P2</out>");
</script>
```

#### port\_chain\_if\_else (spaces, match, filter="", notmatch="", fid\_type="")

```javascript
<script src="common.js"></script>
<script>
    port_chain ("P0",
        port_chain_if_else ("    ", "<out>P1</out>", "F2", "<out>P2</out>"),
        "F1",
        "<out>P2</out>");
</script>
```
