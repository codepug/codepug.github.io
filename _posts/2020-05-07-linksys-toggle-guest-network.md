---
layout: home
title: Toggle the Guest Network on Your Linksys Router
permalink: /wiki/linksys-toggle-guest-network
tag: misc
---

## Toggle the Guest Network on Your Linksys Router

One of the cool features found in many SOHO wireless router firmwares now a days is the ability to broadcast a guest network.  This guest network allows people who are visiting your home or small office to connect to the Internet while at the same time preventing direct connections to the other computers on your network.  However, I found it also useful to be able to toggle this guest network on and off depending if I have visitors or not.  The following scripts can be customized to run from a Linux or Mac platform to provide a quick and easy way to turn this feature on and off.

### Customizable Scripts

Script to activate the guest network.  The osascript command is optional and used to display an alert for MacOS X systems.

<code>
#!/bin/sh

IS_ACTIVE=true
SSID=<NAME OF GUEST NETWORK>
PWD=<PASSWORD TO CONNECT HERE>
AUTH=<BASE64 ENCODED VALUE USERNAME:PASSWORD>
ROUTER_IP=192.168.1.1

curl -v -H "Content-Type: application/json" -H "X-JNAP-AUTHORIZATION: Basic $AUTH" -H "X-JNAP-ACTION: http://linksys.com/jnap/guestnetwork/SetGuestRadioSettings" -X POST -d '{"isGuestNetworkEnabled":'$IS_ACTIVE',"maxSimultaneousGuests":5,"radios":[{"radioID":"RADIO_2.4GHz","isEnabled":'$IS_ACTIVE',"broadcastGuestSSID":true,"guestSSID":"'$SSID'","guestPassword":"'$PWD'"},{"radioID":"RADIO_5GHz","isEnabled":false,"broadcastGuestSSID":false,"guestSSID":"'$SSID'5","guestPassword":"'$PWD'"}]}' http://$ROUTER_IP/JNAP/
osascript -e 'display notification "Turning '$SSID' on with password '$PWD'" with title "Activating Guest Network"'
</code>

Script to deactivate the guest network.
<code>
#!/bin/sh

IS_ACTIVE=false
SSID=<NAME OF GUEST NETWORK>
PWD=<PASSWORD TO CONNECT HERE>
AUTH=<BASE64 ENCODED VALUE USERNAME:PASSWORD>
ROUTER_IP=192.168.1.1

curl -v -H "Content-Type: application/json" -H "X-JNAP-AUTHORIZATION: Basic $AUTH" -H "X-JNAP-ACTION: http://linksys.com/jnap/guestnetwork/SetGuestRadioSettings" -X POST -d '{"isGuestNetworkEnabled":'$IS_ACTIVE',"maxSimultaneousGuests":5,"radios":[{"radioID":"RADIO_2.4GHz","isEnabled":'$IS_ACTIVE',"broadcastGuestSSID":true,"guestSSID":"'$SSID'","guestPassword":"'$PWD'"},{"radioID":"RADIO_5GHz","isEnabled":false,"broadcastGuestSSID":false,"guestSSID":"'$SSID'5","guestPassword":"'$PWD'"}]}' http://$ROUTER_IP/JNAP/
osascript -e 'display notification "Turning '$SSID' off" with title "Shutting Down Guest Network"'
</code>

To make these scripts executable by double clicking on the MacOS X platform, open up the AppleScript Editor and save the following as applications.

Filename: TurnOnGuestNetwork
<code>
property IS_ACTIVE : "true"
property SSID : "<NAME OF GUEST NETWORK>"
property PWD : "<PASSWORD TO CONNECT HERE>"
property AUTH : "<BASE64 ENCODED VALUE USERNAME:PASSWORD>"
property ROUTER_IP : "192.168.1.1"

do shell script "curl -v -H \"Content-Type: application/json\" -H \"X-JNAP-AUTHORIZATION: Basic " & AUTH & "\" -H \"X-JNAP-ACTION: http://linksys.com/jnap/guestnetwork/SetGuestRadioSettings\" -X POST -d '{\"isGuestNetworkEnabled\":'" & IS_ACTIVE & "',\"maxSimultaneousGuests\":5,\"radios\":[{\"radioID\":\"RADIO_2.4GHz\",\"isEnabled\":'" & IS_ACTIVE & "',\"broadcastGuestSSID\":true,\"guestSSID\":\"'" & SSID & "'\",\"guestPassword\":\"'" & PWD & "'\"},{\"radioID\":\"RADIO_5GHz\",\"isEnabled\":false,\"broadcastGuestSSID\":false,\"guestSSID\":\"'" & SSID & "'5\",\"guestPassword\":\"'" & PWD & "'\"}]}' http://" & ROUTER_IP & "/JNAP/"


display notification "Turning '" & SSID & "' on with password '" & PWD & "'" with title "Activating Guest Network"
</code>

Filename: TurnOffGuestNetwork
<code>
property IS_ACTIVE : "false"
property SSID : "<NAME OF GUEST NETWORK>"
property PWD : "<PASSWORD TO CONNECT HERE>"
property AUTH : "<BASE64 ENCODED VALUE USERNAME:PASSWORD>"
property ROUTER_IP : "192.168.1.1"

do shell script "curl -v -H \"Content-Type: application/json\" -H \"X-JNAP-AUTHORIZATION: Basic " & AUTH & "\" -H \"X-JNAP-ACTION: http://linksys.com/jnap/guestnetwork/SetGuestRadioSettings\" -X POST -d '{\"isGuestNetworkEnabled\":'" & IS_ACTIVE & "',\"maxSimultaneousGuests\":5,\"radios\":[{\"radioID\":\"RADIO_2.4GHz\",\"isEnabled\":'" & IS_ACTIVE & "',\"broadcastGuestSSID\":true,\"guestSSID\":\"'" & SSID & "'\",\"guestPassword\":\"'" & PWD & "'\"},{\"radioID\":\"RADIO_5GHz\",\"isEnabled\":false,\"broadcastGuestSSID\":false,\"guestSSID\":\"'" & SSID & "'5\",\"guestPassword\":\"'" & PWD & "'\"}]}' http://" & ROUTER_IP & "/JNAP/"

display notification "Turning '" & SSID & "' off" with title "Shutting Down Guest Network"
</code>