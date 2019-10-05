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
| eth.addr | MAC address | MAC address | eth.addr == 12:34:56:78:9a:bc |
| eth.src | MAC address | source MAC address | eth.src == 12:34:56:78:9a:bc |
| eth.dst | MAC address | dest MAC address | eth.dst == 12:34:56:78:9a:bc |
| eth.type | int(DEC) | EtherType | eth.type == 2048 (ipv4 0x0800) |
| vlan.id | int(DEC) | vlan id | vlan.id == 5 |
| vlan.l2.id | | | |
| vlan.priority | | | |
| ip | | | |
| ip.addr | | | |
| ip.src | | | |
| ip.dst | | | |
| ip.proto | | | |
| ip.fragment | | | |
| ip.dsfield | | | |
| tunnel.outerlayer.ip.dsfield | | | |
| tunnel.innerlayer1.ip.dsfield | | | |
| tunnel.innerlayer2.ip.dsfield | | | |
| ipv6 | | | |
| ipv6.addr | | | |
| ipv6.src | | | |
| ipv6.dst | | | |
| ipv6.nxt | | | |
| tcp | | | |
| tcp.port | | | |
| tcp.srcport | | | |
| tcp.dstport | | | |
| tcp.flags.syn | | | |
| tcp.flags.ack | | | |
| tcp.flags.fin | | | |
| tcp.flags.reset | | | |
| udp | | | |
| udp.port | | | |
| udp.srcport | | | |
| udp.dstport | | | |
| sctp | | | |
| sctp.port | | | |
| sctp.srcport | | | |
| sctp.dstport | | | |
| 5-tuple | | | |
| gtp.cp | | | |
| gtp.data | | | |
| gtp.imsi | | | |
| gtp.imsi.teid_data | | | |
| gtp.teid | | | |
| gre | | | |
| erspan.spanid | | | |
| voip | | | |
| voip.account | | | |
| voip.from | | | |
| voip.to | | | |
| dns.a | | | |
| dns.flags.response | | | |
| dns.qry.name | | | |
| http | | | |
| http.request | | | |
| http.request.method | | | |
| ssl | | | |
| ssl.handshake.type | | | |
| quic.tag | | | |
| regex | | | |
| grism.srcport | | | |
| session.packet.nth | | | |
| heartbeat.target.miss.nth | | | |
| flowtable.matched.fid | | | |
| flowtable.inport | | flow從哪一個實體介面進來 | flowtable.inport == P0 |

## Example
```xml
<find id="1" name="ip.addr" relation="==" content="8.8.8.8" />
```


