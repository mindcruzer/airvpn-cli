AirVPN CLI
===========

This is hopefully going to turn into a one-stop-shop for connecting to AirVPN servers on Linux. To switch VPN servers, I'm fairly tired of

a) Going to airvpn.org     
b) Logging in    
c) Downloading the config file    
d) Opening up my terminal    
e) Copying over the file to /etc/openvpn, setting permissions    
d) Connecting    

I'd rather

a) Open my terminal    
b) Type: airvpn list    
c) Decide on a server    
d) Type: airvpn setup [some server] --connect    
e) Go make waffles    

Among other things, I just want an excuse to write some Python.
