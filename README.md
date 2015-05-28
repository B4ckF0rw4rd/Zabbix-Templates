# Zabbix-Templates

All templates has been tested on Zabbix 2.2.X and 2.4.X branches!

To add my templates into your Zabbix distribution:

1 - Download the desired .xml

2 - From Zabbix Web GUI: Configuration -> Templates and click "import"

3 - Select the downloaded .xml and click on "Import" button

4 - Enjoy your brand new template!

# NOTES

For Template Cisco ASA Discovery:

The regular expression @Firewalls network interfaces for discovery
- Expression: (Internal-Data0/0|Internal-Data1/0|Virtual254|management)
- Expression type: Result is FALSE
- CaseSensitive: TRUE

For Template Cisco WLC Discovery:

The value mapping AP MAC -> NAME:
- AP MAC: It's the corresponding AP <strong>"RADIO"</strong> MAC Address;
- NAME: You can chose anithing suits to you, i've have hostnames like AP1, AP2, ecc

EXAMPLE: AP MAC -> NAME = 00:AA:BB:CC:DD:EE:FF:GG -> AP1

NOTE: The MAC must be in <strong>"UPPERCASE"</strong>.

The regular expression @WLCs uplink interfaces
- Expression: Virtual Interface
- Expression type: Result is FALSE
- CaseSensitive: FALSE

For Template Cisco Access Switch Interfaces Discovery:

The regular expression @Switches physical interfaces
- Expression 1: Loopback
- Expression type 1: Character string not included
- CaseSensitive 1: FALSE
- Expression 2: VLAN
- Expression type 2: Character string not included
- CaseSensitive 2: FALSE
- Expression 3: ^Null0
- Expression type 3: Result is FALSE
- CaseSensitive 2: TRUE

The regular expression @Switches uplink interfaces
- Expression: UPLINK TO
- Expression type: Result is TRUE
- CaseSensitive: TRUE
