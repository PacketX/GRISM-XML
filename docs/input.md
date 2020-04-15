# Element - Input
Defines the Input. 
It has a start tag &lt;input&gt; and an end tag &lt;/input&gt;.

Two main funcitons, "replay pcap files" and "traffic generator".

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger |  |
| type | Specifies a type for an element | String | replayPcap or traffic-gen |


## Example (traffic-gen)
```xml
<run>
  <input type="traffic-gen">
        <port>P0</port>
        <protocol>TCP</protocol>
        <packet_size>1024</packet_size>
        <speed>1000</speed>
        <payload_text>abcdefg</payload_text>
        <src_ip>10.1.0.99</src_ip>
        <src_ip_min>10.1.0.0</src_ip_min>
        <src_ip_max>10.1.0.99</src_ip_max>
        <src_ip_inc>5</src_ip_inc>
    </input>
</run>
```

## Elements in Input - replayPcap
Before using this function, plesase upload pcap files to correct path.

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
Defines output port(must have). 
It has a start tag &lt;port&gt; and an end tag &lt;/port&gt;.
```
  <port>P0</port>
```
### filepath
Defines pcap filepath(must have). 
It has a start tag &lt;filepath&gt; and an end tag &lt;/filepath&gt;.
```
<filepath>H1/in/sample.pcap</filepath>
```
### time
Defines play time(must have). 
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
    </input>
</run>
```

### port
Defines output port(must have). 
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
Defines speed, default line rate. 
It has a start tag &lt;speed&gt; and an end tag &lt;/speed&gt;.
```
<speed>10000</speed>
```

TODO

