AirVPN CLI
===========

Makes connecting to AirVPN servers in Linux a breeze (for me anyway).


**Note:** Because I'm pretty lazy, this has only been tested with Python 2.7


####Install

You have `openvpn` installed, right? Good.

Get the required python packages:

```shell
pip install docopt sh lxml requests texttable
```

If your `python` binary is located somewhere weird, change the first line of `airvpn` appropriately. 

Copy `airvpn` somewhere in your path (ex. `/bin`).


That's it. Open a terminal and type `airvpn -h` for help.


####Using with virtualenv

Do everything above (installing the python packages to your virutalenv, obviously). 

Next, open `airvpn` in a text editor, and change the first line 
to the path of the `python` binary in your virutalenv.

ex. If my name is waffles and I use `virtualenvwrapper` to create a virtualenv called `airvpn-cli`:

```shell
#!/home/waffles/.virtualenvs/airvpn-cli/bin/python

"""
AirVPN CLI.

...
```

####IPTables Rules

The only command that maybe isn't too self explanatory is `airvpn rules`. If you're routing all your traffic through
a VPN, you need to be careful, because if the connection to the VPN drops (among other things), you're now on an unsecured 
connection, and you might never even know. To ensure all traffic that isn't destined for either your LAN, loopback, or 
VPN is dropped, you can set some rules in `iptables`. `airvpn rules` will output the rules in the form used by the `iptables-persistent`
application (which you'll likely need to install), for all configured AirVPN servers. The rules are stored in `/etc/iptables/rules.v4` 
by default. Thus, if this is something you want, run `airvpn rules > /etc/iptables/rules.v4`. Yes,
it will only make IPv4 rules, because, to my knowledge, AirVPN doesn't support IPv6.


####Why are some commands kind of slow?
It's slow because ~~AirVPN doesn't have an API~~ while AirVPN does have an API, it lacks some required functions, and 
as such things are getting done the old fashioned way.


####What doesn't it do?

The only real restriction this has at the moment is that the configuration it generates is opinionated. All configurations
generated use UDP, and port 443, without the possibility of configuring a proxy (ie. because this is what I use). If you
think this is ridiculous, well, this is GitHub, so maybe you should do something about it.
