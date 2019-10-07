# Element - find
Defines the find. 
It has a start tag &lt;find&gt;

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | |
| name | refer to wireshark filter function, but less item | String | * |
| relation | Equal or Not equal | ==/!= | * |
| content | content of name, could be empty | String | * |

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
| tunnel.outerlayer.ip.dsfield | | | |
| tunnel.innerlayer1.ip.dsfield | | | |
| tunnel.innerlayer2.ip.dsfield | | | |
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
| 5-tuple | 5 Tuple, - means don't care | Source IP Address, Destination IP Address, Source Port, Destination Port, Protocol | - 192.168.1.203 - 443 - |
| gtp.cp | | | |
| gtp.data | | | |
| gtp.imsi | | | |
| gtp.imsi.teid_data | | | |
| gtp.teid | | | |
| gre | | is GRE | gre == |
| erspan.spanid | | ERSPAN id | erspan.spanid == 1|
| voip | | is SIP or RTP | voip == |
| voip.account | | | voip.account == 212@o.gentrice.net |
| voip.from | | | voip.from == 212@o.gentrice.net |
| voip.to | | | voip.to == 212@o.gentrice.net |
| dns.a | IPv4 address | DNS type A ip addresses  | dns.a == 216.239.32.10 |
| dns.flags.response | 0 or 1 | DNS Response | dns.flags.response == 1 |
| dns.qry.name | Character string | DNS query name | dns.qry.name == google.com |
| http | | is HTTP | http == |
| http.request | | is HTTP request | http.request == |
| http.request.method | GET,HEAD,POST,etc.| HTTP request method | http.request.method == GET |
| http.request.url | url | HTTP request url | http.request.url == www.whitehollowtransport.com/current-elliott-c-89.html  |
| ssl | | is SSL | ssl == |
| ssl.handshake.type | 0 or 1 | SSL handshake type | ssl.handshake.type == 1 |
| quic.tag | CHLO | QUIC tag | quic.tag == CHLO |
| regex | | Regular Expression | regex == \{s\}\\\/\.\*Host: nlpqflkbvkdde\.eu |
| grism.srcport | | | |
| session.packet.nth | | | |
| heartbeat.target.miss.nth | | | |
| flowtable.matched.fid | | | |
| flowtable.inport | | which port flow comes | flowtable.inport == P0 |

## Example
```xml
<find id="1" name="ip.addr" relation="==" content="8.8.8.8" />
```


