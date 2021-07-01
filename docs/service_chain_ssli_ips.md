## Service Chain with SSLi(Array) and IPS, with heatbeat enabled(setting on GRISM Web Console->Configuration->Heatbeat)
```
                         WAN
                          |
                          |P7 
                    ---------------         ----------
                   |               | P1----|          |
  ---------        |               |       |   Array  |
 |         |----P5 |               | P3----|          |
 |   IPS   |       |     GRISM     |        ----------
 |         |----P4 |               |        ----------
  ---------        |               | P2----|          |
                   |               |       |   Array  |
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
	<filter id="101" sessionBase="no">
		<or>
			<find name="heartbeat.target.miss.nth" relation="==" content="2"/>
		</or>
	</filter>
	<chain>
		<in>P6</in>
		<fid>F101</fid>
		<out>P7</out>
		<next type="notmatch">
			<fid>F100</fid>
			<out>P4</out>
			<next type="notmatch">
				<fid type="and">F1,F3</fid>
				<out>P0</out>
				<next type="notmatch">
					<out>P4</out>
				</next>
			</next>
		</next>
	</chain>
	<chain>
		<in>P7</in>
		<fid>F101</fid>
		<out>P6</out>
		<next type="notmatch">
			<fid>F100</fid>
			<out>P5</out>
			<next type="notmatch">
				<fid type="and">F1,F3</fid>
				<out>P1</out>
				<next type="notmatch">
					<out>P5</out>
				</next>
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

## Service Chain with SSLi(A10) and IPS, with heatbeat enabled(setting on GRISM Web Console->Configuration->Heatbeat)
```
                         WAN
                          |
                          |P7 
                    ---------------         ----------
                   |               | P1----|          |
  ---------        |               |       |    A10   |
 |         |----P5 |               | P3----|          |
 |   IPS   |       |     GRISM     |        ----------
 |         |----P4 |               |        ----------
  ---------        |               | P2----|          |
                   |               |       |    A10   |
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
		</or>
	</filter>
	<filter id="2" sessionBase="no">
		<or>
			<find name="tcp.port" relation="==" content="443"/>
			<find name="tcp.port" relation="==" content="8080"/>
		</or>
	</filter>
	<filter id="3" sessionBase="no">
		<or>
			<find name="ip.addr" relation="==" content="192.168.1.0/24"/>
		</or>
	</filter>
	<filter id="99" sessionBase="no">
		<or>
			<find name="ip.proto" relation="==" content="1"/>
			<find name="arp" relation="==" content=""/>
		</or>
	</filter>
	<filter id="100" sessionBase="no">
		<or>
			<find name="heartbeat.target.miss.nth" relation="==" content="0"/>
			<find name="heartbeat.target.miss.nth" relation="==" content="1"/>
		</or>
	</filter>
	<filter id="101" sessionBase="no">
		<or>
			<find name="heartbeat.target.miss.nth" relation="==" content="2"/>
		</or>
	</filter>
	<chain>
		<in>P6</in>
		<fid>F101</fid>
		<out>P7</out>
		<next type="notmatch">
			<fid>F100</fid>
			<out>P4</out>
			<next type="notmatch">
				<fid type="and">F1,F3</fid>
				<out>P0</out>
				<next type="notmatch">
					<out>P4</out>
				</next>
			</next>
		</next>
	</chain>
	<chain>
		<in>P7</in>
		<fid>F101</fid>
		<out>P6</out>
		<next type="notmatch">
			<fid>F100</fid>
			<out>P5</out>
			<next type="notmatch">
				<fid type="and">F1,F3</fid>
				<out>P1</out>
				<next type="notmatch">
					<out>P5</out>
				</next>
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
	<!-- dup icmp and arp for A10 heartbeat check-->
	<chain>
		<in>P4</in>
		<fid>F99</fid>
		<out>P2</out>
	</chain>
	<chain>
		<in>P5</in>
		<fid>F99</fid>
		<out>P3</out>
	</chain>
	<chain>
		<in>P6</in>
		<fid>F99</fid>
		<out>P0</out>
	</chain>
	<chain>
		<in>P7</in>
		<fid>F99</fid>
		<out>P1</out>
	</chain>
</run>
```
