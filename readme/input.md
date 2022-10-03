---
description: Lightweight javascript language support (ver 4.3)
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
<![CDATA[
    print('<!-- hello -->');
]]>
</script>
```

### grism\_heartbeat\_id\_get()

```javascript
<script>
<![CDATA[
    var heartbeat_id = grism_heartbeat_id_get(lantoport, wantoport);
]]>
</script
```

### common.js

#### port\_mirror (inports, outports)

```javascript
<script src="common.js"></script>
<script>
<![CDATA[
    port_mirror('P0', 'P1,P2');
]]>
</script>
```

#### port\_inline (porta, portb)

```javascript
<script src="common.js"></script>
<script>
<![CDATA[
    port_inline ('P6', 'P7');
]]>
</script>
```

#### port\_loadbalance (inports, outports, lbtype='5thash')

```javascript
<script src="common.js"></script>
<script>
<![CDATA[
    port_loadbalance ('P0', 'P1,P2,P3,P4');
]]>
</script>
```

#### port\_inline\_bypass (lantoport, wantoport, lanport, wanport)

```javascript
<script src="common.js"></script>
<script>
<![CDATA[
    port_inline_bypass ('P4','P5','P6','P7');
-->
</script>
```

#### port\_chain (inports, match, filter='', notmatch='', fid\_type='')

```javascript
<script src="common.js"></script>
<script>
<![CDATA[
    port_chain ('P0', 'P1', 'F1', 'P2');
]]>
</script>
```

#### port\_chain\_next (match, filter='', notmatch='', fid\_type='')

```javascript
<script src="common.js"></script>
<script>
<![CDATA[
    port_chain ('P0', 'P1', 'F1',
        port_chain_next ('P2', 'F2', '<out type="loadBalance">P3,P4</out>'),
    );
]]>
</script>
```
