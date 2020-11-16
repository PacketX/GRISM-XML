## 描述:
inline P6<->P7 block HTTP url and HTTPS server name

## example (with regex)
```xml
<run>
	<filter id="1" sessionBase="no">
		<or>
			<find name="ssl.handshake.type" relation="==" content="0" />
			<find name="ssl.handshake.type" relation="==" content="1" />
			<find name="quic.tag" relation="==" content="CHLO" />
		</or>
	</filter>
	<filter id="2" sessionBase="no">
		<or>
			<find name="regex" relation="==" content="{s}googlevideo\.com"/>
		</or>
	</filter>
	<filter id="3" sessionBase="no">
		<or>
			<find name="http.request.url" relation="==" content="yahoo.com/index.html"/>
		</or>
	</filter>
	<chain>
		<in>P6</in>
		<fid type="and">F1,F2</fid>
		<out>0</out>
		<next type="notmatch">
			<fid>F3</fid>
			<out>0</out>
			<next type="notmatch">
				<out>P7</out>
			</next>
		</next>
	</chain>
	<chain>
		<in>P7</in>
		<fid type="and">F1,F2</fid>
		<out>0</out>
		<next type="notmatch">
			<fid>F3</fid>
			<out>0</out>
			<next type="notmatch">
				<out>P6</out>
			</next>
		</next>
	</chain>
</run>
```

## example (replace regex by ssl.server_name, support after version 20201103)
```xml
<run>
	<filter id="1" sessionBase="no">
		<or>
			<find name="ssl.server_name" relation="==" content="googlevideo.com"/>
		</or>
	</filter>
	<filter id="2" sessionBase="no">
		<or>
			<find name="http.request.url" relation="==" content="yahoo.com/index.html"/>
		</or>
	</filter>
	<chain>
		<in>P6</in>
		<fid type="or">F1,F2</fid>
		<out>0</out>
		<next type="notmatch">
			<out>P7</out>
		</next>
	</chain>
	<chain>
		<in>P7</in>
		<fid type="or">F1,F2</fid>
		<out>0</out>
		<next type="notmatch">
			<out>P6</out>
		</next>
	</chain>
</run>
```
