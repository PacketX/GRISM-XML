# Element - Output
Defines the Output. 
It has a start tag &lt;output&gt; and an end tag &lt;/output&gt;.

It can be used in &lt;out&gt;&lt;out&gt; replace default port like P0,P1,..etc.

And output id=1 -> O1, refer to Example

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| type | output type | String | mix |
| name | Specifies a name for an element | String | |
| mtu | Maximum Transmission Unit | Interger | 0(unlimited) |
| stl | Second To Live | Interger | 0(unlimited) |


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
&lt;port&gt;, &lt;Q&gt;, &lt;QinQ&gt;, &lt;stripping&gt;, &lt;tagging&gt;, &lt;maxlen&gt;, &lt;modify_srcip&gt;, &lt;modify_dstip&gt;, &lt;modify_srcmac&gt;, &lt;modify_dstmac&gt;, &lt;dir&gt;, &lt;nvgre_dip&gt;, &lt;arp_reply_target_mac&gt;, &lt;dns_response_ipv4&gt;

### &lt;port&gt;
Defines output port(must have). 
It has a start tag &lt;port&gt; and an end tag &lt;/port&gt;.

```
<output id="1">
  <port>P0</port>
</output>
```

### &lt;Q&gt;
Defines vlan tagging. 
It has a start tag &lt;Q&gt; and an end tag &lt;/Q&gt;.

```
<output id="1">
  <port>P0</port>
  <Q>10</Q>
</output>
```

### &lt;QinQ&gt;
Defines vlan layer 2 tagging. 
It has a start tag &lt;QinQ&gt; and an end tag &lt;/QinQ&gt;.
```
<output id="1">
  <port>P0</port>
  <QinQ>20</QinQ>
</output>
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
<output id="1">
  <port>P0</port>
  <stripping>vlan</stripping>
</output>
```

### &lt;modify_srcip&gt;
Defines modify source ip address
It has a start tag &lt;modify_srcip&gt; and an end tag &lt;/modify_srcip&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_srcip>10.1.1.0</modify_srcip>
</output>
```

### &lt;modify_dstip&gt;
Defines modify destination ip address
It has a start tag &lt;modify_dstip&gt; and an end tag &lt;/modify_dstip&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_dstip>10.1.1.0</modify_dstip>
</output>
```

### &lt;modify_srcmac&gt;
Defines modify source mac address
It has a start tag &lt;modify_srcmac&gt; and an end tag &lt;/modify_srcmac&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_srcmac>d8:fe:e3:a4:d3:78</modify_srcmac>
</output>
```

### &lt;modify_dstmac&gt;
Defines modify destination mac address
It has a start tag &lt;modify_dstmac&gt; and an end tag &lt;/modify_dstmac&gt;.

```
<output id="1">
  <port>P0</port>
  <modify_dstmac>d8:fe:e3:a4:d3:78</modify_dstmac>
</output>
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
<output id="1">
  <port>P0</port>
  <tagging>grism</taging>
</output>
```

### &lt;maxlen&gt;
Defines packet max length. 
It has a start tag &lt;maxlen&gt; and an end tag &lt;/maxlen&gt;.
```
<output id="1">
  <port>P0</port>
  <maxlen>64</maxlen>
</output>
```

### &lt;dir&gt;
Defines output dir in Harddisk. Save packet to pcap files.
It has a start tag &lt;dir&gt; and an end tag &lt;/dir&gt;.
```
<output id="1">
 <port>H1</port>
 <dir>test</dir>
</output>
```

### &lt;nvgre_dip&gt;
Defines output to gre tunnel. must setting interface port ip addr first.
It has a start tag &lt;nvgre_dip&gt; and an end tag &lt;/nvgre_dip&gt;.
```
<output id="1">
  <port>P7</port>
  <nvgre_dip>192.168.1.201</nvgre_dip>
</output>

```

### &lt;arp_reply_target_mac&gt;
Defines output reply arp target mac address.
It has a start tag &lt;arp_reply_target_mac&gt; and an end tag &lt;/arp_reply_target_mac&gt;.
```
<output id="1">
  <port>P0</port>
  <arp_reply_target_mac>00:0f:bb:ef:8a:25</arp_reply_target_mac>
</output>
```

Example for for inline (P6 <-> P7) reply target mac 02:00:00:00:00:00 when arp request ip 192.168.1.10
```
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

### &lt;dns_response_ipv4&gt;
Defines output response IPv4 address when dns query domain.
It has a start tag &lt;dns_response_ipv4&gt; and an end tag &lt;/dns_response_ipv4&gt;.
```
<output id="1">
  <port>P0</port>
  <dns_response_ipv4>192.168.1.150</dns_response_ipv4>
</output>
```

Example for inline (P6 <-> P7) response ip 192.168.1.201 when dns query google.com
```
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
    <output id="1">
        <port>P6</port>
        <dns_response_ipv4>192.168.1.201</dns_response_ipv4>
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

### type : httprequesthijack
Defines output http request hijack (and redirect to safeweb).

Example for inline (P6 <-> P7) redirect http request url www.httrack.com/ to https://safeweb.secure365.hinet.net/
```
<run>
  <filter id="1" sessionBase="no">
    <or>
      <find name="http.request.url" relation="==" content="www.httrack.com/" />
    </or>
  </filter>
  <output id="1" type="httprequesthijack">
    <port>P6</port>
    <redirect2safeweb>https://safeweb.secure365.hinet.net/</redirect2safeweb>
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


