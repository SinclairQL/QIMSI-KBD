MINERVA PS/2 KEYBOARD DRIVER FOR QIMSI
--------------------------------------
QIMSI is a new multifunctional peripheral for the Sinclair QL which plugs into the extension ROM slot. It offers mass storage though micro-SDHC cards, a PS/2 mouse interface, a PS/2 external keyboard interface and sampled sound output. Details can be found at https://qlforum.co.uk/viewtopic.php?t=4534, ordering info at https://qlforum.co.uk/viewtopic.php?t=4535.

The PS/2 keyboard interface works in conjunction with either SMSQ/E or the Minerva ROM. SMSQ/E 3.39 and later has inbuilt driver support but requires a Gold Card or Super Gold Card on the QL. For the Minerva ROM, the driver is provided here.

This keyboard driver does not work with the official Sinclair ROMs such as AH, JM, JS and MGx. The reason is that these ROMs lack the software hooks that Minerva provides for external keyboard interfaces. Moreover, they require you to press F1 or F2 at startup to continue into the boot process, which requires the presence of the original QL keyboard (or a hardware-based replacement). The Minerva ROM startup prompt has a timeout after which it automatically continues booting, without the need to access the original QL keyboard.

Precautions
-----------
First of all: read the QIMSI manual, in particular the section describing the keyboard interface.

QIMSI has a micro-USB keyboard connector, but currently only accepts keyboards which support the PS/2 protocol (either pure PS/2 or 'combo' standard). If you have a keyboard with PS/2 mini-DIN plug, you have to use a PS/2 to USB adapter cable to connect the keyboard to QIMSI (see https://en.wikipedia.org/wiki/PS/2_port). There are various such adapters around on the market, but they may not always work. The ones that will definitely *not* work are the *active* adapters that contain internal circuitry to convert the PS/2 signals to USB signals. They can usually be identified by having some sort of blob in the middle of the cable or in the plugs (those with both a mouse and keyboard connector on the PS/2 side are definitely active, since the two signals need to be combined into one USB signal). Yes, I've found out the hard way...

So, in that case, you will need a *passive* PS/2 to USB converter. They are pretty simple, containing only four wires. You can even build one yourself if you have sufficient soldering skills, using [this](https://pinoutguide.com/InputCables/usb_ps2_mouse_pinout.shtml) pinout guide. DISCLAIMER: If you manage to get the wiring wrong, permanent damage may result to QIMSI, your keyboard, or both. The responsibility is entirely yours!

Loading and activating the driver
---------------------------------
Simple as that: unzip the QIMSIKBD.ZIP file to your boot drive and put a line **LRESPR win1_QIMSIKBD_bin** in your BOOT file (if you still don't have Toolkit II, you have to use something like **a=RESPR(4096): LBYTES win1_QIMSIKBD_bin,a: CALL a**).

After this, you can control the driver using the following extra S\*BASIC commands:

- **KBD_PS2** to activate the external PS/2 keyboard (note that you need to explicitly issue this command to activate the external keyboard, it's not automatically done after loading)

- **KBD_QL** to switch back to the original QL keyboard

- **KBD_TABLE_PS2** *n* to change the keyboard layout, where *n* represents the telephone country code. Currently supported are 1 (US), 44 (UK), and 49 (German). At startup, it uses US keyboard layout.

These commands are identical to their SMSQ/E counterparts, so you can use them in your BOOT file regardless of which operating system is used.

Contributors
------------
The original driver was written by Richard Zidlicky for the Q68 and further developed by Jan Bredenbeek, who also ported it for use with QIMSI.

The QIMSI interface itself is designed by Peter Graf.
