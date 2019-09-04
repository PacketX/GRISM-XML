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

## Example
```xml
<find id="1" name="ip.addr" relation="==" content="8.8.8.8" />
```


