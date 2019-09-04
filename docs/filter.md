# Element - filter
Defines the filter. 
It has a start tag &lt;filter&gt; and an end tag &lt;/filter&gt;.

- start at &lt;or&gt;&lt;/or&gt;(default) or &lt;and&gt;&lt;/and&gt;
- then put finds &lt;find/&gt; in here

## Attribute
| Attribute | Description | Type | Default (* must have) |
|---|---|---|---|
| id | Specifies a unique id for an element | Interger | * |
| name | Specifies a name for an element | String | |
| sessionBase | If one packet in session match filter, the whole session will treat as match | yes/no | yes |
| masking | only for hfa regex condition, just masking, no filter function | yes/no | no |


## Example
```xml
<filter id="1">
<or>
find contents goes here..
</or>
</run>
```


