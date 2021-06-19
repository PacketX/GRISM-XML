## basic
```
        WAN
         |
         |P7 
  --------------- 
 |               |
 |               |
 |     GRISM     |
 |               |
 |               |
  --------------- 
         |P6
         |
        LAN
```
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
  ---------        |               |
 |         |----P5 |               |
 |   IPS   |       |     GRISM     |
 |         |----P4 |               |
  ---------        |               |
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
    <chain>
        <in>P4</in>
        <out>P6</out>
    </chain>
    <chain>
        <in>P5</in>
        <out>P7</out>
    </chain>
</run>
```
## inline bypass HTTPS Youtube
```
                         WAN
                          |
                          |P7 
                    --------------- 
  ---------        |               |
 |         |----P5 |               |
 |   IPS   |       |     GRISM     |
 |         |----P4 |               |
  ---------        |               |
                    --------------- 
                           |P6
                           |
                          LAN
```
```xml
<run>
    <filter id="5" sessionBase="yes">
        <or>
            <find name="ssl.server_name" relation="==" content="youtube.com"/>
            <find name="ssl.server_name" relation="==" content="youtu.be"/>
            <find name="ssl.server_name" relation="==" content="yt3.ggpht.com"/>
        </or>
    </filter>
    <filter id="6" sessionBase="yes">
        <or>
            <find name="ssl.server_name_public_suffix" relation="==" content="*.googlevideo.com" />
            <find name="ssl.server_name_public_suffix" relation="==" content="*.googleapis.com" />
            <find name="ssl.server_name_public_suffix" relation="==" content="*.youtube.com" />
            <find name="ssl.server_name_public_suffix" relation="==" content="*.ytimg.com" />
        </or>
    </filter>
    <filter id="7" sessionBase="yes">
        <or>
            <find name="flowtable.matched.fid" relation="==" content="F5" />
            <find name="flowtable.matched.fid" relation="==" content="F6" />
        </or>
    </filter>
    <chain>
        <in>P6</in>
        <fid>F5,F6</fid>
        <out>P7</out>
        <next type="notmatch">
            <out>P4</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <fid>F7</fid>
        <out>P6</out>
        <next type="notmatch">
            <out>P5</out>
        </next>
    </chain>
    <chain>
        <in>P4</in>
        <out>P6</out>
    </chain>
    <chain>
        <in>P5</in>
        <out>P7</out>
    </chain>
</run>
```
