HOMEMATIC IP: Playground for some checklists

Connect HOMEMATIC IP GARAGE DOOR MODULE HmIP-MOD-TM
===================================================

How to connect
--------------

online:

  - unlearn the module from previous CCU, with reset to factory default
  - disconnect the module
  - rekeying: See below
  - connect the module
  - wait, it should connect


offline:

  - unlearn the module from previous CCU, with reset to factory default
  - disconnect the module
  - enter Key and SGTIN. FIXME: should the ``-`` separators be entered or not? Raspberrymatic accepts both without error message
  - connect the module
  - wait, it should connect

The vendor doc says that instead of disconnect/connect, we should press the button shortly before starting
learning mode. This does not seem to work reliably.

Meaning of LEDs
---------------
????? This is not documented by the vendor. At least I did not find it.

================== ===========================================================
short red          guessing: learning failed?
------------------ -----------------------------------------------------------
short green        guessing: learning succedeed?
------------------ -----------------------------------------------------------
constant yellow    guessing: learning mode active
================== ===========================================================


Reset to factory defaults
-------------------------
????? This is not documented by the vendor. At least I did not find it.


Rekeying
--------
This seems to transfer a module from one CCU to another.
How does it work? When is it needed? How long does it normally take?

Successful rekeying might look like this:
::

  Jan 6 01:19:05 de.eq3.cbcs.server.local.base.internal.HMIPTRXInitialResponseListener INFO  [Thread-6] Exchanging adapter from 3014F711A0001F58A9XXXXXX to 3014F711A061A7D3CXXXXXX ... 
  Jan 6 01:19:04 de.eq3.cbcs.server.local.base.internal.HMIPTRXInitialResponseListener INFO  [Thread-6] No NWK, try to set address ... 
  Jan 6 01:19:23 de.eq3.cbcs.server.local.base.internal.HMIPTRXInitialResponseListener INFO  [vert.x-eventloop-thread-1] Adapter exchange successful. 

Troubleshooting
---------------

Raspberry:
  - the Pi 4 disturbs homematic communication. Try a USB extension cable for the Homematic USB transceiver

Offline:

  - it seems that the key and the sgtin either do not have a checksum or that they are not checked by Raspberrymatic


Online:

  - When using raspberrymatic:

    - activate ssh login
    - login with ssh
    - ping homematic.com

  - is there a firewall rejecting outgoing connections to port 8443?

More questions
--------------

How are these files used by Raspberrymatic in this context? They seem to contain data of known modules.

==================================== ==================================================================
/etc/config/hmip_address.conf
------------------------------------ ------------------------------------------------------------------
/etc/config/hmip_networkkey.conf
------------------------------------ ------------------------------------------------------------------
  etc/config/crRFD/*                 info about known modules?
==================================== ==================================================================
