# Element - filter
Defines the filter. 
It has a start tag &lt;filter&gt; and an end tag &lt;/filter&gt;.

- start at &lt;or&gt;&lt;/or&gt;(default) or &lt;and&gt;&lt;/and&gt;
- then put finds &lt;find/&gt; in here

### or
Defines all finds conjunct with or. 
It has a start tag &lt;or&gt; and an end tag &lt;/or&gt;.

### and
Defines all finds conjunct with and. 
It has a start tag &lt;and&gt; and an end tag &lt;/and&gt;.

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| name | Specifies a name for an element | String | |
| sessionBase | If one packet in session match filter, the whole session will treat as match | yes/no | yes |
| matchedlog |if match filter and syslog set, send log | yes/no | no |
| maxPackets | only watch max packets in a session | Interger | 0(means no limit) |
| masking | only for hfa regex condition, just masking, no filter function | yes/no | no |

## Example
```xml
<filter id="1">
<or>
find contents goes here..
</or>
</run>
```

## Example - Youtube(SSL+QUIC)
```xml
<filter id="1" name="1" sessionBase="yes">
  <or>
    <find name="ssl.handshake.type" relation="==" content="0" />
    <find name="ssl.handshake.type" relation="==" content="1" />
    <find name="quic.tag" relation="==" content="CHLO" />
  </or>
</filter>
<filter id="2" name="2" sessionBase="yes">
  <or>
    <!-- youtube -->
    <find name="regex" relation="==" content="{s}youtube\." />
    <find name="regex" relation="==" content="{s}youtu\.be\." />
    <find name="regex" relation="==" content="{s}yt3\.ggpht\.com" />
    <find name="regex" relation="==" content="{s}\.googlevideo\.com" />
    <find name="regex" relation="==" content="{s}\.ytimg\.com" />
    <find name="regex" relation="==" content="{s}youtube\-nocookie\." />
    <find name="regex" relation="==" content="{s}ggpht.com" />
    <find name="regex" relation="==" content="{s}googleusercontent\.com" />
  </or>
</filter>
```
