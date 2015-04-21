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

The regular expression @WLCs uplink interfaces
- Expression: Virtual Interface
- Expression type: Result is FALSE
- CaseSensitive: FALSE
