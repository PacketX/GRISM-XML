# Element - Action
Defines the Action.
It has a start tag &lt;action&gt; and an end tag &lt;/action&gt;.

 For example, input packets process

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| name | Specifies a name for an element | String | |
| type | action type | String | * |

## Example
```xml
<run>
  <action id="1" type="input-packet-process">
    <port>P0</port>
    <stripping>vlan</stripping>
  </action>
</run>
```

## Elements in Action
### input-packet-process type
&lt;port&gt;, &lt;Q&gt;, &lt;QinQ&gt;, &lt;stripping&gt;, &lt;tagging&gt;, &lt;maxlen&gt;

### &lt;port&gt;
Defines input port(must have). 
It has a start tag &lt;port&gt; and an end tag &lt;/port&gt;.

```
<action id="1" type="input-packet-process">
  <port>P0</port>
</action>
```

### &lt;Q&gt;
Defines vlan tagging. 
It has a start tag &lt;Q&gt; and an end tag &lt;/Q&gt;.

```
<action id="1" type="input-packet-process">
  <port>P0</port>
  <Q>10</Q>
</action>
```

### &lt;QinQ&gt;
Defines vlan layer 2 tagging. 
It has a start tag &lt;QinQ&gt; and an end tag &lt;/QinQ&gt;.
```
<action id="1" type="input-packet-process">
  <port>P0</port>
  <QinQ>20</QinQ>
</action>
```

### &lt;stripping&gt;
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
<action id="1" type="input-packet-process">
  <port>P0</port>
  <stripping>vlan</stripping>
</action>
```

### &lt;tagging&gt;
Defines tagging. 
It has a start tag &lt;tagging&gt; and an end tag &lt;/tagging&gt;.

#### support type
- timestamp 
- gtp
- gtp2
- grism

```
<action id="1" type="input-packet-process">
  <port>P0</port>
  <tagging>grism</taging>
</action>
```

### &lt;maxlen&gt;
Defines packet max length. 
It has a start tag &lt;maxlen&gt; and an end tag &lt;/maxlen&gt;.
```
<action id="1" type="input-packet-process">
  <port>P0</port>
  <maxlen>64</maxlen>
</action>
```

