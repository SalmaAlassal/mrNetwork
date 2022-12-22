# Command Line Views

| View Name     | Prompt |Function|
|---------------|--------|--------|
|User View      | `<Huawei>`|In the user view, you can view the running status and statistics of the device.|
|System View    | `[Huawei]`|In the system view, you can set the system parameters of the device, and enter other function views from this view.|
|Interface View | `[Huawei-GigabitEthernet0/0/0]` <br> Or <br>`[Huawei-ui-console0]` <br> Or <br> `[Huawei-ui-vty0-4]`|In the interface view, you can configure interface parameters including physical attributes, link layer protocols, and IP addresses.|
|Protocol View  |`[HUAWEI-ospf-1]`|In routing protocol views, you can configure most routing protocol parameters. The routing protocol views include the OSPF view, and RIP view.

# IOS Navigation

|  Views        |	    Access Method  |Prompt	   |Exit Method|
|---------------|----------------------|---------- |------------|
|User View      |  Login                                  | `<Huawei>`|            |
|System View    |`<Huawei>system-view`                    | `[Huawei]`| `quit`    |
|Interface View |`[HUAWEI]interface interfaceName X/Y/Z` <br> `[Huawei]user-interface console 0`  <br>`[Huawei]user-interface vty [first-number] [ last-number ]` |`[HUAWEI-GigabitEthernetX/Y/Z] ` <br> `[Huawei-ui-console0]` <br> `[Huawei-ui-vty0-4]`|`quit`|
|Protocol View  | `[HUAWEI] protocolName`                 | `[HUAWEI-ospf-1]` |`quit`|

```
<Huawei>system-view 
Enter system view, return user view with Ctrl+Z.
[Huawei]
[Huawei]interface Ethernet 0/0/0
[Huawei-Ethernet0/0/0]quit
[Huawei]	
[Huawei]user-interface console 0
[Huawei-ui-console0]quit
[Huawei]	
[Huawei-ui-vty0]user-interface vty 0 4
[Huawei-ui-vty0-4]quit
[Huawei]ospf
[Huawei-ospf-1]
```

# Keyboard Shortcuts

| Command   |Function|
|-----------|--------|
| `CTRL+C`  | Stops performing current functions.|
| `CTRL+Z`  | Returns to the user view.|
| `CTRL+]`  | Stops incoming connections or redirects the connections.|
| `TAB`     | Completes any incomplete keyword that is entered.|

```
<Huawei>system-view
Enter system view, return user view with Ctrl+Z.
[Huawei]^z
//Ctrl+Z
<Huawei>
```

# Help Features

| Partial Help                             | Complete Help                         |
|------------------------------------------|---------------------------------------|
| `<Huawei> d?` <br> `<Huawei> display h?` | `<Huawei> ?` <br> `<Huawei> display ?`|


# Configuration Commands

| Command   |Function|
|-----------|--------|
|`<Huawei>system-view` <br> `[Huawei]sysname salma` <br> `[salma]` | Configure the Device Name.|
|`[R1-GigabitEthernet0/0/0]description message` |A description is configured for the interface. By default, an interface has no description.|


```
<Huawei>system-view 
Enter system view, return user view with Ctrl+Z.
[Huawei]
[Huawei]sysname salma
[salma]
```

```
[R1-GigabitEthernet0/0/0]description This interface connects to R3-G0/0/0
[R1-GigabitEthernet0/0/0]display this
[V200R007C00SPC600]
interface GigabitEthernet0/0/0
description This interface connects to R3-G0/0/0
ip address 10.0.13.1 255.255.255.0
```

# Configurations: View, Save, Copy, Delete

| Command   |Function|
|-----------|--------|
|`<Huawei>display version`   |View the software version and hardware information for the system.|
|`[Huawei-ui-console0] display this` <br> `[Huawei-ui-vty0] display this`|Displays the running configuration in the current view.|
|`<Huawei>dir`|View the file list stored on the current device.|
|`<Huawei>display saved-configuration`  |Display the saved-configuration file.|
|`<Huawei>display current-configuration`|Display the current configuration information.|
|`<Huawei>display startup`              |Display the startup configuration information.|
|`<Huawei>save`|Save the current configuration file.|
|`<Huawei>reset saved-configuration`    |Delete the configuration in the flash memory.|
|`<Huawei>reboot`                       |Restart the router.|

# CLI Clock Settings

