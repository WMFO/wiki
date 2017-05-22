This page described the WMFO IP Address space including conventions for assigning IP addresses, as well as the listing of all currently assigned IP addresses. It relates to the station's [Livewire Address Space](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space"). Please keep this page up-to-date as equitmnet is added/removed or conventions are adopted/droped.

page not found

IPv4 Local Network Info
-----------------------

 Subnet Mask: 255.255.0.0
 
 Net Address: 192.168.0.0
 
 Broadcast: 192.168.255.255
 
 Min Address: 192.168.0.1
 
 Max Address: 192.168.255.254

### Internal DHCP Info

Addresses: 192.168.10.\*

 Subnet Mask: 255.255.0.0
 
 Router: 192.168.0.10
 
 DNS: 192.168.0.10
 
 Search domains: wmfo.local

Basic IPv4 Conventions
----------------------

A method for the madness... Set as of 05/2012. The conventions are desgined to allow for future expansion. If adding new equipment, please follow them to maintain consistency.

### IPv4 Third Byte

*Designates Device Location*


|**Device Location**|**IPv4 Base Address**|
--- | --- 
|Master Control|192.168.0.XXX|
|Studio A|192.168.1.XXX|
|Studio B|192.168.2.XXX|
|Studio C|192.168.3.XXX|
|Annex|192.168.4.XXX|
|MD/GM Office|192.168.5.XXX|
|\<Unassigned\>|192.168.6.XXX|
|\<Unassigned\>|192.168.7.XXX|
|\<Unassigned\>|192.168.8.XXX|
|Tower/Ballou|192.168.9.XXX|
|DHCP/Wireless|192.168.10.XXX|

### IPv4 Fourth Byte Ranges

*Designates Device Type*

#### *General Device Class Ranges*


|**Device Type**|**IPv4 Address Range**|**Notes**|
--- | --- | ---
|Network Device|192.168.YYY.0XX|Start at bottom of range, work up|
|"Other" Device|192.168.YYY.0XX|Start at top of range, work down|
|Livewire/Axia Device|192.168.YYY.1XX|See Subclass Range Info|
|General Computer/Server|192.168.YYY.2XX|See Subclass Range Info|

##### Network Device Subclass Ranges

|**Device Subtype**|**IPv4 Address Range**|**Notes**|
--- | --- | ---
|Switch/Router|192.168.YYY.00X|-|
|Gateway/Router|192.168.YYY.01X|-|
|PDU|192.168.YYY.02X|-|
|Phone Related|192.168.YYY.03X|ATAs etc.|
|Clock|192.168.YYY.04X| |
|Printer|192.168.YYY.05X| |
|UPS|192.168.YYY.08X| |
|Regulatory|192.168.YYY.09X|Split up one day?|

##### Livewire/Axia Device Subclass Ranges

|**Device Subtype**|**IPv4 Address Range**|**Notes**|
--- | --- | ---
|Analog Node|192.168.YYY.10X|-|
|Digital Node|192.168.YYY.11X|-|
|Router Selector Node|192.168.YYY.12X|-|
|ASI/Soundcard/Driver|192.168.YYY.13X|-|
|"Other" Livewire Device|192.168.YYY.14X|e.g. Zephyr IP, Nx6|
|StudioEngine/PowerStation/Mixer|192.168.YYY.150, 192.168.YYY.170|No Intermediate Addresses|
|Element Board|192.168.YYY.160, 192.168.YYY.180|No Intermediate Addresses|
|\<Unassigned\>|192.168.YYY.19X|-|

##### General Computer/Server Subclass Ranges

|**Device Subtype**|**IPv4 Address Range**|**Notes**|
--- | --- | ---
|Linux Based (Primary OS)|192.168.YYY.20X|-|
|Windows Based (Primary OS)|192.168.YYY.21X|-|
|VPN clients|192.168.YYY.22X|-|
|IPMI|192.168.YYY.23X|-|
|VM Guests|192.168.YYY.24X|-|
|\<Unassigned\>|192.168.YYY.25X|-|

IPv4 Address Space
------------------

### WMFO LAN

