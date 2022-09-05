# Configuration Register Settings

- The Configuration Register determines if the router is going to boot the IOS image from its Flash, TFTP server or just load the RXBoot image.

- Hexadecimal value represents the **16-bit configuration register value** that you want to use the next time the router is restarted. The value range is from `0x0` to `0xFFFF` (0 to 65535 in decimal).

- In the following example, the configuration register `0x2142` is used for Password Recovery procedures as it can **ignore the contents of NVRAM** :

   `Router(config)# config-register 0x2142`

**Configuration register boot field may differ from one device to another, so it will always be good to check it from Cisco website.**


# Password Recovery

The password recovery process can be rendered useless if the administrator has previously configured the router not to allow this process to take place. In this case, the router will warn the user and, if he proceeds, **all configuration will be erased, so there will be nothing to recover!**


### Example Scenario

- Consider we have a Cisco router, and we are unable to access it due to a lost password. Console and VTY (telnet) sessions ask for a password which we do not have.

- To initiate the password recovery procedure, connect the **rollover cable to the console port,** then power the router off and back on. As soon as you receive a prompt showing the boot process, hit `Ctrl + Break`:

```
System Bootstrap, Version 11.3(2)XA4, RELEASE SOFTWARE (fc1)
Copyright (c) 1999 by cisco Systems, Inc.
TAC:Home:SW:IOS:Specials for info
PC = 0xfff0a530, Vector = 0x500, SP = 0x680127c8
C2600 platform with 65536 Kbytes of main memory

program load complete, entry point: 0x80008000, size: 0xf54134
PC = 0xfff0a530, Vector = 0x500, SP = 0x83fffe68

<ctrl + Break>

monitor: command "boot" aborted due to user interrupt
rommon 1 >
```

- You'll immediately see the **rommon prompt**, indicating we are in **rom monitor mode**. This is a mini-IOS that allows you to perform very specific tasks in order to recover your router.

- Now, to skip our password-protected configuration, we instruct the router to **by-pass** the configuration located in **NVRAM** during boot up, and reset the router:

```
rommon 1 > confreg 0x2142
You must reset or power cycle for new config to take effect
rommon 2 > reset
```

- The router will now reset and start its normal boot up process, however, the current configuration will be ignored. When the bootup is complete, you will be prompted to **'enter the initial configuration dialog'**:

```
System Bootstrap, Version 11.3(2)XA4, RELEASE SOFTWARE (fc1)
Copyright (c) 1999 by cisco Systems, Inc.
TAC:Home:SW:IOS:Specials for info
C2600 platform with 65536 Kbytes of main memory
program load complete, entry point: 0x80008000, size: 0xf54134
Self decompressing the image : ##
<output omitted>
--- System Configuration Dialog ---
Would you like to enter the initial configuration dialog? [yes/no]: no
Press RETURN to get started!
```

- Next step is to enter 'Privileged Mode' and load the router's configuration **from nvram**. Then reset the 'enable' or 'secret' password. To be sure, we're showing how to reset both. In addition, we are going to reset the console port's password:

```
Router> enable
Router# copy startup-config running-config
Destination filename [running-config]? (hit enter)
Building configuration...
[OK]
Router# configure terminal
Router(config)# enable password cisco
Router(config)# enable secret abc
Router(config)# line console 0
Router(config-line)# password hello
Router(config)# username admin privilege 15 secret abc123
```

- If you use the 'login local' command you'll need to reset the user account of the password you have lost (in our example, it's 'admin').

- Lastly, we need to change the 'configuration register' so the router will load the newly modified configuration next time it reboots, save our settings and reboot the router:

```
Router(config)# config-register 0x2102
Router(config)# exit
Router# copy running-config startup-config   → or you can use wr command
Destination filename [startup-config]? (hit enter)
Building configuration...
[OK]
Router# reload
```

- The router will now reload and use the new configuration that contains the newly set passwords.

- When the router reboots, log in and check your configuration. If you find any interfaces in the 'shutdown' state, you'll need to use the 'no shutdown' command to bring them back up.

**Again, don't forget to save your configuration once all changes are complete!**