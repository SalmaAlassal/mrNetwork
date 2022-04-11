# Banner

A banner is a message presented to a user who is using the Cisco device. Based on the type of banner you configured for use, the message will be shown to the users. Cisco IOS routers support a number of banners, such as:

- MOTD banner 
- Login banner
- Exec banner 


**Syntax:**  `R(config)#banner [motd | login | exec] [delimiting character]`

**To disable the banner :** `R(config)#no banner [motd] [login] [exec]`

----------------------------------------------------------------------------------

## MOTD banner

 It will be displayed before the user authenticates to our devices. It is typically used to display a temporary notice that may change regularly, such as system availability.
 
```
Router(config)#banner motd %
Enter TEXT message.  End with the character '%'.
************************************************
Attention!
We will be having scheduled system maintenance on this device.
************************************************
%
Router(config)#

```
 
 ```
Press RETURN to get started.

************************************************
Attention!
We will be having scheduled system maintenance on this device.
************************************************
Router>
````

**In this example, we use a question mark (%) as a delimiting character to indicate the start and stop of the banner configuration.**

**Another Example**

```
Router(config)#banner motd t
Enter TEXT message.  End with the character 't'.
Hi, have a nice time. t
````

```
Press RETURN to get started.
Hi, have a nice 

Router>
````
Be careful on choosing your delimiter character when configuring your banner, the banner must not have a delimiter character on its content, or else, the cisco ios will interpret it as an indicator to end the banner message.

-------------------------------------------
 
 ## Login banner

The Login banner will also be displayed before the user authenticates to our devices. It will show up after the MOTD banner. Unlike the MOTD Banner, it is designed to commonly display legal notices, such as security warnings and more permanent messages to the users.
 
 
 ```
Router(config)#line console 0
Router(config-line)#password 123
Router(config-line)#login
Router(config-line)#exit
Router(config)#banner login %
Enter TEXT message.  End with the character '%'.
Router(config)#banner login %
Enter TEXT message.  End with the character '%'.
* * * * * * * * * * W A R N I N G * * * * * * * * * *
              Warning text gammmed awii xD
* * * * * * * * * * * * * * * * * * * * * * * * * * *
%

Router(config)#
```


```
Press RETURN to get started.

* * * * * * * * * * W A R N I N G * * * * * * * * * *
               Warning text gammmed awii xD 
* * * * * * * * * * * * * * * * * * * * * * * * * * *

User Access Verification

Password: 
```
 
 -------------------------------------------

 # Exec banner

We use Exec banner to display messages after the users, or network administrators are authenticated to our Cisco IOS devices and before the user enters UserExec Mode. Unlike MOTD, the Exec banner is designed to be more of a permanent message and would not change frequently.
 
 
 ```
Router(config)#banner exec $
Enter TEXT message.  End with the character '$'.
**********************************************
              Salma For Networks xD
**********************************************
$
Router(config)#

```
 
 
```
Press RETURN to get started.


************************************************
Attention!
We will be having scheduled system maintenance on this device.
************************************************

* * * * * * * * * * W A R N I N G * * * * * * * * * *
              Warning text gammmed awii xD
* * * * * * * * * * * * * * * * * * * * * * * * * * *

User Access Verification

Password:
**********************************************
              Salma For Networks xD
**********************************************

Router>

```
 ---------------------------------
