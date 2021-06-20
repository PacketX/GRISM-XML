## Service Chain with SSLi and IPS

```
                         WAN
                          |
                          |P7 
                    ---------------         ----------
                   |               | P1----|          |
  ---------        |               |       |          |
 |         |----P5 |               | P3----|          |
 |   IPS   |       |     GRISM     |       |   SSLi   |
 |         |----P4 |               | P2----|          |
  ---------        |               |       |          |
                   |               | P0----|          |
                    ---------------         ----------
                           |P6
                           |
                          LAN
```                            
```xml
<run>
    <filter id="1" sessionBase="no">
        <or>
            <find name="tcp.port" relation="==" content="443"/>
            <find name="udp.port" relation="==" content="53"/>
        </or>
    </filter>
    <filter id="2" sessionBase="no">
        <or>
            <find name="tcp.port" relation="==" content="443"/>
            <find name="tcp.port" relation="==" content="20443"/>
            <find name="udp.port" relation="==" content="53"/>
        </or>
    </filter>
    <filter id="3" sessionBase="no">
        <or>
            <find name="ip.addr" relation="==" content="10.110.185.0/24"/>
        </or>
    </filter>
    <chain>
        <in>P6</in>
        <fid type="and">F1,F3</fid>
        <out>P0</out>
        <next type="notmatch">
            <out>P4</out>
        </next>
    </chain>
    <chain>
        <in>P7</in>
        <fid type="and">F1,F3</fid>
        <out>P1</out>
        <next type="notmatch">
            <out>P5</out>
        </next>
    </chain>
    <chain>
        <in>P4</in>
        <fid type="and">F2,F3</fid>
        <out>P2</out>
        <next type="notmatch">
            <out>P6</out>
        </next>
    </chain>
    <chain>
        <in>P5</in>
        <fid type="and">F2,F3</fid>
        <out>P3</out>
        <next type="notmatch">
            <out>P7</out>
        </next>
    </chain>
    <chain>
        <in>P0</in>
        <out>P6</out>
    </chain>
    <chain>
        <in>P1</in>
        <out>P7</out>
    </chain>
    <chain>
        <in>P2</in>
        <out>P4</out>
    </chain>
    <chain>
        <in>P3</in>
        <out>P5</out>
    </chain>
</run>
```

## Service Chain with Two SSLi(with heartbeat bypass) and IPS
```
                         WAN
                          |
                          |P7 
                    ---------------         ----------
                   |               | P1----|          |
  ---------        |               |       |  SSLi    |
 |         |----P5 |               | P3----|          |
 |   IPS   |       |     GRISM     |        ----------
 |         |----P4 |               |        ----------
  ---------        |               | P2----|          |
                   |               |       |  SSLi    |
                   |               | P0----|          |
                    ---------------         ----------
                           |P6
                           |
                          LAN
```                            
```xml
<run>
	<filter id="1" sessionBase="no">
		<or>
			<find name="tcp.port" relation="==" content="443"/>
			<find name="udp.port" relation="==" content="53"/>
		</or>
	</filter>
	<filter id="2" sessionBase="no">
		<or>
			<find name="tcp.port" relation="==" content="443"/>
			<find name="tcp.port" relation="==" content="20443"/>
			<find name="udp.port" relation="==" content="53"/>
		</or>
	</filter>
	<filter id="3" sessionBase="no">
		<or>
			<find name="ip.addr" relation="==" content="10.110.185.0/24"/>
		</or>
	</filter>
	<filter id="100" sessionBase="no">
		<or>
			<find name="heartbeat.target.miss.nth" relation="==" content="0"/>
			<find name="heartbeat.target.miss.nth" relation="==" content="1"/>
		</or>
	</filter>
	<chain>
		<in>P6</in>
		<fid>F100</fid>
		<out>P4</out>
		<next type="notmatch">
			<fid type="and">F1,F3</fid>
			<out>P0</out>
			<next type="notmatch">
				<out>P4</out>
			</next>
		</next>
	</chain>
	<chain>
		<in>P7</in>
		<fid>F100</fid>
		<out>P5</out>
		<next type="notmatch">
			<fid type="and">F1,F3</fid>
			<out>P1</out>
			<next type="notmatch">
				<out>P5</out>
			</next>
		</next>
	</chain>
	<chain>
		<in>P4</in>
		<fid>F100</fid>
		<out>P6</out>
		<next type="notmatch">
			<fid type="and">F2,F3</fid>
			<out>P2</out>
			<next type="notmatch">
				<out>P6</out>
			</next>
		</next>
	</chain>
	<chain>
		<in>P5</in>
		<fid>F100</fid>
		<out>P7</out>
		<next type="notmatch">
			<fid type="and">F2,F3</fid>
			<out>P3</out>
			<next type="notmatch">
				<out>P7</out>
			</next>
		</next>
	</chain>
	<chain>
		<in>P0</in>
		<out>P6</out>
	</chain>
	<chain>
		<in>P1</in>
		<out>P7</out>
	</chain>
	<chain>
		<in>P2</in>
		<out>P4</out>
	</chain>
	<chain>
		<in>P3</in>
		<out>P5</out>
	</chain>
</run>
```
