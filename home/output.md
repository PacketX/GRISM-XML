---
description: Defines the Output. It has a start tag <output> and an end tag </output>.
---

# Element \<output>

It can be used in \<out>\<out> replace default port like P0,P1,..etc.

And output id=1 -> O1, refer to Example

## Attribute

| Attribute       | Description                          | Type     | Default (\* must have) | Support  |
| --------------- | ------------------------------------ | -------- | ---------------------- | -------- |
| id              | Specifies a unique id for an element | Interger | \*                     |          |
| type            | output type                          | String   | mix                    |          |
| name            | Specifies a name for an element      | String   |                        |          |
| mtu             | Maximum Transmission Unit            | Interger | 0(unlimited)           |          |
| stl             | Second To Live                       | Interger | 0(unlimited)           |          |
| minbps          | Minimum bandwidth reserved           | Interger | 0(unlimited)           | ver. 3.7 |
| maxbps          | Maximum bandwidth reserved           | Interger | 0(unlimited)           | ver. 3.7 |
| arp\_dstip\_mac | arp request for dstip mac            | yes/no   | no                     |          |

## Example

```xml
<run>
  <output id="1">
    <port>P0</port>
    <stripping>vlan</stripping>
  </output>
  <chain>
    <in>P1</in>
    <out>O1</out>
  </chain>
</run>
```

## Elements in Output

\<port>, \<Q>, \<QinQ>, \<stripping>, \<tagging>, \<maxlen>, \<modify\_srcip>, \<modify\_dstip>, \<modify\_srcmac>, \<modify\_dstmac>, \<dir>, \<nvgre\_dip>, \<arp\_reply\_target\_mac>, \<dns\_response\_ipv4>

### \<port>

Defines output port(must have). It has a start tag \<port> and an end tag \</port>.

```xml
<output id="1">
  <port>P0</port>
</output>
```

### \<gateway>

Defines gateway It has a start tag \<gateway> and an end tag \</gateway>. The ouptut will send arp request to gateway for mac address, than use this mac to replace destination mac address on packet.

```xml
<output id="1">
  <port>P0</port>
  <gateway>192.168.1.1</gateway>
</output>
```

### \<Q>

Defines vlan tagging. It has a start tag \<Q> and an end tag \</Q>.

```xml
<output id="1">
  <port>P0</port>
  <Q>10</Q>
</output>
```

### \<QinQ>

Defines vlan layer 2 tagging. It has a start tag \<QinQ> and an end tag \</QinQ>.

```xml
<output id="1">
  <port>P0</port>
  <QinQ>20</QinQ>
</output>
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

```xml
<output id="1">
  <port>P0</port>
  <stripping>vlan</stripping>
</output>
```

### \<modify\_srcip>

Defines modify source ip address It has a start tag \<modify\_srcip> and an end tag \</modify\_srcip>.

| Attribute | Description                                        | Type   | Default (\* must have) |
| --------- | -------------------------------------------------- | ------ | ---------------------- |
| nat       | NAT support, don't forget to set args->nat to true | yes/no | no                     |

```xml
<output id="1">
  <port>P0</port>
  <modify_srcip>10.1.1.0</modify_srcip>
</output>
```

### \<modify\_dstip>

Defines modify destination ip address It has a start tag \<modify\_dstip> and an end tag \</modify\_dstip>.

```xml
<output id="1">
  <port>P0</port>
  <modify_dstip>10.1.1.0</modify_dstip>
</output>
```

### \<modify\_srcmac>

Defines modify source mac address It has a start tag \<modify\_srcmac> and an end tag \</modify\_srcmac>.

```xml
<output id="1">
  <port>P0</port>
  <modify_srcmac>d8:fe:e3:a4:d3:78</modify_srcmac>
</output>
```

### \<modify\_src\_default\_mac/>

Defines modify source mac address use port default mac address (ver. 3.8)

```xml
<output id="1">
  <port>P0</port>
  <modify_src_default_mac/>
</output>
```

### \<modify\_dstmac>

Defines modify destination mac address It has a start tag \<modify\_dstmac> and an end tag \</modify\_dstmac>.

```xml
<output id="1">
  <port>P0</port>
  <modify_dstmac>d8:fe:e3:a4:d3:78</modify_dstmac>
</output>
```

### \<tagging>

Defines tagging. It has a start tag \<tagging> and an end tag \</tagging>.

#### support type

* timestamp
* gtp
* gtp2
* grism

```xml
<output id="1">
  <port>P0</port>
  <tagging>grism</taging>
</output>
```

### \<maxlen>

Defines packet max length. It has a start tag \<maxlen> and an end tag \</maxlen>.

```xml
<output id="1">
  <port>P0</port>
  <maxlen>64</maxlen>
</output>
```

### \<dir>

Defines output dir in Hard disk. Save packet to pcap files. It has a start tag \<dir> and an end tag \</dir>.

| Attribute        | Description               | Type           | Default (\* must have) |
| ---------------- | ------------------------- | -------------- | ---------------------- |
| timeout          | timeout to next pcap file | seconds        | 0 (No timeout)         |
| max\_split\_size | max pcap size             | integer(bytes) | 104857600 (100M)       |

```xml
<output id="1">
 <port>H1</port>
 <dir>test</dir>