| Command   |Function|
|-----------|--------|
|`<Huawei>clock timezone time-zone-name add HH:MM:SS`|Sets the time zone (Adds an offset to the UTC time).|
|`<Huawei>clock datetime HH:MM:SS YYYY-MM-DD`        |Sets the current time and date.|
|`<HUAWEI>clock daylight-saving-time`                |Sets the daylight saving time.|
|`<Huawei>display clock`                             |Displays the current date and clock setting.

```
<Huawei>clock timezone BJ add 08:00:00
<Huawei>clock datetime 10:20:29 2016-04-11
<Huawei>display clock
2016-04-11 10:20:48
Thursday
Time Zone(BJ) : UTC+08:00
```

# CLI Header Messages

| Command                                      | Function |
|----------------------------------------------|----------|
| `[Huawei]header login information "message"` | Sets the header that is displayed on a terminal when a user is authenticated by a device.|
| `[Huawei]header shell information "message"` | Sets the header that is displayed on a terminal after the user logs into the device.

```
[Huawei]header login information "welcome to huawei certification!"
[Huawei]header shell information "Please don't reboot the device!"
……
welcome to huawei certification!
Login authentication
Password:
Please don't reboot the device!
<Huawei>
```

# Line Console Configurations

| Command   |Function|
|-----------|--------|
| `[Huawei-ui-console0] idle-timeout [minutes] [seconds]`  |Set the timeout duration for disconnection from a user interface. If a user logs in to the device and does not perform an operation, the user interface is occupied unnecessarily. You can run the idle-timeout command to disconnect the user's terminal from the device.|
| `[Huawei-ui-console0]screen-length` | Sets the number of lines displayed on each terminal screen after a command is executed.|
|`[Huawei-ui-console0] history-command max-size [n]` | Sets the size of the history command buffer.

Set the size of the history command buffer to 20 & the timeout duration to 1 minute and 30 seconds.

```
<Huawei>system-view
[Huawei]user-interface console 0
[Huawei-ui-console0] history-command max-size 20
[Huawei-ui-console0] idle-timeout 1 30
```

# IP Address Configuration

| Command   | Function |
|-----------|----------|
|`<Huawei> display ip interface interfaceName X/Y/Z`| Displays the IP configuration and statistics on interfaces.|
|`[Huawei]interface interfaceName X/Y/Z` <br> `[Huawei-interfaceNameX/Y/Z]ip address IPAddress`|Configure an IP address for the interface.|
|`[Huawei-GigabitEthernet0/0/0] interface loopback 0` <br> `[Huawei-LoopBack0] ip address 1.1.1.1 32` |Configure a loopback interface.|

Configure an IP address of `10.0.12.1/24` on interface `G0/0/0` and an IP address of `1.1.1.1/32` on loopback interface `0`.

```
<Huawei>system-view
[Huawei]interface GigabitEthernet 0/0/0
[Huawei-GigabitEthernet0/0/0] ip address 10.0.12.1 255.255.255.0
[Huawei-GigabitEthernet0/0/0] interface loopback 0
[Huawei-LoopBack0] ip address 1.1.1.1 32
```

Another Example

```
<Huawei>system-view 
Enter system view, return user view with Ctrl+Z.

[Huawei]interface Ethernet 0/0/0	
[Huawei-Ethernet0/0/0]ip address 192.168.33.1 255.255.255.0

[Huawei-Ethernet0/0/0]display interface Ethernet 0/0/0
Ethernet0/0/0 current state : UP 
Line protocol current state : UP
Last line protocol up time : 2022-12-22 18:45:05 UTC-08:00
Description:
Route Port,The Maximum Transmit Unit is 1500
Internet Address is 192.168.33.1/24 -------------------------------------------> Notice that line
IP Sending Frames' Format is PKTFMT_ETHNT_2, Hardware address is 5489-986b-6c09
Last physical up time   : 2022-12-22 18:45:05 UTC-08:00
Last physical down time : 2022-12-22 18:39:11 UTC-08:00
Current system time: 2022-12-22 18:45:44-08:00
Hardware address is 5489-986b-6c09
    Last 300 seconds input rate 0 bytes/sec, 0 packets/sec
    Last 300 seconds output rate 0 bytes/sec, 0 packets/sec
    Input: 0 bytes, 0 packets
    Output: 60 bytes, 1 packets
    Input:
      Unicast: 0 packets, Multicast: 0 packets
      Broadcast: 0 packets
    Output:
      Unicast: 0 packets, Multicast: 0 packets
      Broadcast: 1 packets
    Input bandwidth utilization  :    0%
    Output bandwidth utilization :    0%

[Huawei-Ethernet0/0/0]
```

