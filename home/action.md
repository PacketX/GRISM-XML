---
description: Defines the Action. It has a start tag <action> and an end tag </action>.
---

# Element \<action>

Two main funcitons, "input packet process" and "link pairs".

## Attribute

| Attribute | Description                          | Type     | Default (\* must have)            |
| --------- | ------------------------------------ | -------- | --------------------------------- |
| id        | Specifies a unique id for an element | Interger | \*                                |
| name      | Specifies a name for an element      | String   |                                   |
| type      | action type                          | String   | input-packet-process or linkpairs |

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

\<port>, \<Q>, \<QinQ>, \<stripping>, \<tagging>, \<maxlen>

### \<port>

Defines input port(must have). It has a start tag \<port> and an end tag \</port>.

```xml
<action id="1" type="input-packet-process">
  <port>P0</port>
</action>
```

### \<Q>

Defines vlan tagging. It has a start tag \<Q> and an end tag \</Q>.

```xml
<action id="1" type="input-packet-process">
  <port>P0</port>
  <Q>10</Q>
</action>
```

### \<QinQ>

Defines vlan layer 2 tagging. It has a start tag \<QinQ> and an end tag \</QinQ>.

```xml
<action id="1" type="input-packet-process">
  <port>P0</port>
  <QinQ>20</QinQ>
</action>
```

### \<stripping>

Defines stripping. It has a start tag \<stripping> and an end tag \</stripping>.

#### support type

* payload
* vlan
* mpls
* gre
* vxlan
* gre-erspan
* gtp
* grism
* mpls-in-udp

```xml
<action id="1" type="input-packet-process">
  <port>P0</port>
  <stripping>vlan</stripping>
</action>
```

### \<tagging>

Defines tagging. It has a start tag \<tagging> and an end tag \</tagging>.

#### support type

* timestamp
* gtp
* gtp2
* grism

```xml
<action id="1" type="input-packet-process">
  <port>P0</port>
  <tagging>grism</taging>
</action>
```

### \<maxlen>

Defines packet max length. It has a start tag \<maxlen> and an end tag \</maxlen>.

```xml
<action id="1" type="input-packet-process">
  <port>P0</port>
  <maxlen>64</maxlen>
</action>
```

### linkpairs type

If portA down, force portB down, and vice versa.

```xml
<action id="1" type="linkpairs">
  <portA>P1</portA>
  <portB>P2</portB>
</action>
```