</output>
```

### \<nvgre\_dip>

Defines output to gre tunnel. must setting interface port ip addr first. It has a start tag \<nvgre\_dip> and an end tag \</nvgre\_dip>.

```xml
<output id="1">
  <port>P7</port>
  <nvgre_dip>192.168.1.201</nvgre_dip>
</output>
```

### \<arp\_reply\_target\_mac>

Defines output reply arp target mac address. It has a start tag \<arp\_reply\_target\_mac> and an end tag \</arp\_reply\_target\_mac>.

```xml
<output id="1">
  <port>P0</port>
  <arp_reply_target_mac>00:0f:bb:ef:8a:25</arp_reply_target_mac>
</output>
```

Example for for inline (P6 <-> P7) reply target mac 02:00:00:00:00:00 when arp request ip 192.168.1.10

```xml
<run>
    <filter id="1" sessionBase="no">
    <or>
         <find name="arp.request.target.ip" relation="" content="192.168.1.10" />
    </or>
    </filter>
    <output id="1">
        <port>P6</port>
        <arp_reply_target_mac>02:00:00:00:00:00</arp_reply_target_mac>
    </output>
    <chain>
        <in>P6</in>
        <fid>F1</fid>
        <out>O1</out>
        <next type="notmatch">
            <out>P7</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <out>P6</out>
    </chain>
</run>
```

### \<arp\_reply\_default\_mac/>

Defines output reply arp default port mac address. (ver. 3.8)

```xml
<output id="1">
    <port>P6</port>
    <arp_reply_default_mac/>
</output>
```

### \<dns\_response\_ipv4>

Defines output response IPv4 address when dns query domain (not support EDNS yet). It has a start tag \<dns\_response\_ipv4> and an end tag \</dns\_response\_ipv4>.

#### dns\_response\_ipv4 Attribute

| Attribute | Description            | Type      | Default (\* must have) |
| --------- | ---------------------- | --------- | ---------------------- |
| noswapmac | do'nt swap mac address | yes or no | no                     |

```xml
<output id="1">
  <port>P0</port>
  <dns_response_ipv4 noswapmac="yes">192.168.1.150</dns_response_ipv4>
</output>
```

Example for inline (P6 <-> P7) response ip 192.168.1.201 when dns query google.com

```xml
<run>
    <filter id="1" sessionBase="no">
    <or>
        <find n="dns.qry.name" r="==" c="google.com" />
        <find n="dns.qry.name" r="==" c="www.google.com" />
        <find n="dns.qry.name" r="==" c="ssl.gstatic.com" />
        <find n="dns.qry.name" r="==" c="www.gstatic.com" />
        <find n="dns.qry.name" r="==" c="apis.google.com" />
    </or>
    </filter>
    <!-- dns query type IPv4 and not EDNS -->
    <filter id="2" sessionBase="no">
    <or>
        <find n="dns.qry.type" r="==" c="1" />
        <find n="dns.count.add_rr" r="==" c="0" />
    </or>
    </filter>
    <output id="1">
        <port>P6</port>
        <dns_response_ipv4>192.168.1.201</dns_response_ipv4>
    </output>
    <chain>
        <in>P6</in>
        <fid type="and">F1,F2</fid>
        <out>O1</out>
        <next type="notmatch">
            <out>P7</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <out>P6</out>
    </chain>
</run>
```

### type : httprequesthijack

Defines output http request hijack (and redirect to safeweb).

#### redirect2safeweb Attribute

| Attribute    | Description            | Type         | Default (\* must have) |
| ------------ | ---------------------- | ------------ | ---------------------- |
| noswapmac    | do'nt swap mac address | yes or no    | no                     |
| redirectPort | redirect to Port       | port (ex.P7) |                        |

Example for inline (P6 <-> P7) redirect http request url www.com/ to https://safeweb.secure365.hinet.net/

```xml
<run>
  <filter id="1" sessionBase="no">
    <or>
      <find name="http.request.url" relation="==" content="www.com/" />
    </or>
  </filter>
  <output id="1" type="httprequesthijack">
    <port>P7</port>
    <redirect2safeweb noswapmac="yes" redirectPort="P7">>https://safeweb.secure365.hinet.net/</redirect2safeweb>
  </output>
  <chain>
    <in>P6</in>
    <fid>F1</fid>
    <out>O1</out>
    <next type="notmatch">
      <out>P7</out>
    </next>
  </chain>
  <chain>
    <in>P7</in>
    <out>P6</out>
  </chain>
</run>

```

### type : udpencap

Defines output pcap header+packet throught UDP encapsulation.

Example

```xml
<run>
  <output id="1" type="udpencap">
    <port>P7</port>
    <dip>192.168.1.201</dip>
    <sport>3060</sport>
    <dport>3060</dport>
  </output>
  <chain>
    <in>P6</in>
    <out>O1</out>
  </chain>
</run>
```
