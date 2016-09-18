Getting Wireless running on the pi

Pi Zero

edit wpa supplicant see sample config file 
	sudo vi /etc/wpa_supplicant/wpa_supplicant.conf

----
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
        ssid="ATT285"
        psk="<pass>"
        scan_ssid=1
        proto=RSN
        pairwise=CCMP
        auth_alg=OPEN
}
----
	
look for name of wlan device
	ifconfig

looking for networks
	sudo iwlist wlan0 scan

starting
	sudo ifconfig wlan0 up
	
confirming ip
	ifconfig

see:

https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md
http://askubuntu.com/questions/652864/wpa-supplicant-does-not-connect-with-ioctlsiocsiwencodeext-invalid-argument
