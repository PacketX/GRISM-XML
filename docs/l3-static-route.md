# L3 Static Route

* inner: P6   10.10.1.1  10.10.1.0/24
* outer: P7   125.229.111.10 gateway: 168.95.98.254

```xml
<run>
    <action>
        <port>P6</port>
        <ip>10.10.1.1</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
    </action>
    <filter id="1" sessionBase="no">
        <and>
            <find name="ip.src" relation="==" content="10.10.1.10"/>
            <find name="tcp.srcport" relation="==" content="443"/>
        </and>
    </filter>
    <filter id="2" sessionBase="no">
        <or>
            <find name="tcp.dstport" relation="==" content="443"/>
        </or>
    </filter>  
    <output id="6" arp_dstip_mac="yes">
        <port>P6</port>
        <modify_src_default_mac/>
        <modify_dstip>10.10.1.10<modify_dstiop/>
    </output>
    <output id="7">
        <port>P7</port>
        <modify_src_default_mac/>
        <modify_srcip>125.229.111.10</modify_srcip>
        <gateway>168.95.98.254</gateway>
    </output>
    <chain>
        <in>P6</in>
        <fid>F1</fid>
        <out>O7</out>
    </chain>
    <chain>
        <in>P7</in>
        <fid>F2</fid>
        <out>O6</out>
    </chain>
</run>
```
