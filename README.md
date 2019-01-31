# Zabbix-Templates

All templates has been tested on Zabbix 3.X

To add my templates into your Zabbix distribution:

0 - Download the Cisco MIBs from **ftp://ftp.cisco.com/pub/mibs/v2**

1 - Download the desired .xml

2 - From Zabbix Web GUI: Configuration -> Templates and click "import"

3 - Select the downloaded .xml and click on "Import" button

4 - Enjoy your brand new template!

# NOTES

For Template Cisco ASA Discovery:

The regular expression @Firewalls network interfaces for discovery
- Expression: (Internal|Virtual|management|plane|Null)
- Expression type: Result is FALSE
- CaseSensitive: TRUE

For Template Cisco WLC Discovery:

The value mapping AP MAC -> NAME:
- AP MAC: It's the corresponding AP <strong>"RADIO"</strong> MAC Address;
- NAME: You can chose anithing suits to you, i've have hostnames like AP1, AP2, ecc

EXAMPLE: AP MAC -> NAME = 00:AA:BB:CC:DD:EE:FF:GG -> AP1

Thanks to the help of <strong>@DRN88</strong> if you wanna create a quick Value map:

1. Configure SSH Client to save your terminal log. Like putty
2. Log into your WLC with ssh
3. Run this command: `show access-point-config` then keep pressing `q` (not space for more)
4. Quit putty session and find your log: `putty.log`
5. Run this bash script to generate the value map XML
```bash
egrep "(Cisco AP Name|MAC Address)" putty.log | awk 'NR%2{printf "%s ",$0;next;}1' | awk '{print $4","toupper($NF)}' | awk -f wlc.awk | xmllint --format - > zabbix-wlc-valuemap.xml
```
6. Import `zabbix-wlc-valuemap.xml` into zabbix

Content of `wlc.awk`

```awk
BEGIN{
FS=","
print "<?xml version=\"1.0\" encoding=\"UTF-8\"?>"
print "<zabbix_export>"
print "<version>3.4</version>"
print "<date>2018-03-09T11:56:38Z</date>"
print "<value_maps>"
print "<value_map>"
print "<name>AP MAC -> NAME</name>"
}
{
  print "<mapping>"
  print "<value>"$2"</value>"
  print "<newvalue>"$1"</newvalue>"
  print "</mapping>"
}
END{
print "</value_map>"
print "</value_maps>"
print "</zabbix_export>"
}
```

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
