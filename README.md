# VICINITY-AAU-VAS-Optimal-Scheduling-and-Operation-Energy-Management
This documentation describes the adapter of AAU VAS - Optimal Scheduling and Operation Energy Management.

# Infrastructure overview

The energy consumption data is collected through an emulated residential microgrid which includes PV, wind turbine and battery, and GORENJE smart oven and refrigerator. A LabVIEW-based energy management system is developed to achieve optimized control for energy resources and local loads and to perform load-scheduling function. The Optimal Scheduling and Operation Energy Management VAS subscribes to the event published by GORENJE appliances and send actions (baking and delay) to the GORENJE appliances.  
Adapter serves as the interface between VICINITY and LabVIEW enabling to use all required interaction patterns.

![Image text](https://github.com/YajuanGuan/pics/blob/master/OptimalScheduling&OperationEnergyManagement.png)

# Configuration and deployment

Adapter runs on Python 3.6.

# Adapter changelog by version
Adapter releases are as aau_adapter_x.y.z.py

## 1.0.0
Start version, it works with agent-service-full-0.6.3.jar. The objective is to maintain power balance and reduce electricity cost by encouraging residential customers to shift loads according to the renewable energy generation and the time-dependent tariff. 
The VAS makes action requests to its agent to start oven baking function and start refrigerator fast freeze function. It can subscribe to the event of oven device status and get the properties of the refrigerator. 

# Functionality and API
## User can read the Active power consumption, power generation of wind turbine, power generation of PV, and the state of charge of batteries. 
### Endpoint:
            GET : /remote/objects/{oid}/properties/{pid}
### Return:
After executing GET method, a response can be received, for instance:  
properties/Load_ActivePower:  
{  
    "value": "1",  
    "time": "2018-11-10 11:30:29"  
}

properties/WT_ActivePower:  
{  
    "value": "2",  
    "time": "2018-11-10 11:30:29"  
}

properties/BMS_SoC:  
{  
    "value": "60%",  
    "time": "2018-11-10 11:30:29"  
}

properties/PV_ActivePower:  
{  
    "value": "3",  
    "time": "2018-11-10 11:30:29"  
}

## PUT GORENJE refrigerator property
### Endpoint:
            PUT : /remote/objects/{oid}/properties/{pid}
For PUT method request the following JSON is needed:  
{  
    "fastfreeze": "ON"  
}


## POST GORENJE oven baking parameters
### Endpoint:
            POST : /remote/objects/{oid}/actions/{aid}
For PUT method request the following JSON is needed:  
{  
"duration": "20",  
    "temperature": "150",  
    "heater_system": "hotair"  
}

