## 描述
Service chain with SSLi(Array) and IPS(PA)

                           WAN
                            |
                            |v102 
                     ----------------          ----------
                     |               |v106----|          |
  ---------          |               |        |          |
 |         |----v104 |               |v108----|          |
 |   PA    |         |     GRISM     |        |   SSLi   |
 |         |----v103 |               |v107----|          |
  ---------          |               |        |          |
                     |               |v105----|          |
                     |               |        |          |
                     -----------------         ----------
                             |v101
                             |
                            LAN
                            
## xml
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
        <in>V101</in>
        <fid type="and">F1,F3</fid>
        <out>V105</out>
        <next type="notmatch">
            <out>V103</out>
        </next>
    </chain>
    <chain>
        <in>V102</in>
        <fid type="and">F1,F3</fid>
        <out>V106</out>
        <next type="notmatch">
            <out>V104</out>
        </next>
    </chain>
    <chain>
        <in>V103</in>
        <fid type="and">F2,F3</fid>
        <out>V107</out>
        <next type="notmatch">
            <out>V101</out>
        </next>
    </chain>
    <chain>
        <in>V104</in>
        <fid type="and">F2,F3</fid>
        <out>V108</out>
        <next type="notmatch">
            <out>V102</out>
        </next>
    </chain>
    <chain>
        <in>V105</in>
        <out>V101</out>
    </chain>
    <chain>
        <in>V106</in>
        <out>V102</out>
    </chain>
    <chain>
        <in>V107</in>
        <out>V103</out>
    </chain>
    <chain>
        <in>V108</in>
        <out>V104</out>
    </chain>
</run>
```
