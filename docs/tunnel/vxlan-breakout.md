---
description: concat all network of the world with VXLAN tunnel
---

# VXLAN Breakout

```
                                     
                                            ---------------
                                           | VXLAN(source) |    ---------
                    -------------       ---| 192.168.2.100 |---|L2 Switch|--- user
    ---------      |             |     |    ---------------     ---------
   |L2 Switch|---P0|    GRISM    |P1---|    
    ---------      | VXLAN(dest) |     |    
        |          | 192.168.2.1 |     |    ---------------     ---------
                   | :4789       |      ---| VXLAN(source) |---|L2 Switch|--- user
       user         -------------      |   | 192.168.2.101 |    ---------
                                       |    ---------------
                                       |
                                        ---... more   
```

## Config XML

```xml
<configSet reboot="no">
    <args>
        <vxlanCorrelation>True</vxlanCorrelation>
        <vxlanCorrelationPort>P1</vxlanCorrelationPort>   
    </args>
    <filters>
        <in-tunnels>     
            <VXLAN>True</VXLAN>
        </in-tunnels>
    </filters>
</configSet>
```

## GRISM XML

```xml
<run>
    <action>
        <port>P1</port>
        <ip>192.168.2.1</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
    </action>
    <output id="2">
        <port>P0</port>
        <stripping>vxlan</stripping>
    </output>
    <output id="3">
        <port>P1</port>
        <tagging>vxlan</tagging>
    </output>
    <chain>
        <in>P1</in>
        <out>O2</out>
    </chain>
    <chain>
        <in>P0</in>
        <out>O3</out>
    </chain>
</run>
```

## GRISM XML add source to source

```xml
<run>
    <filter id="2" sessionBase="no">
        <or>
            <find name="dstmac.in.vxlan.mapping.table" relation="==" content=""/>
        </or>
    </filter>
    <filter id="3" sessionBase="no">
        <or>
            <find name="arp" relation="==" content=""/>
        </or>
    </filter>
    <action>
        <port>P1</port>
        <ip>192.168.2.1</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
    </action>
    <output id="2">
        <port>P0</port>
        <stripping>vxlan</stripping>
    </output>
    <output id="3">
        <port>P1</port>
        <tagging>vxlan</tagging>
    </output>
    <output id="4">
        <port>P1</port>
        <stripping>vxlan</stripping>
        <tagging>vxlan</tagging>
    </output>
    <chain>
        <in>P1</in>
        <fid>F2</fid>
        <out>O4</out>
        <next type="notmatch">
            <fid>F3</fid>
            <out>O4,O2</out>
            <next type="notmatch">
                <out>O2</out>
            </next>
        </next>
    </chain>
    <chain>
        <in>P0</in>
        <out>O3</out>
    </chain>
</run>
```
