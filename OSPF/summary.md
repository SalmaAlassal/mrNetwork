# OSPF Basic Configuration

|Command                                                         |Description |
|----------------------------------------------------------------|------------|
|`R(config)#router ospf [Process ID]`                            |To get into the OSPF configuration.|
|`R(config-router)#network [IP Address] [Wildcard] area [Number]`|To enable OSPF on a Network (Advertise the networks that fall within this range in OSPF).|
|`R(config-router)#router-id [RID]`                              | Assigns RID.                          |
|`R(config-if)#ip ospf priority [Number]`                        |Changes router priority value.               |
|`R(config-if)#no ip ospf priority`                              |Changes router priority value to the default.|
|`R#clear ip ospf process`                                       |Clears the OSPF process. |

--------------------------------------------

# OSPF Hello & Dead Intervals

|Command                                          |Description                               |
|-------------------------------------------------|------------------------------------------|
|`R(config-if)#ip ospf hello-interval [n Seconds]`|Changes the hello interval.               |
|`R(config-if)#no ip ospf hello-interval`         |Changes the hello interval to the default.|
|`R(config-if)#ip ospf dead-interval [n Seconds]` |Changes the dead interval.                |
|`R(config-if)#no ip ospf dead-interval minimal hello-multiplier [n Seconds]`|Makes the router send n hello packets each second and the dead interval will be set to 1 second.|
|`R(config-if)#no ip ospf dead-interval minimal hello-multiplier [n Seconds]`|To disable it.|
 
--------------------------------------------

# Creating a Default Route in OSPF

|Command                                                |Description|
|-------------------------------------------------------|-----------|
|`R(config-router)#default-information originate`       |Advertise the default route to 0.0.0.0/0 only if a default route already exist in the routing table.|
|`R(config-router)#default-information originate always`|Always advertise the default route to 0.0.0.0/0.|

--------------------------------------------

# OSPF Troubleshooting

|Command                  |Description|
|-------------------------|-----------|
|`R#debug ip ospf packet` |Displays hello packets being sent and received on your router.|
|`R# debug ip ospf hello` | Displays hello packets being sent and received on your router. It also displays more information than the `R#debug ip ospf packet`.|
|`R#debug ip ospf adj`    | Displays information about OSPF adjacencies and authentication, including DR and BDR elections, sent and received hello packets, neighbor state transitions, and database description information. Refers to a specific adjacency event.|

--------------------------------------------
   
# Show Commands

|Command                  |Description|
|-------------------------|-----------|
|`R#show ip ospf int f0/0`|Displays information about specific OSPF-enabled interfaces.|
|`R#show ip ospf neighbor`|To see if your router has OSPF neighbors. When the state is full you know that the routers have successfully become neighbors.|
