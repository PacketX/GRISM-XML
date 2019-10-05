# Element - Output
Defines the Output. 
It has a start tag &lt;output&gt; and an end tag &lt;/output&gt;.

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| name | Specifies a name for an element | String | |
| mtu | Maximum Transmission Unit | Interger | 0(unlimited) |

## Example
```xml
<output id="1">
  <port>P0</port>
  <stripping>vlan</stripping>  
</output>
```

## Elements in Output
&lt;port&gt;, &lt;Q&gt;, &lt;QinQ&gt;, &lt;stripping&gt;
### port
Defines output port. 
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
Defines stripping
It has a start tag &lt;stripping&gt; and an end tag &lt;/stripping&gt;.

#### support type
- payload 
- vlan
- mpls
- gre
- vxlan
- gre-erspan

```
 <stripping>vlan</stripping>
```



