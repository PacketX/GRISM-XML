---
description: >-
  DNS spoofing to 220.134.41.144 / ::ffff:dc86:2990 if dns request name in block
  list
---

# DNS Spoofing

```xml
<run>
    <filter id="1" sessionBase="no" alt="DNS block list">
        <or>
            <find name="dns.qry.name" relation="==" content="www.abc.com"/>
            <find name="dns.qry.name" relation="==" content="www.def.com"/>
        </or>
    </filter>
    <filter id="2" sessionBase="no" alt="dns request">
        <or>
            <find name="dns.flags.response" relation="==" content="0"/>
        </or>
    </filter>
    <filter id="3" sessionBase="no" alt="dns type A and not EDNS">
        <and>
            <find name="dns.qry.type" relation="==" content="1"/>
            <find n="dns.count.add_rr" r="==" c="0" />
        </and>
    </filter>
    <filter id="4" sessionBase="no" alt="dns type AAAA and not EDNS">
        <and>
            <find name="dns.qry.type" relation="==" content="28"/>
            <find n="dns.count.add_rr" r="==" c="0" />
        </and>
    </filter>
     <output id="2">
        <port>P7</port>
        <dns_response_ipv4>220.134.41.144</dns_response_ipv4>
    </output>
    <output id="3">
        <port>P7</port>
        <dns_response_ipv6>::ffff:dc86:2990</dns_response_ipv6>
    </output>
     <chain>
        <in>P7</in>
        <fid>F1</fid>
        <next>
            <fid>F2</fid>
            <next>
                <fid>F3</fid>
                <out>O2</out>
                <next type="notmatch">
                    <fid>F4</fid>
                    <out>O3</out>
                </next>
            </next>
        </next>
        <next type="notmatch">
            <out>P6</out>
        </next>
    </chain>
    <chain>
        <in>P6</in>
        <out>P7</out>
    </chain>
</run>
```
