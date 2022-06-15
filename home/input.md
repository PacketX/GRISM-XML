# Element - Input

Defines the Input. It has a start tag \<input> and an end tag \</input>.

Two main funcitons, "replay pcap files" and "traffic generator".

## Attribute

| Attribute | Description                          | Type     | Default (\* must have)    |
| --------- | ------------------------------------ | -------- | ------------------------- |
| id        | Specifies a unique id for an element | Interger |                           |
| type      | Specifies a type for an element      | String   | replayPcap or traffic-gen |

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

Defines output port**(must have)**.

It has a start tag \<port> and an end tag \</port>.

```
  <port>P0</port>
```

### time

Defines play time**(must have)**.

It has a start tag \<time> and an end tag \</time>.

```
<time>1</time>
```

### filepath

Defines pcap filepath**(either filepath or scandir must have)**.

It has a start tag \<filepath> and an end tag \</filepath>.

```
<filepath>H1/in/sample.pcap</filepath>
```

### scandir

Defines pcap scandir**(either filepath or scandir must have)**.

It has a start tag \<scandir> and an end tag \</scandir>., limit 1024 files

#### Attribute

| Attribute                              | Description                                                | Type     | Default (\* must have) |
| -------------------------------------- | ---------------------------------------------------------- | -------- | ---------------------- |
| interval                               | Scan interval                                              | Seconds  | 60                     |
| minbytes                               | will replay if pcap file bigger than minbytes              | Interger | 0                      |
| timeout                                | force replay if pcap file less than minbytes after timeout | Interger | 0                      |

```xml
<scandir interval="10" minbytes="1048576" timeout="60">H1/in</scandir>
```

### playedFilesHandle

Defines pcap file handle after replay. 

It has a start tag \<playedFilesHandle> and an end tag \</playedFilesHandle>. must be **delete** or **move**

```
<playedFilesHandle>move</playedFilesHandle>
```

### playedFilesMoveTo

Defines pcap file move to dir after after replay.

It has a start tag \<playedFilesMoveTo> and an end tag \</playedFilesMoveTo>.

```
<playedFilesMoveTo>H1/in/played</playedFilesMoveTo>
```

### speed

Defines speed, default is full line rate.

It has a start tag \<speed> and an end tag \</speed>.

```
<speed>10000</speed>
```

### msinterval

Defines the play ms interval between each packet.

It has a start tag \<msinterval> and an end tag \</msinterval>.

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
        <src_ip_random>0</src_ip_random>
        <dest_ip>11.1.1.99</dest_ip>
        <dest_ip_min>11.1.1.0</dest_ip_min>
        <dest_ip_max>11.1.2.99</dest_ip_max>
        <dest_ip_inc>2</dest_ip_inc>
        <dest_ip_random>0</dest_ip_random>
        <src_port>1234</src_port>
        <src_port_min>2</src_port_min>
        <src_port_max>9999</src_port_max>
        <src_port_inc>1</src_port_inc>
        <src_port_random>0</src_port_random>
        <dest_port>2222</dest_port>
        <dest_port_min>0</dest_port_min>
        <dest_port_max>65535</dest_port_max>
        <dest_port_inc>1</dest_port_inc>
        <dest_port_random>0</dest_port_random>
    </input>
</run>
```

### port

Defines output port**(must have)**.

It has a start tag \<port> and an end tag \</port>.

```
  <port>P0</port>
```

### protocol

Defines protocol TCP/UDP, default UDP

It has a start tag \<protocol> and an end tag \</protocol>.

```
<protocol>UDP</protocol>
```

### packet\_size

Defines packet size, default 512

It has a start tag \<packet\_size> and an end tag \</packet\_size>.

```
<packet_size>1024</packet_size>
```

### speed

Defines speed, default is full line rate.

It has a start tag \<speed> and an end tag \</speed>.

```
<speed>10000</speed>
```

### payload\_text

Defines payload text

It has a start tag \<payload\_text> and an end tag \</payload\_text>.

```
<payload_text>abcdefg</payload_text>
```

### src\_ip

Defines source ip, default 10.0.1.99

It has a start tag \<src\_ip> and an end tag \</src\_ip>.

```
<src_ip>10.1.0.99</src_ip>
```

### src\_ip\_min

Defines minimum source ip

It has a start tag \<src\_ip\_min> and an end tag \</src\_ip\_min>.

```
<src_ip_min>10.1.0.0</src_ip_min>
```

### src\_ip\_max

Defines maximum source ip

It has a start tag \<src\_ip\_max> and an end tag \</src\_ip\_max>.

```
<src_ip_max>10.1.0.99</src_ip_max>
```

### src\_ip\_inc

Defines the number to increase source ip, default 0

It has a start tag \<src\_ip\_inc> and an end tag \</src\_ip\_inc>.

```
<src_ip_inc>5</src_ip_inc>
```

### src\_ip\_random

Defines source ip random (0 or 1), default 0

It has a start tag \<src\_ip\_random> and an end tag \</src\_ip\_random>.

```
<src_ip_random>1</src_ip_random>
```

### src\_port

Defines source port, default 5000

It has a start tag \<src\_port> and an end tag \</src\_port>.

```
<src_port>1234</src_port>
```

### src\_port\_min

Defines minimum source port

It has a start tag \<src\_port\_min> and an end tag \</src\_port\_min>.

```
<src_port_min>2</src_port_min>
```

### src\_port\_max

Defines maximum source port

It has a start tag \<src\_port\_max> and an end tag \</src\_port\_max>.

```
<src_port_max>9999</src_port_max>
```

### src\_port\_inc

Defines the number to increase source port, default 0

It has a start tag \<src\_port\_inc> and an end tag \</src\_port\_inc>.

```
 <src_port_inc>10</src_port_inc>
```

### src\_port\_random

Defines random source port (0 or 1), default 0

It has a start tag \<src\_port\_random> and an end tag \</src\_port\_random>.

```
 <src_port_random>1</src_port_random>
```

### dest\_ip

Defines destination ip,default 10.0.0.99

### dest\_ip\_min

Defines minimum destination ip

### dest\_ip\_max

Defines maximum destination ip

### dest\_ip\_inc

Defines the number to increase destination ip, default 0

### dest\_ip\_random

Defines destination ip random (0 or 1), default 0

### dest\_port

Defines destination port, default 5001

### dest\_port\_min

Defines minimum destination port

### dest\_port\_max

Defines maximum destination port

### dest\_port\_inc

Defines the number to increase destination port, default 0

### dest\_port\_random

Defines random destination port (0 or 1), default 0

//destination ip and port, please refer to src\_ip and src\_port for xml syntax
