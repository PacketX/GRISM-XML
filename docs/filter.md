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
| masking | only for hfa regex condition, just masking, no filter function | yes/no | no |

## Example
```xml
<filter id="1">
<or>
find contents goes here..
</or>
</run>
```


