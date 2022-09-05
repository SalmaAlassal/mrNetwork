### Configuring Passwords

|  Password Type |Commands|Mode|
|----------------|--------|----|
|Console Password| `R> en` <br> `R# config t` <br> `R(config)# line console 0` <br> `R(config-line)# password cisco` <br> `R(config-line)# login` |`Press RETURN to get started`. <br>  `User Access Verification` <br> `Password:`|
|Enable Password | `R> en` <br> `R# config t`<br> `R(config)# enable password 123`| `R> enable` <br> `Password:` <br> `R#`|
|Secret Password | `R> en`  <br> `R# config t` <br> `R(config)# enable secret 123ABC`|`R> enable` <br> `Password:` <br> `R#`|
| Aux Password   | `R> en` <br> `R# config t` <br> `R(config)# line aux 0` <br> `R(config-line)# password 123` <br> `R(config-line)# login`||
|Telnet Password |`R1> en` <br> `R1# config t` <br> `R1(config)# line vty 0 4` <br> `R1(config-line)# password cisco` <br> `R1(config-line)# login`|`R2# telnet 10.0.0.2`  <br> `Trying 10.0.0.2 ...Open` <br> `User Access Verification` <br> `Password:`  <br> `R2>`|

### Removing Passwords

|  Password Type |Commands|
|----------------|--------|
|Console Password|`R(config)# line console 0` <br> `R(config-line)# no login` <br> `R(config-line)# no password`  |
|Enable Password |`R(config)# no enable password`                                                                 |
|Secret Password |`R(config)# no enable secret`                                                                   |
|Aux Password    |`R(config) # line aux 0` <br> `R(config-line)# no login` <br> `R(config-line)# no password`     |
|Telnet Password |`R(config-line)# line vty 0 4` <br> `R(config-line)# no password`<br> `R(config-line)# no login`|

### Configuring User Account

| Commands       |Description|
|----------------|-----------|
|`router(config)# username salma password 789` <br> Or <br> `router(config)# username salma secret 123` <br> `router(config)# line console 0` <br> `router(config-line)# login local` | Create a user who will have a privilege level of 1 by default.|

|Command                    | Description |
|---------------------------|-------------|
|`R(config-line)#login`                    | Setting the password does not enable password authentication. You’ll need to tell the router to prompt incoming sessions on the console line to require a password.|
|`R(config-line)# login local`             |Authenticate all incoming sessions via the local username database (prompt incoming sessions to require a username and password).|
|`R(config)#service password-encryption`   | Encrypts both **current and future** passwords. All passwords configured on an IOS device, with the exception of the passwords configured with enable secret password, are stored in clear-text.|
|`R(config)#no service password-encryption`|Decrypts **future** passwords.|
|`R(config-line)#exec-timeout [Min] [Sec]` | To specify a different inactivity timer.|



### Privilege Level Security

| Command        |Description|
|----------------|-----------|
| `R> show privilege` <br> `R# show privilege` |Show the current privilege level.|
| `R(config)# enable secret level {level} {password}`|Configure different privilege level to a password.|

-----------------------------------------------------------------------