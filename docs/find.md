# Element - find (f)
Defines the find. 
It has a start tag &lt;find&gt; or &lt;f&gt;

## Attribute
| Attribute | Alternative | Description | Type | Default (* must have) |
|---|---|---|---|---|
| id | | Specifies a unique id for an element | Interger | |
| name | n | refer to wireshark filter function, but less item | String | * |
| relation | r | Equal or Not equal | ==/!= | * |
| content | c | content of name, could be empty | String | * |

### Attribute -name
| name | type| Description | Example | 
|---|---|---|---|
| eth.addr | MAC address | Source or Destination MAC address | eth.addr == 12\:34\:56\:78\:9a\:bc |
| eth.src | MAC address | Source MAC address | eth.src == 12\:34\:56\:78\:9a\:bc |
| eth.dst | MAC address | Destination MAC address | eth.dst == 12\:34\:56\:78\:9a\:bc |
| eth.type | Unsigned integer, 2 bytes | EtherType | eth.type == 2048 (IPv4 0x0800) |
| vlan.id | Unsigned integer, 2 bytes | vlan id | vlan.id == 5 |
| vlan.l2.id | Unsigned integer, 2 bytes | vlan layer 2 id | vlan.l2.id == 1 |
| vlan.priority | Unsigned integer, 2 bytes | Priority | vlan.priority == 5 |
| ip | | is IPv4 | ip == |
| ip.addr | IPv4 address | Source or Destination Address | ip.addr == 8.8.8.8 |
| ip.src | IPv4 address | Source Address | ip.src == 8.8.8.8 |
| ip.dst | IPv4 address | Destination Address | ip.dst == 8.8.8.8 |
| ip.proto | Unsigned integer, 1 byte | Protocol | ip.proto == 6 (TCP) |
| ip.fragment | | is IPv4 Fragment | ip.fragment == |
| ip.dsfield | Unsigned integer, 1 byte | Differentiated Services Field | ip.dsfield == 1 |
| ipv6 | | is IPv6 | ipv6 == |
| ipv6.addr | IPv6 address | Source or Destination Address | ipv6.addr == 2001\:0db8\:86a3\:08d3\:1319\:8a2e\:0370\:7344 |
| ipv6.src | IPv6 address | Source Address | ipv6.src == 2001\:0db8\:86a3\:08d3\:1319\:8a2e\:0370\:7344 |
| ipv6.dst | IPv6 address | Destination Address | ipv6.dst == 2001\:0db8\:86a3\:08d3\:1319\:8a2e\:0370\:7344 |
| ipv6.nxt | Unsigned integer, 1 byte | Next Header | |
| tcp | | is TCP | tcp == |
| tcp.port | Unsigned integer, 2 bytes | Source or Destination Port | tcp.port == 443 |
| tcp.srcport | Unsigned integer, 2 bytes | Source Port | tcp.srcport == 443 |
| tcp.dstport | Unsigned integer, 2 bytes | Destination Port | tcp.dstport == 443 |
| tcp.flags.syn | 0 or 1 | Syn | tcp.flags.syn == 1 |
| tcp.flags.ack | 0 or 1 | Ack | tcp.flags.ack == 1 |
| tcp.flags.fin | 0 or 1 | Fin | tcp.flags.fin == 1 |
| tcp.flags.reset | 0 or 1 | Reset | tcp.flags.rst == 1 |
| udp | | is UDP | udp == |
| udp.port | Unsigned integer, 2 bytes | Source or Destination Port | udp.port == 53 |
| udp.srcport | Unsigned integer, 2 bytes | Source Port | udp.srcport == 53 |
| udp.dstport | Unsigned integer, 2 bytes | Destination Port | udp.dstport == 53 |
| sctp | | is SCTP | sctp == |
| sctp.port | Unsigned integer, 2 bytes | Source or Destination Port | sctp.port == 2906 |
| sctp.srcport | Unsigned integer, 2 bytes | Source Port | sctp.srcport == 2906 |
| sctp.dstport | Unsigned integer, 2 bytes | Destination Port | sctp.dstport == 2906 |
| 5-tuple | 5 Tuple, - means don't care | Source IP Address, Destination IP Address, Protocol, Source Port, Destination Port | 5-tuple == - 192.168.1.203 - - 443 |
| gtp.cp | | | |
| gtp.data | | | |
| gtp.imsi | | | |
| gtp.teid | | | |
| ip.addr.related.gtp.imsi | | | ip.addr.related.gtp.imsi == 466100000001007 |
| gre | | is GRE | gre == |
| erspan.spanid | | ERSPAN id | erspan.spanid == 1|
| voip | | is SIP or RTP | voip == |
| voip.account | | | voip.account == 212@o.gentrice.net |
| voip.from | | | voip.from == 212@o.gentrice.net |
| voip.to | | | voip.to == 212@o.gentrice.net |
| dns.a | IPv4 address | DNS type A ip addresses  | dns.a == 216.239.32.10 |
| dns.flags.response | 0 or 1 | DNS Response | dns.flags.response == 1 |
| dns.count.add_rr | int | DNS additional records count | dns.count.add_rr == 1 |
| dns.qry.type | int | DNS query type | dns.qry.type == 1 |
| dns.qry.name | Character string | DNS query name | dns.qry.name == google.com |
| dns.qry.name_public_suffix | Character string | DNS query name public suffix | dns.qry.name_public_suffix == *.googlevideo.com |
| dns.qry.name.resp.ip.addr | Character string | DNS query name response ip addr | dns.qry.name.resp.ip.addr == googlevideo.com |
| http | | is HTTP | http == |
| http.request | | is HTTP request | http.request == |
| http.request.method | GET,HEAD,POST,etc.| HTTP request method | http.request.method == GET |
| http.request.url | url | HTTP request url | http.request.url == www.whitehollowtransport.com/current-elliott-c-89.html  |
| ssl | | is SSL | ssl == |
| ssl.server_name | Character string | SSL server_name | ssl.server_name == facebook.com |
| ssl.server_name_public_suffix | Character string | SSL server_name public suffix | ssl.server_name_public_suffix == *.googlevideo.com |
| ssl.handshake.type | 0 or 1 | SSL handshake type | ssl.handshake.type == 1 |
| ssl.ja3_digest | | SSL ja3 digest | ssl.ja3_digest == 39e62db039deed96a9daf75dacdbd207 |
| quic.tag | CHLO | QUIC tag | quic.tag == CHLO |
| arp | | is ARP | arp ==  |
| arp.request | | is ARP request | arp.request ==  |
| arp.reply | | is ARP reply | arp.reply ==  |
| arp.request.target.ip | IPv4 address | ARP target ip Address | arp.request.target.ip == 192.168.1.10 |
| ftp | | is FTP | ftp ==  |
| regex | | Regular Expression | regex == \{s\}\\\/\.\*Host: nlpqflkbvkdde\.eu |
| grism.srcport | | packet comes from which port | grism.srcport == P0 |
| grism.port.linkdown | | grism port link down | grism.port.linkdown == P0 |
| session.packet.nth | | the nth packet in flow | session.packet.nth == 3 |
| heartbeat.target.miss.nth | | heartbeat missed from nth target setting | heartbeat.target.miss.nth == 1 |
| heartbeat.target.miss.id | int | heartbeat missed from target id (recommend) | heartbeat.target.miss.id == 5 |
| flowtable.matched.fid | | flow matched which filter id | flowtable.matched.fid == F1 |
| flowtable.inport | | flow comes from which port | flowtable.inport == P0 |
| 1 | Unsigned integer, 4 byte | true or false | 1 != 1 |

## Example
```xml
<filter id="1">
  <or>
    <find id="1" name="ip.addr" relation="==" content="8.8.8.8" />
    <find id="2" name="ip.addr" relation="==" content="2.2.2.2" />
  </or>
</filter>
```
Or
```xml
<filter id="1">
  <or>
    <f n="ip.addr" r="==" c="8.8.8.8" />
    <f n="ip.addr" r="==" c="2.2.2.2" />
  </or>
</filter>
```


