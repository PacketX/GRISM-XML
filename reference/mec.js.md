# mec.js

### Example

```xml
<run>
    <script src="common.js"></script>
    <script src="mec.js">
    mec('P6', 'P7', 'P5', ['10.45.13.0/24','10.45.14.0/24'], '10.45.13.100');
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
 2024/1/3   add UE to UE setup

 nb_port   : eNB/gNB Port, ex. P6
 core_port : Core Port, ex. P7
 bo_port   : Breakout Port, ex. P5
 bo_ue_ip  : Breakout UE IP range, ex. 10.45.16.0/24 or [10.45.16.0/24, 10.45.17.0/24]
 bo_gateway: Breakout Gateway, ex. 10.45.16.100
 bo_ta_ip  : Breakout Target IP range, ex. 192.168.1.0/24 (optional)
 ue2ue     : UE to UE, default false (optional)
*/
function mec(nb_port, core_port, bo_port, bo_ue_ip, bo_gateway, bo_ta_ip = '', ue2ue = false) {
    print('<filter id="1" sessionBase="no"><or>');
    if (Array.isArray(bo_ue_ip)) {
        bo_ue_ip.forEach(item => print('<find name="ip.src" relation="==" content="' + item + '"/>'));
    } else {
        print('<find name="ip.src" relation="==" content="' + bo_ue_ip + '"/>');
    }
    print('</or></filter>');
    print('<filter id="2" sessionBase="no"><or>');
    if (Array.isArray(bo_ue_ip)) {
        bo_ue_ip.forEach(item => print('<find name="arp.request.target.ip" relation="==" content="' + item + '"/>'));
    } else {
        print('<find name="arp.request.target.ip" relation="==" content="' + bo_ue_ip + '"/>');
    }
    print('</or></filter>');
    print('<filter id="3" sessionBase="no"><or>');
    if (bo_ta_ip.length > 0) {
        print('<find name="ip.dst" relation ="==" content="' + bo_ta_ip + '"/>');
    }
    print('</or></filter>');
    print('<filter id="4" sessionBase="no"><or>');
    if (Array.isArray(bo_ue_ip)) {
        bo_ue_ip.forEach(item => print('<find name="ip.dst" relation="==" content="' + item + '"/>'));
    } else {
        print('<find name="ip.dst" relation="==" content="' + bo_ue_ip + '"/>');
    }
    print('</or></filter>');
    print('<filter id="5" sessionBase="no"><or>' +
        '<find name="arp.request.target.ip" relation="!=" content="' + bo_gateway + '"/>' +
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
    if (ue2ue) {
        print('<output id="4">' +
            '<port>' + nb_port + '</port>' +
            '<stripping>gtp</stripping>' +
            '<tagging>gtp2</tagging>' +
            '</output>');
    }
    port_mirror(core_port, nb_port);
    if (ue2ue) {
        port_chain(nb_port, port_chain_next('O4', 'F1,F4', 'O1', 'and'), 'F1,F3', core_port, 'and');
    } else {
        port_chain(nb_port, 'O1', 'F1,F3', core_port, 'and');
    }
    port_chain(bo_port, 'O3', 'F2,F5', port_chain_next('O2', 'F4'), 'and');
}

/*
 nb_port    : eNB/gNB Port, ex. P6
 core_port  : Core Port, ex. P7
 bo_port    : Breakout Port, ex. P5
 bo_ue_ip   : Breakout UE IP range, ex. 10.45.16.0/24 or [10.45.16.0/24, 10.45.17.0/24]
 bo_nat_ip  : Breakout NAT IP, ex. 192.168.1.2
 bo_gateway : Breakout Gateway, ex. 192.168.1.1 (optional)
 bo_ta_ip   : Breakout Target IP range, default '', ex. 192.168.1.0/24 (optional)
 ue2ue      : UE to UE, default false (optional)
*/
function mec_with_nat(nb_port, core_port, bo_port, bo_ue_ip, bo_nat_ip, bo_gateway = '', bo_ta_ip = '', ue2ue = false) {
    print('<action>' +
        '<port>' + bo_port + '</port>' +
        '<ip>' + bo_nat_ip + '</ip>' +
        '<arp_reply_default_mac/>' +
        '<icmp_reply/></action>');
    print('<filter id="1" sessionBase="no"><or>');
    if (Array.isArray(bo_ue_ip)) {
        bo_ue_ip.forEach(item => print('<find name="ip.src" relation="==" content="' + item + '"/>'));
    } else {
        print('<find name="ip.src" relation="==" content="' + bo_ue_ip + '"/>');
    }
    print('</or></filter>');
    print('<filter id="3" sessionBase="no"><or>');
    if (bo_ta_ip.length > 0) {
        print('<find name="ip.dst" relation ="==" content="' + bo_ta_ip + '"/>');
    }
    print('</or></filter>');
    print('<filter id="4" sessionBase="no"><or>');
    if (Array.isArray(bo_ue_ip)) {
        bo_ue_ip.forEach(item => print('<find name="ip.dst" relation="==" content="' + item + '"/>'));
    } else {
        print('<find name="ip.dst" relation="==" content="' + bo_ue_ip + '"/>');
    }
    print('</or></filter>');
    print('<filter id="5" sessionBase="no"><or>' +
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
        '</output>');
    if (ue2ue) {
        print('<output id="4">' +
            '<port>' + nb_port + '</port>' +
            '<stripping>gtp</stripping>' +
            '<tagging>gtp2</tagging>' +
            '</output>');
    }
    port_mirror(core_port, nb_port);
    if (ue2ue) {
        port_chain(nb_port, port_chain_next('O4', 'F1,F4', 'O1', 'and'), 'F1,F3', core_port, 'and');
    } else {
        port_chain(nb_port, 'O1', 'F1,F3', core_port, 'and');
    }
    port_chain(bo_port, 'O2', 'F5');
}
```
