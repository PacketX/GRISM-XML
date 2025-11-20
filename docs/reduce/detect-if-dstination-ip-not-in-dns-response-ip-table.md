# Detect If Dstination IP NOT in DNS Response IP Table

```
P0 → !F1, F2 → 0
```

```xml
<run>  
    <filter id="1" sessionBase="no" alt="dstip bypass">
        <or>
            <!-- DNS Server -->
            <find name="ip.dst" relation="==" content="8.8.8.8"/>
            <!-- Reversed -->
            <find name="ip.dst" relation="==" content="224.0.0.0/4"/>
            <find name="ip.dst" relation="==" content="255.255.255.255"/>
            <!-- Private -->
            <find name="ip.dst" relation="==" content="10.0.0.0/8"/>
            <find name="ip.dst" relation="==" content="172.16.0.0/12"/>
            <find name="ip.dst" relation="==" content="192.168.0.0/16"/>
        </or>
    </filter>
    <filter id="2" sessionBase="yes" matchedlog="yes">
        <and>
            <find name="ip" relation="==" content=""/>
            <find name="dstip.in.dns.response.ip.table" relation="!=" content=""/>
        </and>
    </filter>
    <chain>
        <in>P0</in>
        <!-- if NOT filter 1 and filter 2, drop it (output to 0) -->
        <fid type="and">!F1,F2</fid>
        <out>0</out>
    </chain>
</run>
```
