## dctl node

Manage nodes, including discovering and listing nodes.

### Syntax

    dctl [global options] node <command> [command options] [arguments...]

### Commands

```
  inventory             Display an inventory of discovered Diamanti nodes.
  list                  Display a summary of all nodes.
  get                   Display information about a specific node.
  health                Display the health status of the node.
  network               Display the status of the management network and the 
                        network ports.
  label                 Manage labels associated with a node.
  rediscover            Rediscover a node to update the drive inventory.
```
### Options

```
  --help, -h            Show help
```

## dctl node inventory

Display an inventory of discovered Diamanti nodes.

### Syntax

    dctl [global options] node inventory [arguments...]

### Example

    dctl node inventory

## dctl node list

Display a summary of all nodes.

### Syntax

    dctl [global options] node list [arguments...]

### Example

    dctl node list

### Output

```
  Name                   The DNS (short) name of the node.
  Node-Status            The status of the node.
  K8S-Status             The Kubernetes status of the node.
  Millicores             The used and available physical CPU cores 
                         (times 1000).
  Memory                 The used and available memory.
  Storage                The used and available storage.
  IOPS                   The used and available input/output operations 
                         per second.
  VNICS                  The number of used and available virtual network 
                         interfaces.
  Bandwidth              The used and available bandwidth.
  Storage Controllers    The number of used and available storage controllers.
  (Total, Remote)
  Labels                 The labels associated with the node.
```

## dctl node get

Display information about a specific node.

### Syntax

    dctl [global options] node get <node-name> [arguments...]

### Example

    dctl node get node01

## dctl node health

Display the health status of the node.

### Syntax

    dctl [global options] node health <command> <node-name> [command options] 
       [arguments...]

### Options

```
  --help, -h    Show help
```

### Example

    dctl node health status node01


### Output
```
  General
  Hostname                  The name of the node.
  UUID                      The universally unique identifier of the node.
  Node Health               The health of the node.
  K8s Health                The Kubernetes health of the node.
  Schedulable               Whether the node is schedulable or not.
  Node State                The state of the node.
  
  Kubernetes Conditions
  OutOfDisk                 True if there is insufficient free space on the 
                            node for adding new pods, otherwise false.
  MemoryPressure            True if pressure exists on the node memory, that 
                            is if the node memory is low; otherwise false.
  DiskPressure              True if pressure exists on the disk size, that is 
                            if the disk capacity is low; otherwise false.
  Ready                     Whether the node is ready, from among the 
                            following:
                              - true if the node is healthy and ready to 
                                accept pods
                              - false if the node is not healthy and is not 
                                accepting pods
                              - unknown if the node controller has not heard 
                                from the node in the last 40 seconds
                              
  Power Supplies
  PS                        The power supply.
  Status                    The status of the power supply.
  Fan                       The status of the power supply fan.
  
  System Fans
  Fan                       The system fan.
  Status                    The status of the system fan.
```

## dctl node network

Display the status of the management network and the network ports.

### Syntax

    dctl [global options] node network <command> <node-name> [command options] 
       [arguments...]

### Options

```
  --help, -h    Show help
```

### Example

    dctl node network status node01

### Ouput
```
  General
  Hostname                  The name of the node.
  UUID                      The universally unique identifier of the node.
  
  Management Network
  Name                      The name of the host or interface.
  IP Address                The IP address of the host or interface.
  MAC Address               The MAC address of the host or interface.
  Gateway                   The gateway of the host or interface.
  Status                    The status of the host or interface.
  DNS                       The domain name servers associated with the host 
                            or interface.
  
  Network Ports
  Port                      The network port.
  Status                    The status of the network port.
```

## dctl node label

Manage labels associated with a node.

### Syntax

    dctl [global options] node label <node-name> <label=value> [command options] 
       [arguments...]

### Options

```
  --overwrite, -o       Overwrite a label.
```
### Examples

```
// Add a label to a node
dctl node label node01 node=web-tier

// Overwrite a label
dctl node label node01 node=db-tier -o

// Remove a label from a node
$ dctl node label node01 node-
```

## dctl node rediscover

Rediscover a node to update the drive inventory.

### Syntax

    dctl [global options] node rediscover <node-name> [arguments...]

### Example

    dctl node rediscover node01


