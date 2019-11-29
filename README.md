# Configure-Sonoff-mini-DIY-mode-using-mac
Configure your Sonoff mini DIY using a Apple mac

In deze tutorial gaan we een Sonoff aansluiten in DIY mode zodat de hele zooi niet via China gaat
Sluit je Sonoff aan via het volgende wiring diagram.

![Sonoff-MINI-Wiring-Diagram](Sonoff-MINI-Wiring-Diagram.jpg)

Plug de Sonoff switch via een stekker in het stopcontact richting een lamp, komt er ongeveer zo uit te zien.

![Sonoff-wired](Sonoff-wired.png)

Verbind je Apple Macbook nu met een kabel, Ga naar internet sharing en share je Ethernet richting Wifi en maak een ssid aan met de volgende gegevens

```
WiFi SSID: sonoffDiy
password: 20170618sn
```
Open als je bent verbonden je Discovery (voormalig Bonjour) en check hierin iets wat op eWelink lijkt

![Sonoff-Discovery](Sonoff-Discovery.png)


Of voer in je terminal in: 
```
<Computername>:~ ><Username>$ dns-sd -B _ewelink._tcp

Browsing for _ewelink._tcp
DATE: ---Thu 28 Nov 2019---
 9:36:38.408  ...STARTING...
Timestamp     A/R    Flags  if Domain               Service Type         Instance Name
 9:36:38.409  Add        2  15 local.               _ewelink._tcp.       eWeLink_1000axxxxx
 9:36:38.734  Add        2   5 local.               _ewelink._tcp.       eWeLink_1000axxxxx
 9:36:38.998  Add        2  14 local.               _ewelink._tcp.       eWeLink_1000axxxxx
```

Alle gegevens die je nodig heb:
```
device1 - 1000axxxxx - 192.168.0.1
device2 - 1000axxxxx - 192.168.0.2
```


gebruik dan het volgende commando om de boel te testen als je nog verbonden bent met je eigen gemaakte netwerk
```
#lamp aan/uit

on
curl -XPOST "http://<Ip-add>:8081/zeroconf/switch" -d '{"deviceid":"1000axxxxx","data":{"switch":"on"}}'

off
curl -XPOST "http://<Ip-add>:8081/zeroconf/switch" -d '{"deviceid":"1000axxxxx","data":{"switch":"off"}}'
```

wijzig het SSID met het volgende commando

```
curl -XPOST "http://<Ip-add>:8081/zeroconf/wifi" -d '{"deviceid":"1000axxxxx","data":{"ssid": "<Wifi network name>","password": "<Wifi Password>"}}'
```

Test na dit commando via het netwerk of je nu de lamp in gebruik kan nemen
Het kan even duren voordat hij in discovery verschijnt, check eventueel het IP in je Router/Firewall met de naam ESP_8xxxxx
```
#lamp aan/uit

on
curl -XPOST "http://<Ip-add>:8081/zeroconf/switch" -d '{"deviceid":"1000axxxxx","data":{"switch":"on"}}'

off
curl -XPOST "http://<Ip-add>:8081/zeroconf/switch" -d '{"deviceid":"1000axxxxx","data":{"switch":"off"}}'
```
