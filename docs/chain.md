# Element - chain
Defines the chain. 
It has a start tag &lt;chain&gt; and an end tag &lt;/chain&gt;.

## Attribute
| Attribute | Description | Type | Default \(\* must have\) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | \* |
| name | Specifies a name for an element | String | |
| sessionUnique | one session one output | yes/no | no |
| disable | disable chain  | yes/no | no |

## Elements in chain
### in
Defines input ports. It has a start tag &lt;in&gt; and an end tag &lt;/in&gt;.

#### Example
```xml
<in>P0</in>

<in>P0,P1,P2</in>

<in>V0,V1</in>
```
### out
Defines output ports. It has a start tag &lt;out&gt; and an end tag &lt;/out&gt;.

#### Attribute
| Attribute | Description | Type | Default \(\* must have\) |
|---|---|---|---|
| type | duplicate or loadBalance | String | duplicate |
| lbtype | Load Balance type, includes session, ethtype, iptype, smac, dmac, sip, dip, rr, 5thash | String | session |
| failover | Load Balance fail over | yes/no | yes |
| weight | Load Balance weight \(not support session\, rr type\) | String | 20,80 |


#### Example
```xml
<out>P0</out>

<out type="loadBalance" lbtype="5thash">P0,P1,P2</out>

<out>V0,V1</out>

<out>O1,O2</out>
```

### fid
Defines packets pass through filter id. It has a start tag &lt;fid&gt; and an end tag &lt;/fid&gt;.
#### Attribute
| Attribute | Description | Type | Default \(\* must have\) |
|---|---|---|---|
| type | and/or | String | or |

#### Example
```xml
  <fid>F1</fid>

  <fid type="or">F1,F2</fid>
```
### next
Defines going next if packet match/not match filter. It has a next tag &lt;next&gt; and an end tag &lt;/next&gt;.

#### Attribute
| Attribute | Description | Type | Default \(\* must have\) |
|---|---|---|---|
| type | match/notmatch | String | match |

#### Example
```xml
  <next>
    <out>P1</out>
  </next>
 
  <next type="notmatch">
    <fid>F1</fid>
    <out>P1</out>
  </next>
```

## Example
```
P0->F1->P1        
```
```xml
<chain id="1">
  <in>P0</in>
  <fid>F1</fid>
  <out>P1</out>
</chain>
```

```
P0->F1->F2->P1
      !>P2
```
```xml
<chain id="1">
  <in>P0</in>
  <fid>F1</fid>
  <next>
    <fid>F2</fid>
    <out>P1</out> 
  </next>
  <next type="notmatch">
    <out>P2</out>
  <next>
</chain>
```

```
P0->F1->F2->P1
          !>P2
```
```xml
<chain id="1">
  <in>P0</in>
  <fid>F1</fid>
  <next>
    <fid>F2</fid>
    <out>P1</out>
    <next type="notmatch">
      <out>P2</out>
    </next>
  </next>
</chain>
```


