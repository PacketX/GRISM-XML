## 描述:
inline loadbalance to IPS(default fail-over)

## tag簡介
* P0,P1: P0對內P1對外
* P2,P3: 接第一台IPS
* P4,P5: 接第二台IPS

## xml
```xml
<run>
    <chain id="1">
        <in>P0</in>
        <out type="loadBalance" lbtype="5thash">P2,P4</out>
    </chain>
    <chain id="2">
        <in>P1</in>
        <out type="loadBalance" lbtype="5thash">P3,P5</out>
    </chain>
    <chain id="3">
         <in>P2,P4</in>
         <out>P0</out>
    </chain>
    <chain id="4">
         <in>P3,P5</in>
         <out>P1</out>
    </chain>
</run>
```
