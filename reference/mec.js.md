# mec.js

### Example

```xml
<run>
    <script src="common.js"></script>
    <script src="mec.js">
    mec('P6', 'P7', 'P5', '10.45.0.0/16', '10.45.0.100');
    </script>
</run>
```

### Example (with NAT)

```xml
<run>
    <script src="common.js"></script>
    <script src="mec.js">
    mec_with_nat('P6', 'P7', 'P5', '10.45.0.0/16', '192.168.1.2');
    </script>
</run>
```

### Script

```javascript
/*
 2023/12/28 first add

 nb_port   : eNB/gNB Port, ex. P6
 core_port : Core Port, ex. P7
 bo_port   : Breakout Port, ex. P5
 bo_ue_ip  : Breakout UE IP range, ex. 10.45.16.0/24
 bo_gateway: Breakout Gateway, ex. 10.45.16.100
 bo_ta_ip  : Breakout Target IP range, ex. 192.168.1.0/24 (optional)
*/
function mec(nb_port, core_port, bo_port, bo_ue_ip, bo_gateway, bo_ta_ip = '') {
    print('<filter id="1" sessionBase="no"><or>' +
        '<find name="ip.src" relation="==" content="' + bo_ue_ip + '"/>' +
        '</or></filter>' +
        ' <filter id="2" sessionBase="no"><and>' +
        '<find name="arp.request.target.ip" relation="==" content="' + bo_ue_ip + '"/>' +
        '<find name="arp.request.target.ip" relation="!=" content="' + bo_gateway + '"/>' +
        '</and></filter>' +
        '<filter id="3" sessionBase="no"><or>');
    if (bo_ta_ip.length > 0) {
        print('<find name="ip.dst" relation ="==" content="' + bo_ta_ip + '"/>');
    }
    print('</or></filter>' +
        '<filter id="4" sessionBase="no"><or>' +
        '<find name="ip.dst" relation="==" content="' + bo_ue_ip + '"/>' +
        '</or></filter>');
    print('<output id="1" arp_dstip_mac="yes">' +
        '<port>' + bo_port + '</port>' +
        '<gateway>' + bo_gateway + '</gateway>' +
        '<stripping>gtp</stripping>' +
        '</output>' +
        '<output id="2">' +
        '<port>' + nb_port + '</port>' +
        '<tagging>gtp2</tagging>' +
        '</output>' +
        '<output id="3">' +
        '<port>' + bo_port + '</port>' +
        '<arp_reply_default_mac/>' +
        '</output>');
    port_mirror(core_port, nb_port);
    port_chain(nb_port, 'O1', 'F1,F3', 'P7', 'and');
    port_chain(bo_port, 'O3', 'F2', port_chain_next('O2', 'F4'));
}

/*
 nb_port    : eNB/gNB Port, ex. P6
 core_port  : Core Port, ex. P7
 bo_port    : Breakout Port, ex. P5
 bo_ue_ip   : Breakout UE IP range, ex. 10.45.16.0/24
 bo_nat_ip  : Breakout NAT IP, ex. 192.168.1.2
 bo_gateway : Breakout Gateway, ex. 192.168.1.1 (optional)
 bo_ta_ip   : Breakout Target IP range, ex. 192.168.1.0/24 (optional)
*/
function mec_with_nat(nb_port, core_port, bo_port, bo_ue_ip, bo_nat_ip, bo_gateway = '', bo_ta_ip = '') {
    print('<filter id="1" sessionBase="no"><or>' +
        '<find name="ip.src" relation="==" content="' + bo_ue_ip + '"/>' +
        '</or></filter>' +
        ' <filter id="2" sessionBase="no"><or>' +
        '<find name="arp.request.target.ip" relation="==" content="' + bo_nat_ip + '"/>' +
        '</or></filter>' +
        '<filter id="3" sessionBase="no"><or>');
    if (bo_ta_ip.length > 0) {
        print('<find name="ip.dst" relation ="==" content="' + bo_ta_ip + '"/>');
    }
    print('</or></filter>' +
        '<filter id="4" sessionBase="no"><or>' +
        '<find name="ip.dst" relation="==" content="' + bo_nat_ip + '"/>' +
        '</or></filter>');
    print('<output id="1" arp_dstip_mac="yes">' +
        '<port>' + bo_port + '</port>');
    print('<modify_src_default_mac/>' +
        '<modify_srcip nat="yes">' + bo_nat_ip + '</modify_srcip>');
    if (bo_gateway.length > 0) {
        print('<gateway>' + bo_gateway + '</gateway>');
    }
    print('<stripping>gtp</stripping>' +
        '</output>' +
        '<output id="2">' +
        '<port>' + nb_port + '</port>' +
        '<modify_dstip2nat/>' +
        '<tagging>gtp2</tagging>' +
        '</output>' +
        '<output id="3">' +
        '<port>' + bo_port + '</port>' +
        '<arp_reply_default_mac/>' +
        '</output>');
    port_mirror(core_port, nb_port);
    port_chain(nb_port, 'O1', 'F1,F3', 'P7', 'and');
    port_chain(bo_port, 'O3', 'F2', port_chain_next('O2', 'F4'));
}
```
