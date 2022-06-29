# Black List block/detect

### IP/domain/url/ssl server\_name Block/Detect Sample

### Black List

```xml
<run>
    <filter id="10000" sessionBase="yes" matchedlog="yes">
        <or>
            <find id="10000" name="ip.addr" relation="==" content="8.8.8.8"/>
        </or>
    </filter>
    <filter id="10001" sessionBase="no" matchedlog="yes">
        <or>
            <find id="10002" name="dns.qry.name" relation="==" content="www.cittv.com.tw"/>
        </or>
    </filter>
    <filter id="10002" sessionBase="no" matchedlog="yes">
        <or>
            <find id="10004" name="http.request.url" relation="==" content="www.whitehollowtransport.com/current-elliott-c-89.html" />
        </or>
    </filter>
    <filter id="10003" sessionBase="no" matchedlog="yes">
        <or>
            <find id="10005" name="ssl.server_name" relation="==" content="facebook.com" />
        </or>
    </filter>
    <filter id="10004" sessionBase="no" matchedlog="yes">
        <or>
            <find id="10006" name="ssl.server_name_public_suffix" relation="==" content=" *.googlevideo.com" />
        </or>
    </filter>
</run>
```

### Block Sample

```xml
<run>
    <chain>
        <in>P6</in>
        <fid>F10000,F10001,F10002,F10003,F10004</fid>
        <out>0</out>
        <next type=”notmatch”>
            <out>P7</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <fid>F10000,F10001,F10002,F10003,F10004</fid>
        <out>0</out>
        <next type=”notmatch”>
            <out>P6</out>
        </next>
    </chain>
</run>
```

### Detect Sample

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
    <chain>
        <in>P6,P7</in>
        <fid>F10000,F10001,F10002,F10003,F10004</fid>
        <out>0</out>
    </chain>
</run>
```
