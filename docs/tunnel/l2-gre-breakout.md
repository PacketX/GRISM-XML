---
description: concat all network of the world with GRE tunnel
---

# L2 GRE Breakout

```
                                     
                                            ---------------
                                           | GRE(source)   |    ---------
                    -------------       ---| 192.168.2.100 |---|L2 Switch|--- user
    ---------      |             |     |    ---------------     ---------
   |L2 Switch|---P0|    GRISM    |P1---|    
    ---------      | GRE(dest)   |     |    ---------------     ---------
        |          | 192.168.2.1 |      ---| GRE(source)   |---|L2 Switch|--- user
       user         -------------      |   | 192.168.2.101 |    ---------
                                       |    ---------------
                                       |
                                        ---... more   
```

## Config XML

```xml
<configSet reboot="no">
    <args>
        <grel2Correlation>True</grel2Correlation>
        <grel2CorrelationPort>P1</grel2CorrelationPort>   
    </args>
    <filters>
        <in-tunnels>     
            <GRE>True</GRE>
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
    <filter id="1" sessionBase="no">
    <or>
        <find name="gre" relation="==" content=""/>
    </or>
    </filter>
    <output id="2">
        <port>P0</port>
        <stripping>gre</stripping>
    </output>
    <output id="3">
        <port>P1</port>
        <tagging>l2gre</tagging>
    </output>
    <chain>
        <in>P1</in>
        <fid>F1</fid>
        <out>O2</out>
    </chain>
    <chain>
        <in>P0</in>
        <out>O3</out>
    </chain>
</run>
```
