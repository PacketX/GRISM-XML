## 描述
4 Ports Bypass Switch service chain, P6,P7 has hardware bypass function
* P6(LAN)
* P7(WAN)
* P4,P5(IPS device)


## Bypass Switch service chain
```xml
<run>
  <chain>
    <in>P6</in>
    <out>P4</out>
  </chain>
  <chain>
    <in>P7</in>
    <out>P5</out>
  </chain>
  <chain>
    <in>P4</in>
    <out>P6</out>
  </chain>
  <chain>
    <in>P5</in>
    <out>P7</out>
  </chain>
</run>
```

## Bypass Switch service chain (with heartbeat)
assume heartbeat packet has been set sending from P4, and will be come back from P5
```xml
<run>
  <filter id="1" sessionBase="no">
    <or>
      <find name="heartbeat.target.miss.nth" relation="==" content="1" />
    </or>
  </filter>
  <chain>
    <in>P6</in>
    <fid>F1</fid>
    <out>P7</out>
    <next type="notmatch">
      <out>P4</out>
    </next>
  </chain>
  <chain>
    <in>P7</in>
    <fid>F1</fid>
    <out>P6</out>
    <next type="notmatch">
      <out>P5</out>
    </next>
  </chain>
  <chain>
    <in>P4</in>
    <out>P6</out>
  </chain>
  <chain>
    <in>P5</in>
  <out>P7</out>
  </chain>
</run>
```

