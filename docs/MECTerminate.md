## 描述
4G/5G Mobile Edge Computing Termination Sample

P5: Edge
P6: Core
P7: eNB

Functions
1. keep inline connect between Core and eNB
2. filter destination IP which need to be Terminate to Edge
3. stripping GTP header before packet send to Edge
4. tagging GTP headaer when packet comes from Edge
5. reply ARP when Edge request for termination IP

## xml
```xml
<run>
    <filter id="1" sessionBase="no">
        <or>
            <find name="ip.dst" relation="==" content="10.239.0.0/24"/>
        </or>
    </filter>
    <filter id="2" sessionBase="no">
        <or>
            <find name="arp.request.target.ip" relation="==" content="10.239.0.0/24"/>
        </or>
    </filter>
    <output id="1">
        <port>P5</port>
        <stripping>gtp</stripping>
        <modify_dstmac>00:0c:29:d3:a4:56</modify_dstmac>
    </output>
    <output id="2">
        <port>P7</port>
        <tagging>gtp2</tagging>
    </output>
    <output id="3">
        <port>P5</port>
        <arp_reply_target_mac>02:01:00:00:00:00</arp_reply_target_mac>
    </output>
    <chain>
        <in>P6</in>
        <out>P7</out>
    </chain>
    <chain>
        <in>P7</in>
        <fid>F1</fid>
        <out>O1</out>
        <next type="notmatch">
            <out>P6</out>
        </next>
    </chain>
    <chain>
        <in>P5</in>
        <fid>F2</fid>
        <out>O3</out>
        <next type="notmatch">
            <out>O2</out>
        </next>
    </chain>
</run>
```

