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
to the path of the python binary in your virutalenv. 

ie. If my name is waffles and I use `virtualenvwrapper` to create a virtualenv called `airvpn-cli`:

```shell
#!/home/waffles/.virtualenvs/airvpn-cli/bin/python

"""
AirVPN CLI.

...
```

####
