# VXLAN Encapsulation

<img src="../../.gitbook/assets/file.excalidraw (2) (1).svg" alt="VXLAN Encapsulation for inline" class="gitbook-drawing">

## Config XML

```xml
<configSet reboot="no">
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
        <port>P7</port>
        <ip>192.168.1.155</ip>
        <arp_reply_default_mac/>
        <icmp_reply/>
    </action>
    <filter id="3" sessionBase="no">
        <or>
            <find name="vxlan.vni" relation="==" content="1234"/>
        </or>
    </filter>
    <output id="1" arp_dstip_mac="yes">
        <port>P7</port>
        <vxlan_sip>192.168.1.155</vxlan_sip>
        <vxlan_dip>192.168.1.12</vxlan_dip>
        <vxlan_sport>4789</vxlan_sport>
        <vxlan_dport>4789</vxlan_dport>
        <vxlan_vni>1234</vxlan_vni>
    </output>
    <output id="2">
        <port>P6</port>
        <stripping>vxlan</stripping>
    </output>
    <chain>
        <in>P6</in>
        <out>O1</out>
    </chain>
    <chain>
        <in>P7</in>
        <fid>F3</fid>
        <out>O2</out>
    </chain>
</run>
```
