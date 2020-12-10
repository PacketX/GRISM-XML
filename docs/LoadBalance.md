## 描述
P0,P1 load balance to P3,P4,P5,P6 by 5-tuple (sip,dip,sport,dport,ip_proto)

## xml
```xml
<run>
    <chain>
        <in>P0,P1</in>
        <out type="loadBalance" lbtype="5thash">P3,P4,P5,P6</out>
    </chain>
</run>
```