# Telnet Configuration

### Password Configurations

| Command   | Function |
|-----------|----------|
|`[Huawei-ui-vty0-4]authentication-mode password`      |Set authentication mode to password authentication. By default, a Telnet user must enter a password for authentication before login.|
|`[Huawei-ui-vty0-4]set authentication password cipher`|Set a ciphertext password.|

### Router
```
[Huawei]interface Ethernet 0/0/0
[Huawei-Ethernet0/0/0]ip address 10.1.1.1 24
[Huawei]user-interface vty 0 4
[Huawei-ui-vty0-4]authentication-mode password
[Huawei-ui-vty0-4]set authentication password cipher
Enter Password(<8-128>): huawei12
```

### PC
```
<Host>telnet 10.1.1.1
Trying 10.1.1.1 ...
Press CTRL+K to abort
Connected to 10.1.1.1 ...
Login authentication
Password:
Info: The max number of VTY users is 5, and the number
of current VTY users on line is 1.
The current login time is 2013-04-19 16:32:00.
<Huawei>
```

# CLI Command Levels

| User Level | Command    | Level Name        |Description|
|------------|------------|-------------------|-----------|
|    `0`     |0           |Visit level        |Commands of this privilege level include commands used for network diagnosis such as ping and tracert commands, and commands that are used to access a remote device such as a Telnet client.|
|    `1`     |0 and 1     |Monitoring level   |Commands of this level are used for system maintenance, including display commands.|
|    `2`     |0,1 and 2   |Configuration level|Commands of this privilege level are used for service configuration.|
|    `3-15`  |0,1,2 and 3 |Management level   |Commands of this privilege level are used to control basic system operations and provide support for services, including file system, FTP, TFTP download, user management, command privilege level setting, and debugging commands for fault diagnosis.|


| Command   | Function |
|-----------|----------|
|`[Huawei]command-privilege level [level] view [view-name] [command-key]`|Set the command level in a specified view.|


Set the privilege level of the save command to 3.

```
<Huawei> system-view
[Huawei]command-privilege level 3 view user save
```

# CLI Interface Permissions

| Command   | Function |
|-----------|----------|
|`[Huawei-ui-vty0-4] user privilege level [n]`|Configures the user level.|

Set the user level on the VTY0-4 user interface to 2.

```
<Huawei>system-view
[Huawei]user-interface vty 0 4
[Huawei-ui-vty0-4] user privilege level 2
[Huawei-ui-vty0-4] set authentication password cipher
Enter Password(<8-128>): huawei123
```

----------------------------------------------------





# Routing

# Static Routes

|Command          | Description |
|-----------------|-------------|
|`[Huawei]display ip routing-table` |To show the router's routing table.|
|`[Huawei]ip route-static Destination_Network Subnet_Mask <Exit interface>` <br> Or <br> `[Huawei]ip route-static Destination_Network Subnet_Mask <Next_Hop_IP_Address>`| To configure Static Route.|
|`[Huawei]ip route-static 0.0.0.0 0.0.0.0 [Destination_Network]` | To configure the default route. The command instructs the router to match all IP address and subnet masks and send the packets to `Destination_Network`.|
|`[Huawei]ip route-static Destination_Network Subnet_Mask <Exit interface> preference [n]` <br> Or <br> `[Huawei]ip route-static Destination_Network Subnet_Mask <Next_Hop_IP_Address> preference [n]`|To configure Floating Static Route.|


### Floating Static Routes

Floating static routes provide an alternative route in the event that the primary static route fails.

Specifies the preference of a static route. A smaller value indicates a higher preference.

The value is an integer that ranges from 1 to 255. The default value is 60.

### Default Static Routes

A default route defines where packets will be sent if no specific route for the destination network is listed in the routing table.

-------------------------------------------------------

# Switch Basic Configuration

| Command   | Function |
|-----------|----------|
|`[SWA-GigabitEthernet0/0/1] undo negotiation auto`|Configures an Ethernet interface to work in non-auto negotiation mode. By default, Ethernet interfaces work in auto-negotiation mode.|
|`[SWA-GigabitEthernet0/0/1] duplex full`|Set the duplex mode to full-duplex.|
|`[SWA-GigabitEthernet0/0/1] speed 100`  |Set the interface rate to 100 Mbit/s.|
|`[SWA]display interface interfaceName X/Y/Z`|Display interface running status and statistics.|
