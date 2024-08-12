# common.js

## Example

```xml
<script src="common.js"></script>
<script>
<![CDATA[
    port_mirror('P0', 'P1,P2');
]]>
</script>
```

## Script source

```javascript
var g_filter_start_id = 1000001;
var g_action_start_id = 1000001;
var g_output_start_id = 1000001;

function port_chain_next(match, filter = '', notmatch = '', fid_type = '') {
    var ret = '';
    if (filter.length > 0) {
        if (fid_type.length > 0) {
            ret += '<fid type="' + fid_type + '">' + filter + '</fid>\n';
        } else {
            ret += '<fid>' + filter + '</fid>\n';
        }
    }
    if (match.indexOf('<') == -1) {
        ret += '<out>' + match + '</out>\n';
    } else {
        if (match.indexOf('<out') == 0) {
            ret += match + '\n';
        } else {
            ret += '<next>\n';
            ret += match + '\n';
            ret += '</next>\n';
        }
    }
    if (notmatch.length > 0) {
        ret += '<next type="notmatch">\n';
        if (notmatch.indexOf('<') == -1) {
            ret += '<out>' + notmatch + '</out>\n';
        } else {
            ret += notmatch + '\n';
        }
        ret += '</next>\n';
    }
    return ret;
}

function port_chain(inports, match, filter = '', notmatch = '', fid_type = '') {
    print('<chain>\n    <in>' + inports + '</in>\n');
    print(port_chain_next(match, filter, notmatch, fid_type));
    print('</chain>\n');
}

function port_loadbalance(inports, outports, lbtype = '5thash') {
    port_chain(inports, '<out type="loadBalance" lbtype="' + lbtype + '">' + outports + '</out>');
}

function port_mirror(inports, outports) {
    port_chain(inports, outports);
}

function port_inline(porta, portb) {
    port_chain(porta, portb);
    port_chain(portb, porta);
}

function port_inline_tap(lantoport, wantoport, lanport, wanport) {
    port_chain(lanport, wanport + ',' + lantoport);
    port_chain(wanport, lanport + ',' + wantoport);
}

function port_inline_bypass(lantoport, wantoport, lanport, wanport) {
    var heartbeat_id = grism_heartbeat_id_get(lantoport, wantoport);
    if (heartbeat_id == -1) {
        print('<!-- [ERROR] ' + lantoport + ',' + wantoport + ' heartbeat not set yet (Configuration::Heartbeat) -->');
        return;
    }
    var heartbeat_filter_id = g_filter_start_id++;
    print('<filter id="' + heartbeat_filter_id + '" sessionBase="no"><or><find name="heartbeat.target.miss.id" relation="==" content="' + heartbeat_id + '"/></or></filter>\n');
    port_chain(lanport, wanport, 'F' + heartbeat_filter_id, lantoport);
    port_chain(wanport, lanport, 'F' + heartbeat_filter_id, wantoport);
    port_chain(lantoport, lanport);
    port_chain(wantoport, wanport);
}

function port_inline_bypass_tap(lantoport, wantoport, lanport, wanport) {
    var heartbeat_id = grism_heartbeat_id_get(lantoport, wantoport);
    if (heartbeat_id == -1) {
        print('<!-- [ERROR] ' + lantoport + ',' + wantoport + ' heartbeat not set yet (Configuration::Heartbeat) -->');
        return;
    }
    var heartbeat_filter_id = g_filter_start_id++;
    print('<filter id="' + heartbeat_filter_id + '" sessionBase="no"><or><find name="heartbeat.target.miss.id" relation="==" content="' + heartbeat_id + '"/></or></filter>\n');
    port_chain(lanport, wanport + ',' + lantoport, 'F' + heartbeat_filter_id, lantoport);
    port_chain(wanport, lanport + ',' + wantoport, 'F' + heartbeat_filter_id, wantoport);
    port_chain(lantoport, lanport, '!F' + heartbeat_filter_id);
    port_chain(wantoport, wanport, '!F' + heartbeat_filter_id);
}

function port_input_vlan_tag(port, vlan) {
    print('<action id="' + g_action_start_id + '" type="input-packet-process">\n');
    print('    <port>' + port + '</port>\n');
    print('    <Q>' + vlan + '</Q>\n');
    print('</action>\n');
    g_action_start_id++;
}

function port_input_linkpairs(porta, portb) {
    print('<action id="' + g_action_start_id + '" type="linkpairs">\n');
    print('    <portA>' + porta + '</portA>\n');
    print('    <portB>' + portb + '</portB>\n');
    print('</action>\n');
    g_action_start_id++;
}

function port_output_vlan_tag(port, vlan, id = -1) {
    if (id < 0) {
        id = g_output_start_id;
        g_output_start_id++;
    }
    print('<output id="' + id + '">\n');
    print('    <port>' + port + '</port>\n');
    print('    <Q>' + vlan + '</Q>\n');
    print('</output>\n');
    return id;
}

function port_output_vlan_stripping(port, id = -1) {
    if (id < 0) {
        id = g_output_start_id;
        g_output_start_id++;
    }
    print('<output id="' + id + '">\n');
    print('    <port>' + port + '</port>\n');
    print('    <stripping>vlan</stripping>\n');
    print('</output>\n');
    return id;
}
```
