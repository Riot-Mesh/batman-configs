# batman-configs
### Tested on Linux OpenWrt 4.14.167 #0 SMP Wed Jan 29 16:05:35 2020 aarch64 GNU/Linux
#### kmod-batman-adv - 4.14.167+2019.2-5
#### batctl-default - 2019.2-3

``/etc/config/network``
```
config interface 'loopback'
	option ifname 'lo'
	option proto 'static'
	option ipaddr '127.0.0.1'
	option netmask '255.0.0.0'

config globals 'globals'
	option ula_prefix 'fd93:f71f:8e3c::/48'

config interface 'lan'
	option type 'bridge'
	option ifname 'eth0'
	option netmask '255.255.255.0'
	option ip6assign '60'
	option proto 'dhcp'
	option ipaddr '192.168.1.2'

# ADD THIS
config interface bat0
	option proto 'batadv'
 
# ADD THIS
config interface 'nwi_mesh0'
	option mtu '2304'
	option proto 'batadv_hardif'
	option master 'bat0'
```

``/etc/config/wireless``
```
config wifi-device 'radio1'
        option type 'mac80211'
        option channel '36'
        option hwmode '11a'
        option path 'platform/soc/3f980000.usb/usb1/1-1/1-1.5/1-1.5:1.0'
        option htmode 'VHT80'
        option disabled '0' # remember to enable this interface

config wifi-iface 'default_radio1'
        option device 'radio1'
        option mode 'adhoc'
        option ssid 'mymeshaarnav'
        option encryption 'none'
        option channel '8'
        option mtu '1536'
        option network 'nwi_mesh0'
```
