# Element - chain
Defines the chain. 
It has a start tag &lt;chain&gt; and an end tag &lt;/chain&gt;.

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| name | Specifies a name for an element | String | |
| sessionUnique | one session one output | yes/no | no |
| disable | disable chain  | yes/no | no |

## Example
```xml
<chain id="1">
  <in>P0</in>
  <fid>F1</fid>
  <out>P1</out>
</chain>
```


