## 描述:
Part of Application filters, includes domain and ip address from NDPI

## xml
```xml
<filter id="5" name="app domain filter" sessionBase="yes">
        <or>
            <!-- youtube -->
            <find name="regex" relation="==" content="{s}upload\.youtube\.com" />
            <find name="regex" relation="==" content="{s}upload\.video\.google\.com" />
            <find name="regex" relation="==" content="{s}youtubei\.googleapis\.com" />
            <find name="regex" relation="==" content="{s}youtube\." />
            <find name="regex" relation="==" content="{s}youtu\.be\." />
            <find name="regex" relation="==" content="{s}yt3\.ggpht\.com" />
            <find name="regex" relation="==" content="{s}\.googlevideo\.com" />
            <find name="regex" relation="==" content="{s}\.ytimg\.com" />
            <find name="regex" relation="==" content="{s}youtube\-nocookie\." />
            <!-- Gmail -->
            <find name="regex" relation="==" content="{s}\.gmail\." />
            <find name="regex" relation="==" content="{s}mail\.google\." />
            <!-- Dailymotion -->
            <find name="regex" relation="==" content="{s}dailymotion\.com" />
            <!-- webex -->
            <find name="regex" relation="==" content="{s}\.webex\.com" />
            <!-- Skype -->
            <find name="regex" relation="==" content="{s}\.skype\." />
            <find name="regex" relation="==" content="{s}\.skypeassets\." />
            <find name="regex" relation="==" content="{s}\.skypedata\." />
            <find name="regex" relation="==" content="{s}\.skypeecs\-" />
            <find name="regex" relation="==" content="{s}\.skypeforbusiness\." />
            <find name="regex" relation="==" content="{s}\.lync.com" />
            <find name="regex" relation="==" content="{s}e7768\.b\.akamaiedge\.net" />
            <find name="regex" relation="==" content="{s}e4593\.dspg\.akamaiedge\.net" />
            <find name="regex" relation="==" content="{s}e4593\.g\.akamaiedge\.net" />
            <find name="regex" relation="==" content="{s}\.gateway\.messenger\.live\.com" />
        </or>
    </filter>
    <filter id="6" name="app ip filter" sessionBase="yes">
        <or>
            <!-- webex -->
            <find name="ip.addr" relation="==" content="25.192.0/24" />
            <find name="ip.addr" relation="==" content="62.109.192.0/18" />
            <find name="ip.addr" relation="==" content="64.68.96.0/19" />
            <find name="ip.addr" relation="==" content="66.114.160.0/20" />
            <find name="ip.addr" relation="==" content="66.163.32.0/19" />
            <find name="ip.addr" relation="==" content="114.29.192.0/19" />
            <find name="ip.addr" relation="==" content="173.243.0.0/20" />
            <find name="ip.addr" relation="==" content="207.182.160.0/19" />
            <find name="ip.addr" relation="==" content="208.8.81.0/24" />
            <find name="ip.addr" relation="==" content="209.197.192.0/19" />
            <find name="ip.addr" relation="==" content="210.4.192.0/20" />
            <!-- Skype  (Microsoft CDN) -->
            <find name="ip.addr" relation="==" content="157.56.135.64/26" />
            <find name="ip.addr" relation="==" content="157.56.185.0/26" />
            <find name="ip.addr" relation="==" content="157.56.52.0/26" />
            <find name="ip.addr" relation="==" content="157.56.53.128/25" />
            <find name="ip.addr" relation="==" content="157.56.198.0/26" />
            <find name="ip.addr" relation="==" content="157.60.0.0/16" />
            <find name="ip.addr" relation="==" content="157.54.0.0/15" />
            <find name="ip.addr" relation="==" content="13.64.0.0/11" />
            <find name="ip.addr" relation="==" content="13.107.3.128" />
            <find name="ip.addr" relation="==" content="13.107.3.129" />
            <find name="ip.addr" relation="==" content="111.221.64.0/18" />
            <find name="ip.addr" relation="==" content="91.190.216.0/21" />
            <find name="ip.addr" relation="==" content="91.190.218.0/24" />
            <find name="ip.addr" relation="==" content="40.126.129.109" />
            <find name="ip.addr" relation="==" content="65.55.223.0/26" />
            <find name="ip.addr" relation="==" content="23.96.0.0/13" />
            <find name="ip.addr" relation="==" content="52.114.74.5" />
            <find name="ip.addr" relation="==" content="20.180.0.0/14" />
            <find name="ip.addr" relation="==" content="20.184.0.0/13" />
            <find name="ip.addr" relation="==" content="13.107.64.0/18" />
            <find name="ip.addr" relation="==" content="52.112.0.0/14" />
            <find name="ip.addr" relation="==" content="13.70.151.216/32" />
            <find name="ip.addr" relation="==" content="13.71.127.197/32" />
            <find name="ip.addr" relation="==" content="13.72.245.115/32" />
            <find name="ip.addr" relation="==" content="13.73.1.120/32" />
            <find name="ip.addr" relation="==" content="13.75.126.169/32" />
            <find name="ip.addr" relation="==" content="13.89.240.113/32" />
            <find name="ip.addr" relation="==" content="13.107.3.0/24" />
            <find name="ip.addr" relation="==" content="13.107.64.0/18" />
            <find name="ip.addr" relation="==" content="51.140.155.234/32" />
            <find name="ip.addr" relation="==" content="51.140.203.190/32" />
            <find name="ip.addr" relation="==" content="51.141.51.76/32" />
            <find name="ip.addr" relation="==" content="52.112.0.0/14" />
            <find name="ip.addr" relation="==" content="52.163.126.215/32" />
            <find name="ip.addr" relation="==" content="52.170.21.67/32" />
            <find name="ip.addr" relation="==" content="52.172.185.18/32" />
            <find name="ip.addr" relation="==" content="52.178.94.2/32" />
            <find name="ip.addr" relation="==" content="52.178.161.139/32" />
            <find name="ip.addr" relation="==" content="52.228.25.96/32" />
            <find name="ip.addr" relation="==" content="52.238.119.141/32" />
            <find name="ip.addr" relation="==" content="52.242.23.189/32" />
            <find name="ip.addr" relation="==" content="52.244.160.207/32" />
            <find name="ip.addr" relation="==" content="104.215.11.144/32" />
            <find name="ip.addr" relation="==" content="104.215.62.195/32" />
            <find name="ip.addr" relation="==" content="138.91.237.237/32" />
            <find name="ip.addr" relation="==" content="13.70.151.216/32" />
            <find name="ip.addr" relation="==" content="13.71.127.197/32" />
            <find name="ip.addr" relation="==" content="13.72.245.115/32" />
            <find name="ip.addr" relation="==" content="13.73.1.120/32" />
            <find name="ip.addr" relation="==" content="13.75.126.169/32" />
            <find name="ip.addr" relation="==" content="13.89.240.113/32" />
            <find name="ip.addr" relation="==" content="13.107.3.0/24" />
            <find name="ip.addr" relation="==" content="13.107.64.0/18" />
            <find name="ip.addr" relation="==" content="51.140.155.234/32" />
            <find name="ip.addr" relation="==" content="51.140.203.190/32" />
            <find name="ip.addr" relation="==" content="51.141.51.76/32" />
            <find name="ip.addr" relation="==" content="52.112.0.0/14" />
            <find name="ip.addr" relation="==" content="52.163.126.215/32" />
            <find name="ip.addr" relation="==" content="52.170.21.67/32" />
            <find name="ip.addr" relation="==" content="52.172.185.18/32" />
            <find name="ip.addr" relation="==" content="52.178.94.2/32" />
            <find name="ip.addr" relation="==" content="52.178.161.139/32" />
            <find name="ip.addr" relation="==" content="52.228.25.96/32" />
            <find name="ip.addr" relation="==" content="52.238.119.141/32" />
            <find name="ip.addr" relation="==" content="52.242.23.189/32" />
            <find name="ip.addr" relation="==" content="52.244.160.207/32" />
            <find name="ip.addr" relation="==" content="104.215.11.144/32" />
            <find name="ip.addr" relation="==" content="104.215.62.195/32" />
            <find name="ip.addr" relation="==" content="138.91.237.237/32" />
            <find name="ip.addr" relation="==" content="13.70.151.216/32" />
            <find name="ip.addr" relation="==" content="13.71.127.197/32" />
            <find name="ip.addr" relation="==" content="13.72.245.115/32" />
            <find name="ip.addr" relation="==" content="13.73.1.120/32" />
            <find name="ip.addr" relation="==" content="13.75.126.169/32" />
            <find name="ip.addr" relation="==" content="13.89.240.113/32" />
            <find name="ip.addr" relation="==" content="13.107.3.0/24" />
            <find name="ip.addr" relation="==" content="13.107.64.0/18" />
            <find name="ip.addr" relation="==" content="51.140.155.234/32" />
            <find name="ip.addr" relation="==" content="51.140.203.190/32" />
            <find name="ip.addr" relation="==" content="51.141.51.76/32" />
            <find name="ip.addr" relation="==" content="52.112.0.0/14" />
            <find name="ip.addr" relation="==" content="52.163.126.215/32" />
            <find name="ip.addr" relation="==" content="52.170.21.67/32" />
            <find name="ip.addr" relation="==" content="52.172.185.18/32" />
            <find name="ip.addr" relation="==" content="52.178.94.2/32" />
            <find name="ip.addr" relation="==" content="52.178.161.139/32" />
            <find name="ip.addr" relation="==" content="52.228.25.96/32" />
            <find name="ip.addr" relation="==" content="52.238.119.141/32" />
            <find name="ip.addr" relation="==" content="52.242.23.189/32" />
            <find name="ip.addr" relation="==" content="52.244.160.207/32" />
            <find name="ip.addr" relation="==" content="104.215.11.144/32" />
            <find name="ip.addr" relation="==" content="104.215.62.195/32" />
            <find name="ip.addr" relation="==" content="138.91.237.237/32" />
        </or>
    </filter>
```
