# GRISM XML

## Tutorial

> GRISM XML is the standard markup language for SDN

> With GRISM XML you can define the Network with XML

> GRISM XML is easy to learn - You will enjoy it!

## Features

* Easy to learn and use, simple to edit
* User-Friendly
* Easy to integrate with third-party software
* Simple and lightweight

## Device Support

For detailed technical specifications and compatibility information, please refer to the official documentation at

* GRISM G8
* GRISM T4, GRISM T12, GRISM T20, GRISM F2T12
* GRISM G8-MEC
* GRISM T4-MEC, GRISM T12-MEC, GRISM T20-MEC
* GRISM AH32 (supports L2–L4 filtering functions only)

For detailed technical specifications and compatibility information, please refer to the official documentation at [https://packetx.biz/](https://packetx.biz/)

## Online Doc

[https://packetx.gitbook.io/grism-xml/](https://packetx.gitbook.io/grism-xml/)

## A Simple GRISM XML

Define filter id=1 aka **F1** as black IP list and descript network topology in chain. When packets come from P0, if matched F1, send to P1, else if not matched, send to P2

```xml
<run>
    <filter id="1" name="black IP list">
        <or>
            <find name="ip.addr" relation="==" content="92.53.120.155" />
            <find name="ip.addr" relation="==" content="67.229.164.135" />
            <find name="ip.addr" relation="==" content="159.203.92.222" />            
        </or>
    </filter>
    <chain>
        <in>P0</in>
        <fid>F1</fid>
        <out>P1</out>
        <next type="notmatch">
            <out>P2</out>
        </next>
    </chain>
</run>
```

## Version

5.6.240412
