---
description: Network Address Translation(NAT) implement
---

# NAT

## ConfigXML

Set TCP/UDP flow inactive timeout to 15 minutes

```xml
<configSet reboot="no">
    <log>
        <netflow>
            <inactive_timeout>900</inactive_timeout>
        </netflow>
    </log>
</configSet>
```

## NAT

* inner: P6   10.10.1.1  10.10.1.0/24
* outer: P7   192.168.1.151 gateway: 192.168.1.1

```xml
<run>
    <action>
        <port>P6</port>
        <ip>10.10.1.1</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
    </action> 
    <action>
        <port>P7</port>
        <ip>192.168.1.151</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
    </action>
    <filter id="1" sessionBase="no">
        <or>
            <find name="ip.src" relation="==" content="10.10.1.0/24"/>
        </or>
    </filter>
    <filter id="2" sessionBase="no">
        <or>
            <find name="ip.dst" relation="==" content="192.168.1.151"/>
        </or>
    </filter>
    <output id="6" arp_srcip="10.10.1.1" arp_dstip_mac="yes">
        <port>P6</port>
        <modify_src_default_mac/>
        <modify_dstip2nat/>
    </output>
    <output id="7">
        <port>P7</port>
        <modify_src_default_mac/>
        <modify_srcip nat="yes">192.168.1.151</modify_srcip>
        <gateway>192.168.1.1</gateway>
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

## NAT and set mtu 1480

* inner: P6   10.10.1.1  10.10.1.0/24
* outer: P7   192.168.1.151 gateway: 192.168.1.1

```xml
<run>
    <action>
        <port>P6</port>
        <ip>10.10.1.1</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
    </action> 
    <action>
        <port>P7</port>
        <ip>192.168.1.151</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
        <icmp_reply_fragment_need mtu="1480"/>
    </action>
    <filter id="1" sessionBase="no">
        <or>
            <find name="ip.src" relation="==" content="10.10.1.0/24"/>
        </or>
    </filter>
    <filter id="2" sessionBase="no">
        <or>
            <find name="ip.dst" relation="==" content="192.168.1.151"/>
        </or>
    </filter>
    <output id="6" arp_srcip="10.10.1.1" arp_dstip_mac="yes">
        <port>P6</port>
        <modify_src_default_mac/>
        <modify_dstip2nat/>
    </output>
    <output id="7">
        <port>P7</port>
        <modify_src_default_mac/>
        <modify_srcip nat="yes">192.168.1.151</modify_srcip>
        <gateway>192.168.1.1</gateway>
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

## NAT breakout dns traffic

* inner: P6
* outer: P7
* dns breakout outer: P5 172.16.10.10  gateway: 192.16.10.1

<pre class="language-markup"><code class="lang-markup">&#x3C;run>
<strong>    &#x3C;action>
</strong>        &#x3C;port>P5&#x3C;/port>
        &#x3C;ip>172.16.10.10&#x3C;/ip>
        &#x3C;arp_reply_default_mac/>
        &#x3C;icmp_reply/>
    &#x3C;/action> 
    &#x3C;filter id="99" alt="dns query" sessionBase="no">
        &#x3C;or>
            &#x3C;find name="udp.port" relation="==" content="53"/>
        &#x3C;/or>
    &#x3C;/filter> 
    &#x3C;output id="5">
        &#x3C;port>P5&#x3C;/port>
        &#x3C;modify_src_default_mac/>
        &#x3C;modify_srcip nat="yes">172.16.10.10&#x3C;/modify_srcip>
        &#x3C;gateway>172.16.10.1&#x3C;/gateway>
    &#x3C;/output>
    &#x3C;output id="6" arp_dstip_mac="yes">
        &#x3C;port>P6&#x3C;/port>
        &#x3C;modify_src_default_mac/>
        &#x3C;modify_dstip2nat/>  
    &#x3C;/output>
    &#x3C;chain>
        &#x3C;in>P6&#x3C;/in>
        &#x3C;fid type="and">F99&#x3C;/fid>
        &#x3C;out>O5&#x3C;/out>
        &#x3C;next type="notmatch">
            &#x3C;out>P7&#x3C;/out>
        &#x3C;/next>
    &#x3C;/chain>
    &#x3C;chain>
        &#x3C;in>P7&#x3C;/in>
        &#x3C;out>P6&#x3C;/out>
    &#x3C;/chain>
    &#x3C;chain>
        &#x3C;in>P5&#x3C;/in>  
        &#x3C;out>O6&#x3C;/out>
    &#x3C;/chain>
&#x3C;/run>
</code></pre>
