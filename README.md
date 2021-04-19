# RBK753-AP-Satellite-Sync
Share - RBK753 AP Mode satellite ssid/encryption type/key not consistance with router


### Prepare:
* Setup your router wifi config first:
  * Set up router as AP mode
  * Make sure the security type is "WPA2-PSK[AES]"
  * Remove all existing satellites
* Reset all satellites  => power up => Sync up with main router(I hard wired router and satellites), make sure satellites shows in "Connected Satellites"


### To Do:
Now if login into satellite, you should see the satellites **2.4g ssid is preset "ORBIXXX"** and **5g ssid is correct but Security Type is none** which is not consistance as what we set in the main router.


What we going to do here is mannually make change for satellites nvram settting via telnet.

First, to enable the telnet by using the tool below:
  * https://github.com/insanid/NetgearTelnetEnable
  

```
telnet YOUR_SATELLITES_IP
```

Motify and execute command below or save as bash file, run `/bin/sh xxx.sh`

```
nvram set wla_temp_ssid="YOUR_SSID"
nvram set wla_ssid="YOUR_SSID"
nvram set radio1.vap1.ssid="YOUR_SSID"
nvram set wlh_temp_ssid="YOUR_SSID"
nvram set wlh_ssid="YOUR_SSID"
nvram set radio2.vap1.ssid="YOUR_SSID"
nvram set radio1.vap1.passphrase="YOUR_PASSWORD"
nvram set wlh_passphrase="YOUR_PASSWORD"
nvram set radio2.vap1.passphrase="YOUR_PASSWORD"
nvram set wla_passphrase="YOUR_PASSWORD"
nvram set wla_secu_type="WPA2-PSK"
nvram set radio3.vap1.secu_type="WPA2-PSK"
nvram set wlg_secu_type="WPA2-PSK"
nvram set radio2.vap1.secu_type="WPA2-PSK"
nvram set wlh_secu_type="WPA2-PSK"
nvram set radio1.vap1.secu_type="WPA2-PSK"
nvram set radio2.vap2.secu_type="WPA2-PSK"
nvram set wla_ssid_3="YOUR_GUEST_SSID"
nvram set radio1.vap2.ssid="YOUR_GUEST_SSID"
nvram set wlh_ssid_2="YOUR_GUEST_SSID"
nvram set radio2.vap3.ssid="YOUR_GUEST_SSID"

nvram commit

```
Run `Reboot` satellites and wait for the router sync with satellite, the problem should be fixed. 

Note: if you saw other unconsistance config, please telnet into router and satellite. Compare the difference and make your own change(`nvram show`). 

Good Luck!




