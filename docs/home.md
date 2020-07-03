# GRISM XML

## Tutorial
> GRISM XML is the standard markup language for SDN

> With GRISM XML you can describes the structure of Network Packet Broker

> GRISM XML is easy to learn - You will enjoy it!

## Features

- Easy to learn and use, simple to edit
- User-Friendly
- Easy to integrate with third-party software
- Simple and lightweight

## A Simple GRISM XML
First define filter id=1 aka <b>F1</b> as black IP list.<br>
Second define chain, When packets come from P0, if matched F1, send to P1
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
    </chain>
</run>
```
