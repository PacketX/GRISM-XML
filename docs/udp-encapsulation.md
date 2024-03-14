# UDP Encapsulation

<img src="../.gitbook/assets/file.excalidraw (1).svg" alt="UDP Tunnel for Mirror traffic" class="gitbook-drawing">

## GRISM1

### Config XML

```xml
<configSet reboot="no">
     <ifcfgs>
        <find role="ft">
            <enable>True</enable>
            <ip>192.168.1.100</ip>
            <name>P7</name>
            <netmask>255.255.255.0</netmask>
            <gateway></gateway>
        </find>
    </ifcfgs>
</configSet>
```

### GRISM XML

```xml
<run>
    <output id="7" type="udpencap">
        <port>P7</port>
        <dip>192.168.1.101</dip>
        <sport>3060</sport>
        <dport>3060</dport>
    </output>
    <chain>
        <in>P6</in>
        <out>O7</out>
    </chain>
</run>
```

## GRISM2

### Config XML

```xml
<configSet reboot="no">
     <ifcfgs>
        <find role="ft">
            <enable>True</enable>
            <ip>192.168.1.101</ip>
            <name>P7</name>
            <netmask>255.255.255.0</netmask>
            <gateway></gateway>
        </find>
    </ifcfgs>
</configSet>
```

### GRISM XML

```xml
<run>
    <chain>
        <in>P7</in>
        <out>P6</out>
    </chain>
</run>
```
