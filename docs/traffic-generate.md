# Traffic Generate

```xml
<run>
  <input type="traffic-gen">
        <port>P0</port>
        <protocol>TCP</protocol>
        <packet_size>1024</packet_size>
        <speed>10000</speed>
        <payload_text>abcdefg</payload_text>
        <src_mac>00:0d:48:28:28:56</src_mac>
        <dest_mac>00:0d:48:28:28:57</dest_mac>  
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
