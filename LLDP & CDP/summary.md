## CDP Commands

|Command                      |Description|
|------------------------------|-----------|
|`R# show cdp`                 |It shows if CDP is enabled or not, also the timers, etc.|
|`R# show cdp neighbors`       |To see all **directly connected** neighbors. It will give you a nice brief summary view.|
|`R# show cdp neighbors detail`|It will show more verbose output, including the IP addresses configured on those devices.|
|`R(config)# no cdp run`       |To turn it off.|
|`R(config)# cdp run`          |To turn it back on again.|
|`R(config)# int g0/1` <br> `R(config-if)# no cdp enable`    | To disable it at the interface level.|
|`R(config)# cdp timer [seconds]` <br> `R(config)# cdp holdtime [seconds]`| To change the default time. <br> **Note that** they won't work on packet tracer.|
|`R# clear cdp table`          |Delete the CDP table of information about neighbors.|

## LLDP Commands

|Command                        |Description|
|-------------------------------|-----------|
|`R# show lldp`                 |It will show if LLDP is enabled or not. |
|`R# show lldp neighbors`       |It will show a summary of our neighbors.|
|`R# show lldp neighbors detail`|It will show more verbose output, including the IP addresses configured on those devices.|
|`R(config)# lldp run`          |To turn it on. |
|`R(config)# no lldp run`       |To turn it off.|
|`R(config-if)# no lldp transmit` <br> `R1(config-if)#no lldp receive` |To disable it at the interface level, we do it for both transmit and receive separately.|
|`R(config)# lldp timer [seconds]`  <br> `R(config)#lldp holdtime [seconds]`|To change the default time.|
|`R# clear lldp table`           |Delete the LLDP table of information about neighbors.|