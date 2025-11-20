---
description: Defines the Action. It has a start tag <action> and an end tag </action>.
---

# Element \<action>

Two main funcitons, "input packet process" and "link pairs".

GRISM AH32 is **not supported**

## Attribute

<table><thead><tr><th width="150">Attribute</th><th width="213.26479750778813">Description</th><th width="150">Type</th><th>Default (* must have)</th></tr></thead><tbody><tr><td>id</td><td>Specifies id for an element</td><td>Interger</td><td>0</td></tr><tr><td>name</td><td>Specifies a name for an element</td><td>String</td><td></td></tr><tr><td>type</td><td>action type<br>* input-packet-process<br>* linkpairs</td><td>String</td><td>input-packet-process</td></tr></tbody></table>

Example

```xml
<run>
  <action>
    <port>P0</port>
    <stripping>vlan</stripping>
  </action>
</run>
```

## Elements in Action

### input-packet-process type

### \<port>

Defines input port(must have). It has a start tag \<port> and an end tag \</port>.

```xml
<action>
  <port>P0</port>
</action>
```

### \<Q>

Defines vlan tagging. It has a start tag \<Q> and an end tag \</Q>.

```xml
<action>
  <port>P0</port>
  <Q>10</Q>
</action>
```

### \<QinQ>

Defines vlan layer 2 tagging. It has a start tag \<QinQ> and an end tag \</QinQ>.

```xml
<action>
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
* mpls-in-gre

```xml
<action>
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
<action>
  <port>P0</port>
  <tagging>grism</taging>
</action>
```

### \<maxlen>

Defines packet max length. It has a start tag \<maxlen> and an end tag \</maxlen>.

```xml
<action>
  <port>P0</port>
  <maxlen>64</maxlen>
</action>
```

### \<ip>

Defines IP. It has a start tag \<ip> and an end tag \</ip>.

```xml
<action>
  <port>P0</port>
  <ip>192.168.1.100</ip>
</action>
```

### \<netmask> (v7.0)

Defines netmask. It has a start tag \<netmask> and an end tag \</netmask>.

### \<gateway> (v7.0)

Defines IP. It has a start tag \<gateway> and an end tag \</gateway>.

```xml
<action>
  <port>P0</port>
  <ip>192.168.1.100</ip>
  <netmask>255.255.255.0</netmask>
  <gateway>192.168.1.1</gateway>
</action>
```

### \<arp\_reply\_default\_mac>

Defines arp reply default mac address.  It has a start tag \<arp\_reply\_default\_mac/> .

```xml
<action>
  <port>P0</port>
  <ip>192.168.1.100</ip>
  <arp_reply_default_mac/>
</action>
```

### \<icmp\_reply>

Defines icmp reply. It has a start tag \<icmp\_reply/> .

```xml
<action>
  <port>P0</port>
  <ip>192.168.1.100</ip>
  <icmp_reply/>
</action>
```

### \<icmp\_reply\_fragment\_need>

Defines icmp reply fragment need. It has a start tag \<icmp\_reply\_fragment\_need /> .

#### Attritube

<table><thead><tr><th width="150">Attribute</th><th width="213.26479750778813">Description</th><th width="150">Type</th><th>Default (* must have)</th></tr></thead><tbody><tr><td>mtu</td><td>Specifies mtu size</td><td>Interger</td><td>0*</td></tr></tbody></table>

```xml
<action>
  <port>P0</port>
  <ip>192.168.1.100</ip>
  <icmp_reply_fragment_need mtu="1492"/>
</action>
```

### linkpairs type

If portA down, force portB down, and vice versa.

```xml
<action type="linkpairs">
  <portA>P1</portA>
  <portB>P2</portB>
</action>
```
