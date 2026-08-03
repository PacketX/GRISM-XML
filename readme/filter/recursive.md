---
description: >-
  Defines nested filter groups. <and>, <or> and <not> can contain other groups,
  so one filter can express any boolean expression. (v6.5.260731)
---

# Recursive Filter

A filter group (\<and>, \<or>) is not limited to \<find/> elements. It can also contain **other groups**, and those groups can contain groups again. There is no operator precedence to remember - the nesting *is* the precedence.

With \<not>, the three group types cover every boolean expression, so a rule that used to need several filters combined in \<fid> can be written as a single filter.

<table><thead><tr><th width="330">Element</th><th width="200">Description</th><th>Support</th></tr></thead><tbody><tr><td>Group in group (<code>&#x3C;and></code>, <code>&#x3C;or></code>)</td><td>nested filter groups</td><td>v6.5.260731</td></tr><tr><td><code>&#x3C;not></code></td><td>invert a group</td><td>v6.5.260731</td></tr></tbody></table>

```xml
<filter id="1">
    <and>
        <or>
            <find name="tcp.port" relation="==" content="80" />
            <find name="tcp.port" relation="==" content="443" />
        </or>
        <not>
            <or>
                <find name="ip.addr" relation="==" content="10.0.0.0/8" />
            </or>
        </not>
    </and>
</filter>
```

> (tcp.port == 80 **or** tcp.port == 443) **and not** (ip.addr == 10.0.0.0/8)

## Elements in a group

### \<or>

Matches if **any** child (\<find/>, \<and>, \<or>, \<not>) matches.

### \<and>

Matches if **every** child (\<find/>, \<and>, \<or>, \<not>) matches.

### \<not>

Inverts the group it contains. It has a start tag \<not> and an end tag \</not>.

\<not> must contain an \<and> or \<or> group - a \<find/> can not be put directly into \<not>. The group makes the meaning explicit, so there is never a question of how the terms inside are conjuncted:

```xml
<!-- not (A or B) -> matches when neither A nor B -->
<not>
    <or>
        <find name="ip.addr" relation="==" content="8.8.8.8" />
        <find name="ip.addr" relation="==" content="8.8.4.4" />
    </or>
</not>
```

```xml
<!-- not (A and B) -> matches unless both A and B -->
<not>
    <and>
        <find name="ip.addr" relation="==" content="8.8.8.8" />
        <find name="udp.port" relation="==" content="53" />
    </and>
</not>
```

\<not> must be nested inside an \<and> or \<or> group. The outermost group of a filter is still \<and> or \<or>, as described in [Element - \<filter>](./).

{% hint style="info" %}
To invert one single field, use `relation="!="` on the \<find/> instead - `<find name="ip.addr" relation="!=" content="8.8.8.8"/>`. Use \<not> to invert a whole group.
{% endhint %}

## Example

Traffic from CN or RU, on HTTPS or DNS port, excluding two well-known public resolvers:

```xml
<run>
    <filter id="1" name="suspicious geo traffic" sessionBase="no">
        <and>
            <!-- country is CN or RU -->
            <or>
                <find name="country.iso_code" relation="==" content="CN"/>
                <find name="country.iso_code" relation="==" content="RU"/>
            </or>
            <!-- and port is 443 or 53 -->
            <or>
                <find name="tcp.port" relation="==" content="443"/>
                <find name="udp.port" relation="==" content="53"/>
            </or>
            <!-- and not a trusted resolver -->
            <not>
                <or>
                    <find name="ip.addr" relation="==" content="8.8.8.8"/>
                    <find name="ip.addr" relation="==" content="168.95.1.1"/>
                </or>
            </not>
        </and>
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

## Compare with \<fid>

The same rule written the flat way - one filter per term, combined in the chain with \<fid>:

```xml
<run>
    <filter id="1" name="geo" sessionBase="no">
        <or>
            <find name="country.iso_code" relation="==" content="CN"/>
            <find name="country.iso_code" relation="==" content="RU"/>
        </or>
    </filter>
    <filter id="2" name="port" sessionBase="no">
        <or>
            <find name="tcp.port" relation="==" content="443"/>
            <find name="udp.port" relation="==" content="53"/>
        </or>
    </filter>
    <filter id="3" name="trusted resolver" sessionBase="no">
        <or>
            <find name="ip.addr" relation="==" content="8.8.8.8"/>
            <find name="ip.addr" relation="==" content="168.95.1.1"/>
        </or>
    </filter>
    <chain>
        <in>P0</in>
        <fid type="and">F1,F2,!F3</fid>
        <out>P1</out>
        <next type="notmatch">
            <out>P2</out>
        </next>
    </chain>
</run>
```

Both forms are valid. Which one to pick:

<table><thead><tr><th width="200">Use</th><th>When</th></tr></thead><tbody><tr><td>Recursive filter</td><td>The expression belongs to one rule, and mixes <em>and</em> / <em>or</em> at different levels. Keeps the chain short and the filter self-documenting.</td></tr><tr><td>Several filters + <code>&#x3C;fid></code></td><td>The terms are reused by more than one chain, or each term needs its own filter attributes (<code>sessionBase</code>, <code>maxPackets</code>, <code>matchedlog</code>, <code>start</code>/<code>within</code>, ...) - those are set per filter, not per group.</td></tr></tbody></table>

## Notes

* Filter attributes such as `sessionBase`, `maxPackets` and `matchedlog` apply to the **whole filter**, not to an individual group. Split into separate filters when different terms need different attributes.
* Attributes that anchor a search (`start`, `position`, `within`) also apply to the whole filter, so all `regex` finds inside every group share them.
* An empty group has no terms to evaluate - see `blockifempty` in [Element - \<filter>](./).
