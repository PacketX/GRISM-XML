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
<output id="1">
  <port>P0</port>
</output>
```

### Q
Defines vlan tagging. 
It has a start tag &lt;Q&gt; and an end tag &lt;/Q&gt;.

```
<output id="1">
  <port>P0</port>
  <Q>10</Q>
</output>
```

### QinQ
Defines vlan layer 2 tagging. 
It has a start tag &lt;QinQ&gt; and an end tag &lt;/QinQ&gt;.
```
<output id="1">
  <port>P0</port>
  <QinQ>20</QinQ>
</output>
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
<output id="1">
  <port>P0</port>
  <stripping>vlan</stripping>
</output>
```

### modify_srcip
Defines modify source ip address
It has a start tag &lt;modify_srcip&gt; and an end tag &lt;/modify_srcip&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_srcip>10.1.1.0</modify_srcip>
</output>
```

### modify_dstip
Defines modify destination ip address
It has a start tag &lt;modify_dstip&gt; and an end tag &lt;/modify_dstip&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_dstip>10.1.1.0</modify_dstip>
</output>
```

### modify_srcmac
Defines modify source mac address
It has a start tag &lt;modify_srcmac&gt; and an end tag &lt;/modify_srcmac&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_srcmac>d8:fe:e3:a4:d3:78</modify_srcmac>
</output>
```

### modify_dstmac
Defines modify destination mac address
It has a start tag &lt;modify_dstmac&gt; and an end tag &lt;/modify_dstmac&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_dstmac>d8:fe:e3:a4:d3:78</modify_dstmac>
</output>
```

### tagging
Defines tagging. 
It has a start tag &lt;tagging&gt; and an end tag &lt;/tagging&gt;.

#### support type
- timestamp 
- gtp
- grism

```
<output id="1">
  <port>P0</port>
  <tagging>grism</taging>
</output>
```

### maxlen
Defines packet max length. 
It has a start tag &lt;maxlen&gt; and an end tag &lt;/maxlen&gt;.
```
<output id="1">
  <port>P0</port>
  <maxlen>64</maxlen>
</output>
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

