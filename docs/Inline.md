## 描述
inline samples

## basic
```xml
<run>
    <chain>
        <in>P6</in>
        <out>P7</out>
    </chain>
    <chain>
        <in>P7</in>
        <out>P6</out>
    </chain>
</run>
```

## inline bypass 443 without first 10 packets
```
                           WAN
                            |
                            |P7 
                      --------------- 
                     |               |
  ---------          |               |
 |         |----P5   |               |
 |   IPS   |         |     GRISM     |
 |         |----P4   |               |
  ---------          |               |
                     |               |
                     |               |
                      --------------- 
                             |P6
                             |
                            LAN
```
```xml
<run>
    <filter id="1" sessionBase="no">
        <or>
            <find name="tcp.port" relation="==" content="443" />
            <find name="udp.port" relation="==" content="443" />
        </or>
    </filter>
    <filter id="2" sessionBase="no" maxPackets="10">
        <or>
            <find name="tcp.port" relation="==" content="443" />
            <find name="udp.port" relation="==" content="443" />
        </or>
    </filter>
    <chain>
        <in>P6</in>
        <fid>F1</fid>
        <next>
            <fid>F2</fid>
            <out>P4</out>
            <next type="notmatch">
                <out>P7</out>
            </next>
        </next>
        <next type="notmatch">
            <out>P4</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <fid>F1</fid>
        <next>
            <fid>F2</fid>
            <out>P5</out>
            <next type="notmatch">
                <out>P6</out>
            </next>
        </next>
        <next type="notmatch">
            <out>P5</out>
        </next>
    </chain>
</run>
```
