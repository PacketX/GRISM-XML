## 描述:
inline loadbalance (default fail-over)

## xml
```xml
<run>
    <chain id="1">
        <in>P0</in>
        <out type="loadBalance" lbtype="5thash">P1,P2</out>
    </chain>
    <chain id="2">
        <in>P1,P2</in>
        <out>P0</out>
    </chain>
</run>
```