|**IPv4 Address**|**FQDN**|**Name**|**Adapter**|**Description**|**Speed**|**MAC**|
|:---------------|:-------|:-------|:----------|:--------------|:--------|:------|
|192.168.0.0|-|NETWORK|-|NETWORK|-|NETWORK|
|192.168.0.1|-|CONS1|Catalyst 2960G-24|Cisco Switch|Mixed|-|
|192.168.0.2|-|CONS2|Procurve 2610-24|HP Switch|Mixed|-|
|192.168.0.10|-|Primary Gateway|D-Link DIR-655|D-Link Router|10/100/1000|-|
|192.168.0.30|-|conata1| |ATA w/ 8 FXS|10/100| |
|192.168.0.90|-|CONEAS|-|EAS|10/100|-|
|192.168.0.80|ups.wmfo.local|station-ups|-|UPS|10/100|00:C0:B7:52:1C:61|
|192.168.0.100|-|CONA1|-|Axia Analog Node|10/100|00:50:C2:80:1F:FB |
|192.168.0.110|-|COND1|-|Axia Digital Node|10/100|-|
|192.168.0.120|-|CONRS1|-|Axia RS Node|10/100|-|
|192.168.0.130|-|CONASI1|ASI6585|Audioscience Livewire PCI|10/100|-|
|192.168.0.140|-|CONZP1|-|Teleos Zephyr/IP|10/100|-|
|192.168.0.141|-|CONNX1|-|Teleos Nx6|10/100|-|
|192.168.0.142|-|CONOMNIA1|-|Omnia ONE|10/100|00:50:C2:49:34:84|
|192.168.0.150|-|CONSE1|-|Axia Studio Engine|10/100/1000|00:19:DB:E4:02:06|
|192.168.0.200 |thinwhiteduke.wmfo.local|ThinWhiteDuke|ADMTek NC110|Linux Server PCI|10/100|00:22:6B:BC:82:C7|
|192.168.0.201|ringo.wmfo.local|Ringo|?|File Server Embedded|10/100/1000|0C:C4:7A:68:87:F8|
|192.168.0.210|supertramp.wmfo.local|Supertramp|Marvell Yukon 88E8056|File Server Embedded|10/100/1000|00:24:8C:19:69:67|
|192.168.0.230|ipmi.tbd.wmfo.local|IPMI Tbd|-|File Server Embedded|-|00:24:8C:19:69:67|
|192.168.1.20|sapdu.wmfo.local|SAPDU| | |10/100|00:0C:B7:79:09:D0|
|192.168.1.40|-|SACLK|PoE|NTP PoE Clock|10/100|00:60:35:1D:45:56|
|192.168.1.80| | | | | | |
|192.168.1.100|-|SAA1|-|Axia Analog Node|10/100|-|
|192.168.1.160|-|SAEGP1|-|Axia Element|10/100|-|
|192.168.1.200|tinmachine.wmfo.local|Tinmachine|PCI|Retired Studio A Terminal|10/100/1000|-|
|192.168.1.201|adele.wmfo.local|adele|Internal|Studio A Terminal|10/100/1000|00:01:2E:4E:3F:1B|
|192.168.2.100| -|SBA1|-|Axia Analog Node|10/100|00:50:C2:80:1F:FC|
|192.168.2.110| -|SBD1|-|Axia Digital Node|10/100|-|
|192.168.2.120| -|SBRS1|-|Axia RS Node|10/100|00:50:C2:80:1C:82|
|192.168.2.210|devolution.wmfo.local|Devolution|-|Studio B Terminal|10/100/1000|00:24:8C:2E:4D:27|
|192.168.3.20|-|SCPDU| |CyberPower PDU|10/100|00:0C:15:40:39:B9|
|192.168.3.150|-|SCPSM1|-|Axia PowerStation Main|10/100/1000|00:50:C2:80:64:19|
|192.168.3.151|-|SCPSM1S|-|Switch in SCPSM1|"|"|
|192.168.3.152|-|SCPSM1A|-|Audio Node in SCPSM1|"|"|
|192.168.3.153|-|SCPSA1|-|Axia PowerStation Aux|10/100|00:50:C2:30:67:3A|
|192.168.3.200|coulton.wmfo.local|Coulton|Mobo|Studio C Terminal|10/100/1000|00:12:3F:71:26:1E|
|192.168.4.210|smoothcriminal.wmfo.local|Smoothcriminal| Marvell Yukon 88E8056|Web Server Embedded|10/100/1000|00:24:8C:6B:78:5F|
|192.168.5.90|-|GM Printer|-|HP LaserJet|10/100|-|
|192.168.5.91|-|MD Printer|-|HP Officejet Pro|10/100|00:1C:C4:FA:2A:52|
|192.168.5.210|floodland.wmfo.local|Floodland|-|MD Terminal|10/100/1000|00:13:72:24:38:46|
|192.168.9.1|-|TOWS1|Catalyst 2960G-8|Cisco Switch|Mixed|-|
|192.168.9.20|-|TOWPDU| |CyberPower PDU|10/100|00:0C:16:40:0F:56|
|192.168.9.90|-|TOWET1|GSC/VRC IP Converter|Burk Ethernet Telemetry|-|-|
|192.168.9.91| |TOWTR1|DB Mozart 100|transmitter| |00:04:40:a5:01:01|
|192.168.9.120 |-| TOWRS1|-|Axia RS Node|10/100|00:50:C2:80:1C:83|
|192.168.9.142| |TowerOmnia1| |Axia Omnia One|10/100| |
|192.168.255.255|-|BROADCAST|-|BROADCAST|-|BROADCAST|

