# Element - filter
Defines the filter. 
It has a start tag &lt;filter&gt; and an end tag &lt;/filter&gt;.

- start at &lt;or&gt;&lt;/or&gt;(default) or &lt;and&gt;&lt;/and&gt;
- then put finds &lt;find/&gt; in here

### &lt;or&gt;
Defines all finds conjunct with or. 
It has a start tag &lt;or&gt; and an end tag &lt;/or&gt;.

### &lt;and&gt;
Defines all finds conjunct with and. 
It has a start tag &lt;and&gt; and an end tag &lt;/and&gt;.

### &lt;find&gt;
Please refer to [Element - find](find.md)

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| name | Specifies a name for an element | String | |
| sessionBase | If one packet in session match filter, the whole session will treat as match | yes/no | yes |
| matchedlog |if match filter and syslog set, send log | yes/no | no |
| maxPackets | only match first N packets in a session | Interger | 0(means no limit) |
| masking | only for hfa regex condition, just masking, no filter function | yes/no | no |

## Example

### only match first 5 packets in a session
```xml
<run>
<filter id="1" maxPackets="10" >
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
