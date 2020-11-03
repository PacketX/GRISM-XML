## 描述:
bypass HTTPS Youtube

## xml
```xml
<run>
<filter id="5" sessionBase="yes">
        <or>
            <find name="ssl.server_name" relation="==" content="youtube.com"/>
	    <find name="ssl.server_name" relation="==" content="youtu.be"/>
	    <find name="ssl.server_name" relation="==" content="yt3.ggpht.com"/>
        </or>
    </filter>
<filter id="6" sessionBase="yes">
	<or>
		<find name="ssl.server_name_public_suffix" relation="==" content="*.googlevideo.com" />
       		<find name="ssl.server_name_public_suffix" relation="==" content="*.googleapis.com" />
		<find name="ssl.server_name_public_suffix" relation="==" content="*.youtube.com" />
		<find name="ssl.server_name_public_suffix" relation="==" content="*.ytimg.com"" />
	</or>
</filter>
<chain>
    <in>P0</in>
    <fid>F5,F6</fid>
    <out>P8</out>
    <next type="notmatch">
        <out>P1</out>
    </next>
</chain>
</run>
```
