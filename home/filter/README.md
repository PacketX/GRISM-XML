---
description: Defines the filter. It has a start tag <filter> and an end tag </filter>.
---

# Element - \<filter>

In filter, must start at \<or>\</or> or \<and>\</and>, then put \<find/> into there like

```xml
<filter id="1" >
    <or>
	<find name="tcp.port" relation="==" content="443" />
	<find name="udp.port" relation="==" content="53" />
    </or>
</filter>
```

### \<or>

Defines all finds conjunct with or. It has a start tag \<or> and an end tag \</or>.

### \<and>

Defines all finds conjunct with and. It has a start tag \<and> and an end tag \</and>.

### \<find>

Please refer to [Element - \<find](find.md)>

## Attribute

| Attribute                     | Description                                                                  | Type     | Default (\* must have) |
| ----------------------------- | ---------------------------------------------------------------------------- | -------- | ---------------------- |
| id                            | Specifies a unique id for an element                                         | Interger | \*                     |
| name                          | Specifies a name for an element                                              | String   |                        |
| sessionBase                   | If one packet in session match filter, the whole session will treat as match | yes/no   | yes                    |
| matchedlog                    | if match filter and syslog set, send log                                     | yes/no   | no                     |
| blockifempty                  | block if no find in filter                                                   | yes/no   | no                     |
| maxPackets                    | only match first N packets in a session                                      | Interger | 0(means no limit)      |
| masking                       | only for hfa regex condition, just masking, no filter function               | yes/no   | no                     |
| tuple5\_live\_hashtable\_size | set hash table size for tuple5 live use only                                 | Interger | no                     |

## Example

### only match first 10 packets in a session

```xml
<run>
<filter id="1" maxPackets="10">
    <or>
	<find name="regex" relation="==" content="abcdefg" />
    </or>
</filter>
<chain>
    <in>P0</in>
    <fid>F1</fid>
    <out>P1</out>
    <next type="notmatch">
        <out>P2</out>
    </next>
</chain>
</run>
```
