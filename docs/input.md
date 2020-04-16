# Element - Input
Defines the Input. 
It has a start tag &lt;input&gt; and an end tag &lt;/input&gt;.

Two main funcitons, "replay pcap files" and "traffic generator".

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger |  |
| type | Specifies a type for an element | String | replayPcap or traffic-gen |

## Elements in Input - replayPcap
Before using this function, make sure you upload pcap files to the correct path first.

### Example
```xml
<run>
<input type="replayPcap">
        <port>P0</port>
        <filepath>H1/in/sample.pcap</filepath>
        <time>1</time>
        <msinterval>1</msinterval>   
</input>
</run>
```

### port
Defines output port<B>(must have)</B>.

It has a start tag &lt;port&gt; and an end tag &lt;/port&gt;.
```
  <port>P0</port>
```
### filepath
Defines pcap filepath<B>(must have)</B>.

It has a start tag &lt;filepath&gt; and an end tag &lt;/filepath&gt;.
```
<filepath>H1/in/sample.pcap</filepath>
```
### time
Defines play time<B>(must have)</B>.

It has a start tag &lt;time&gt; and an end tag &lt;/time&gt;.
```
<time>1</time>
```

### msinterval
Defines the play ms interval between each packet. 

It has a start tag &lt;msinterval&gt; and an end tag &lt;/msinterval&gt;.
```
<msinterval>1</msinterval>
```

## Elements in Input - traffic-gen
generate traffic

### Example
```xml
<run>
  <input type="traffic-gen">
        <port>P0</port>
        <protocol>TCP</protocol>
        <packet_size>1024</packet_size>
        <speed>10000</speed>
        <payload_text>abcdefg</payload_text>
        <src_ip>10.1.0.99</src_ip>
        <src_ip_min>10.1.0.0</src_ip_min>
        <src_ip_max>10.1.0.99</src_ip_max>
        <src_ip_inc>5</src_ip_inc>
        <dest_ip>11.1.1.99</dest_ip>
        <dest_ip_min>11.1.1.0</dest_ip_min>
        <dest_ip_max>11.1.2.99</dest_ip_max>
        <dest_ip_inc>2</dest_ip_inc>
        <src_port>1234</src_port>
        <src_port_min>2</src_port_min>
        <src_port_max>9999</src_port_max>
        <src_port_inc>111</src_port_inc>
        <dest_port>2222</dest_port>
        <dest_port_min>0</dest_port_min>
        <dest_port_max>65535</dest_port_max>
        <dest_port_inc>222</dest_port_inc>
    </input>
</run>
```

### port
Defines output port<B>(must have)<B>.

It has a start tag &lt;port&gt; and an end tag &lt;/port&gt;.
```
  <port>P0</port>
```
### protocol
Defines protocol TCP/UDP, default UDP

It has a start tag &lt;protocol&gt; and an end tag &lt;/protocol&gt;.
```
<protocol>UDP</protocol>
```
### packet_size
Defines packet size, default 512 

It has a start tag &lt;packet_size&gt; and an end tag &lt;/packet_size&gt;.
```
<packet_size>1024</packet_size>
```

### speed
Defines speed, default is full line rate. 

It has a start tag &lt;speed&gt; and an end tag &lt;/speed&gt;.
```
<speed>10000</speed>
```

### payload_text
Defines payload text

It has a start tag &lt;payload_text&gt; and an end tag &lt;/payload_text&gt;.
```
<payload_text>abcdefg</payload_text>
```

### src_ip
Defines source ip

It has a start tag &lt;src_ip&gt; and an end tag &lt;/src_ip&gt;.
```
<src_ip>10.1.0.99</src_ip>
```

### src_ip_min
Defines minimum source ip

It has a start tag &lt;src_ip_min&gt; and an end tag &lt;/src_ip_min&gt;.
```
<src_ip_min>10.1.0.0</src_ip_min>
```

### src_ip_max
Defines maximum source ip

It has a start tag &lt;src_ip_max&gt; and an end tag &lt;/src_ip_max&gt;.
```
<src_ip_max>10.1.0.99</src_ip_max>
```
### src_ip_inc
Defines the number to increase source ip 

It has a start tag &lt;src_ip_inc&gt; and an end tag &lt;/src_ip_inc&gt;.
```
<src_ip_inc>5</src_ip_inc>
```

### src_port
Defines source port

It has a start tag &lt;src_port&gt; and an end tag &lt;/src_port&gt;.
```
<src_port>1234</src_port>
```

### src_port_min
Defines minimum source port

It has a start tag &lt;src_port_min&gt; and an end tag &lt;/src_port_min&gt;.
```
<src_port_min>2</src_port_min>
```

### src_port_max
Defines maximum source port

It has a start tag &lt;src_port_max&gt; and an end tag &lt;/src_port_max&gt;.
```
<src_port_max>9999</src_port_max>
```

### src_port_inc
Defines the number to increase source port

It has a start tag &lt;src_port_inc&gt; and an end tag &lt;/src_port_inc&gt;.
```
 <src_port_inc>10</src_port_inc>
```

### dest_ip
### dest_ip_min
### dest_ip_max
### dest_ip_inc
### dest_port
### dest_port_min
### dest_port_max
### dest_port_inc

please refer to src_ip and src_port
