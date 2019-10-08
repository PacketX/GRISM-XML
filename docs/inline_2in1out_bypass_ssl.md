## 描述:
兩組inline 接兩組IPS，最基本設定，不做loadbalance也不做port tag/stripping功能

## tag簡介
* P0,P2: 第一組接Switch, P0對內P2對外
* P1,P3: 第一組接IPS
* P4,P6: 第二組接Switch, P0對內P2對外
* P5,P7: 第二組接IPS
* F1: 過濾ssl封包
* F2: 過濾封包是否屬於flow table裡面有紀錄為F1的flow

## xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<run>
    <filter id="1" name="1" sessionBase="yes">
        <or>
	    <find name="ssl.handshake.type" relation="==" content="0" />
            <find name="ssl.handshake.type" relation="==" content="1" />
            <find name="quic.tag" relation="==" content="CHLO" />
        </or>
    </filter>
    <filter id="2" sessionBase="yes">
        <or>
            <find name="flowtable.matched.fid" relation="==" content="F1" />
        </or>
    </filter>
    <chain id="1" sessionUnique="yes">
        <in>P0</in>
	<fid>F1</fid>
	<out>P2</out>
	<next type="notmatch">
	    <out>P1</out>
	</next>
    </chain>
    <chain id="2" sessionUnique="yes">
        <in>P2</in>
        <fid>F2</fid>
        <out>P0</out>
        <next type="notmatch">
            <out>P3</out>
        </next>
    </chain>
    <chain id="3">
        <in>P1</in>
        <out>P0</out>
    </chain>
    <chain id="4">
        <in>P3</in>
        <out>P2</out>
    </chain>
    <chain id="5" sessionUnique="yes">
        <in>P4</in>
	<fid>F1</fid>
	<out>P6</out>
	<next type="notmatch">
	    <out>P5</out>
	</next>
    </chain>
    <chain id="6" sessionUnique="yes">
        <in>P6</in>
        <fid>F2</fid>
        <out>P4</out>
        <next type="notmatch">
            <out>P7</out>
        </next>
    </chain>
    <chain id="7">
        <in>P5</in>
        <out>P4</out>
    </chain>
    <chain id="8">
        <in>P7</in>
        <out>P6</out>
    </chain>
</run>
```
