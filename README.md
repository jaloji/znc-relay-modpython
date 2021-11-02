znc-relay-modpython
=============
znc-relay-modpython is a [python module](https://wiki.znc.in/Modpython) for [ZNC](https://github.com/znc/znc) to make a one way relay between two channels on different networks, only the content of the message is relayed and all messages are not relayed only those starting with !help (you can of course modify this according to your need).

It does exactly the same as this mIRC script:
```
on *:text:!help*:#channel-source:{ 
  if $network == network-source {
    scon -at1 if ($network == network-destination) && ($me ison #channel-destination) var % $+ cid = $!cid
    if %cid {
      scid %cid
      msg #channel-destination $1-
      scon -r
    }
  }
}
```

Requirements
------------
You need to have compiled ZNC with option ./configure --enable-python and active modpython.

Installation
-----
Place relay.py in ~/.znc/modules.

Usage
-----
These module parameters are required:
```
--network-source       ZNC-configured IRC network name where the messages came from
--channel-source       IRC channel (including #) where the messages came from
--network-destination  ZNC-configured IRC network name where you want to echo
--channel-destination  IRC channel (including #) where you echo messages
```

Exemple:
```
/msg *status LoadMod relay --network-source=IRC-Source --channel-source=#incoming-messages --network-destination=IRC-Dest --channel-destination=#Echo-messages
```

All required parameters should be passed on module load. Currently, no module commands to configure while module is loaded. Reload with new parameters if needed.
```
/msg *status UnloadMod relay
```
