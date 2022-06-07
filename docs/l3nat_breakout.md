## L3 NAT Breakout

P5: other outer P6: inner P7: outer

Set P6 NAT Breakout to P5 according to filter

### Config XML
```xml
<configSet reboot="no">
    <args>
        <nat>true</nat>   
    </args>
</configSet>
```

### GRISM XML

```xml
<run>
    <filter id="100" alt="breakout server" sessionBase="no">
        <or>
            <find name="ip.dst" relation="==" content="8.8.8.8"/>
        </or>
    </filter>
    <filter id="3" sessionBase="no">
        <or>
            <find name="arp.request.target.ip" relation="==" content="192.168.50.10"/>
        </or>
    </filter>
    <output id="3">
        <port>P5</port>
        <arp_reply_default_mac/>
    </output>
    <output id="5">
        <port>P5</port>
        <modify_src_default_mac/>
        <modify_srcip nat="yes">192.168.50.10</modify_srcip>
        <gateway>192.168.50.1</gateway>
    </output>
    <output id="6" arp_dstip_mac="yes">
        <port>P6</port>
    </output>
    <chain>
        <in>P6</in>
        <fid>F100</fid>
        <out>O5</out>
        <next type="notmatch">
            <out>P7</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <out>P6</out>
    </chain>
    <chain>
        <in>P5</in>
        <fid>F3</fid>
        <out>O3</out>
        <next type="notmatch">
            <out>O6</out>
        </next>
    </chain>
</run>
```
