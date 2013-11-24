AirVPN CLI
===========

Makes connecting to AirVPN servers in Linux a breeze (for me anyway).

###Install

####Prerequisites

Have `openvpn` installed. In Ubuntu and Mint: `sudo apt-get install openvpn`

`airvpn` has only been tested with Python 2.7.x. It requires that you have the following python packages installed:

* docopt
* sh
* lxml
* requests
* texttable

ex. `pip install docopt sh lxml requests texttable`

####Setup

If your `python` binary is located somewhere that isn't `/usr/bin/python`, change the first line of 
`airvpn` appropriately. 

ex. If my name is waffles and I use `virtualenvwrapper` to create a virtualenv called `airvpn-cli`:

```shell
#!/home/waffles/.virtualenvs/airvpn-cli/bin/python

"""
AirVPN CLI.

```

Copy `airvpn` somewhere in your path. ex. `sudo cp airvpn /bin`


###Commands

*Note*: Before you start using `airvpn` for the first time, make sure `openvpn` is not running. 

####list
ex. `airvpn list`

List all AirVPN servers and their locations. To list the servers that are configured on your machine, add the `--local` option. 

####setup

ex. `sudo airvpn setup pavonis`

Generate and save the configuration for the specified server in the OpenVPN configuration directory (`/etc/openvpn` by default). 
If your OpenVPN configuration directory is not the default, specify it with the `--openvpn-dir` option. This command will 
require your AirVPN username and password. To connect immediately after setup, add the `--connect` option.

This command must be run with root permissions.

####connect

ex. `sudo airvpn connect pavonis`

Connect to the specified server. This, of course, requires that you have already run `setup` for the specified server. 

This command must be run with root permissions.

####disconnect

ex. `sudo airvpn disconnect`

Exactly what it sounds like.

This command must be run with root permissions.

####remove

ex. `sudo airvpn remove pavonis`

Remove the specified server configuration from your machine. 

This command must be run with root permissions. 

####status

ex. `airvpn status pavonis`

Display the status of the specified AirVPN server. This will display both the current bandwidth usage, and the number of 
users connected to the server.

####rules

ex. `sudo airvpn rules`

If you're routing all your traffic through a VPN, you need to be careful, because if the connection to the VPN drops (among other things), you're now on an unsecured 
connection, and you might never even know. To ensure all traffic that isn't destined for either your LAN, loopback, or 
VPN is dropped, you can set some rules in `iptables`. `airvpn rules` will output the rules in the form used by the `iptables-persistent`
application (which you'll likely need to install), for all configured AirVPN servers. The rules are stored in `/etc/iptables/rules.v4` 
by default. Thus, if this is something you want, run `airvpn rules > /etc/iptables/rules.v4`. It will only make IPv4 rules, because, to my knowledge, AirVPN doesn't support IPv6. This command requires your LAN IP block 
(`192.168.1.0/24` by default), your physical interface name (`eth0` by default), and your virtual interface name (`tun0` by default). 
These can be changed with the `--lan-ip-block`, `--interface` and `--virtual-interface` options, respectively.

This command must be run with root permissions.

####Why are some commands kind of slow?

They're slow because while AirVPN does have an API, it lacks some required functions, and as such things are getting 
done the old fashioned way.


####What doesn't it do?

The only real restriction this has at the moment is that the configuration it generates is opinionated. All configurations
generated use UDP, and port 443, without the possibility of configuring a proxy (ie. because this is what I use). If you
think this is ridiculous, well, this is GitHub, so maybe you should do something about it.
