# Element - Output
Defines the Output. 
It has a start tag &lt;output&gt; and an end tag &lt;/output&gt;.

It can be used in &lt;out&gt;&lt;out&gt; replace default port like P0,P1,..etc.

And output id=1 -> O1, refer to Example

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| name | Specifies a name for an element | String | |
| mtu | Maximum Transmission Unit | Interger | 0(unlimited) |

## Example
```xml
<run>
  <output id="1">
    <port>P0</port>
    <stripping>vlan</stripping>
  </output>
  <chain id="1">
    <in>P1</in>
    <out>O1</out>
  </chain>
</run>
```

## Elements in Output
&lt;port&gt;, &lt;Q&gt;, &lt;QinQ&gt;, &lt;stripping&gt;, &lt;tagging&gt;, &lt;maxlen&gt;, &lt;modify_srcip&gt;, &lt;modify_dstip&gt;, &lt;modify_srcmac&gt;, &lt;modify_dstmac&gt;, &lt;dir&gt;

### port
Defines output port(must have). 
It has a start tag &lt;port&gt; and an end tag &lt;/port&gt;.

```
 <port>P0</port>
```

### Q
Defines vlan tagging. 
It has a start tag &lt;Q&gt; and an end tag &lt;/Q&gt;.

```
 <Q>10</Q>
```

### QinQ
Defines vlan layer 2 tagging. 
It has a start tag &lt;QinQ&gt; and an end tag &lt;/QinQ&gt;.
```
 <QinQ>20</QinQ>
```

### stripping
Defines stripping. 
It has a start tag &lt;stripping&gt; and an end tag &lt;/stripping&gt;.

#### support type
- payload 
- vlan
- mpls
- gre
- vxlan
- gre-erspan
- gtp
- grism

```
 <stripping>vlan</stripping>
```

### tagging
Defines tagging. 
It has a start tag &lt;tagging&gt; and an end tag &lt;/tagging&gt;.

#### support type
- timestamp 
- gtp
- grism


```
 <stripping>vlan</stripping>
```

### maxlen
Defines packet max length. 
It has a start tag &lt;maxlen&gt; and an end tag &lt;/maxlen&gt;.
```
 <maxlen>64</maxlen>
```

### dir
Defines output dir in Harddisk. 
It has a start tag &lt;dir&gt; and an end tag &lt;/dir&gt;.
```
<output id="1">
 <port>H1</port>
 <dir>test</dir>
</output>
```