### WMFO WAN

|**IPv4 Address**|**FQDN**|**Computer**|**Adapter**|**Description**|**Speed**|**MAC**|
|:---------------|:-------|:-----------|:----------|:--------------|:--------|:------|
|130.64.87.23|wmfo-primary.orgs.tufts.edu|Primary Gateway|D-Link DIR-655|D-Link Router|10/100/1000|00:22:B0:B8:00:F2|
|130.64.87.44|wmfo-smooth.orgs.tufts.edu|Smoothcriminal|Intel PRO/1000 GT|File Server  PCI|10/100/1000|00:1B:21:2F:E2:7F|
|130.64.87.45|[wmfo-wiki.orgs.tufts.edu](http://wmfo-wiki.orgs.tufts.edu "http://wmfo-wiki.orgs.tufts.edu/")|DeltekWiki|Intel PRO/1000 GT|Wiki VM|10/100/1000|00:0C:29:C7:57:E9|
|130.64.87.46|wmfo-super.orgs.tufts.edu|Supertramp|Intel PRO/1000 GT|Web Server PCI|10/100/1000|00:1B:21:2F:E1:B8|
|130.64.87.48|wmfo-duke.orgs.tufts.edu|ThinWhiteDuke|D-Link DGE-560T|Linux Server PCI-E|10/100/1000| 00:21:91:19:94:CF|
|130.64.87.20|wmfo-ringo.orgs.tufts.edu|Ringo|?|File Server|10/100/1000|00:1B;21:C4:12:43|
|130.64.29.251|wmfo-http.orgs.tufts.edu|wmfo-http|?|Web Server|10/100/1000|52:54:00:00:47:5b|
|130.64.29.252|wmfo-webstream.orgs.tufts.edu|wmfo-webstream|?|Webstream Server|10/100/1000|52:54:00:62:35:5b|
|DHCP|-|MOBZP1|LiveWire RJ-45|Telos Zepher|10/100|00:E0:4B:1B:D7:08|
|DHCP|-|MOBZP1 dongle|IOgear WiFi USB 2.0|WiFi dongle|?|00:21:79:C3:19:ED|

### WMFO Server-to-Server

IPv4 DNS Servers
----------------

In order of preference. Linux config is done in `/etc/resolv.conf​` or `/etc/dhcp3/dhclient.conf` if using DHCP

|**Address**|**Name**|
--- | ---
|192.168.0.10|Ubiquiti Gateway DNS Relay|
|130.64.25.5|Tufts|
|130.64.35.5|Tufts|
|8.8.8.8|Google|

NTP Servers
-----------

In order of preference. Linux config is done in `/etc/ntp.conf`

|**Address**|**Name**|
--- | ---
|192.168.0.210|Supertramp|
|192.43.244.18|[time.nist.gov](http://www.pool.ntp.org/scores/192.43.244.18 "http://www.pool.ntp.org/scores/192.43.244.18")|
|24.56.178.140|[www.nist.gov](http://tf.nist.gov/tf-cgi/servers.cgi "http://tf.nist.gov/tf-cgi/servers.cgi")|



