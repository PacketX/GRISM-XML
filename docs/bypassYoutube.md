## 描述:
bypass Youtube, include http, https and quic protocols

## xml
```xml
<run>
<filter id="5" sessionBase="no">
        <or>
            <find name="http.request" relation="==" content=""/>
            <find name="ssl.handshake.type" relation="==" content="0" />
            <find name="ssl.handshake.type" relation="==" content="1" />
            <find name="quic.tag" relation="==" content="CHLO" />
        </or>
    </filter>
<filter id="6" sessionBase="yes">
	<or>
		<!-- youtube -->
		<find name="regex" relation="==" content="{s}upload\.youtube\.com" />
		<find name="regex" relation="==" content="{s}upload\.video\.google\.com" />
		<find name="regex" relation="==" content="{s}youtubei\.googleapis\.com" />
		<find name="regex" relation="==" content="{s}youtube\." />
		<find name="regex" relation="==" content="{s}youtu\.be\." />
		<find name="regex" relation="==" content="{s}yt3\.ggpht\.com" />
		<find name="regex" relation="==" content="{s}\.googlevideo\.com" />
		<find name="regex" relation="==" content="{s}\.ytimg\.com" />
		<find name="regex" relation="==" content="{s}youtube\-nocookie\." />
	</or>
</filter>
<chain>
    <in>P0</in>
    <fid type="and">F5,F6</fid>
    <out>P8</out>
    <next type="notmatch">
        <out>P1</out>
    </next>
</chain>
</run>
```
