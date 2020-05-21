## dctl network

Manage networks, including creating, listing, and deleting networks, as well as displaying information about specific networks.

**Note:** L2 networks are not supported with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] network <command> [command options] [arguments...]

### Commands

```
  create        Create a network.
  get           Display information about a specific network.
  list          Display a summary of all networks.
  update        Update a network.
  delete        Delete a network.
```

### Options

```
  --help, -h    Show help
```

## dctl network create

Create a network.

**Note:** Only overlay networks can be created on Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] network create <network-name> [command options] 
       [arguments...]

### Options

```
  --subnet <subnet/class>, -s <subnet/class>      (Required) The subnet for 
                                                  the network (in CIDR format).
  --start <ip-range-start>                        (Required) The starting 
                                                  address of the range of IP 
                                                  addresses to allocate to 
                                                  containers on the network.
  --end <ip-range-end>                            (Required) The final address 
                                                  of the range of IP addresses 
                                                  to allocate to containers on 
                                                  the network.
  --gateway <gateway>, -g <gateway>               The IP address of the 
                                                  gateway.
  --gateway-mac <gw-mac-address>                  The MAC address of the
                                                  gateway.
  --type <network-type>                           The type of network, for
                                                  example, storage.
  --vlan <vlan-id>, -v <vlan-id>                  The ID of the virtual LAN on 
                                                  which the subnet should be 
                                                  placed based on the network 
                                                  configuration.
  --annotations value, -a value                   The network annotations.
  --selectors <selector>, --sel <selector>        The node selector.
  --perf-tier <perf-tier>, -p <perf-tier>         The performance tier.
  --network-group <group-name>, -n <group-name>   The network group name.
  --zone <zone-name>, -z <zone-name>              The zone name.
  --set-default                                   Set as the default network.
```

### Example

    dctl network create blue -s 192.168.30.0/24 --start 192.168.30.101 
       --end 192.168.30.200 -g 192.168.30.1 -v 2

## dctl network get

Display information about a specific network.

### Syntax

    dctl [global options] network get <network-name> [arguments...]

### Example

    dctl network get blue
    
### Output

```
  Name                      The name of the network.
  Type                      The type of network.
  Start Address             The starting network IP address on the pool.
  Total                     The total number of IP addresses in the network.
  Used                      The number of IP addresses used in the network.
  Gateway                   The IP address of the network gateway.
  VLAN                      The VLAN identifier for the network.
```

## dctl network list

Display a summary of all networks.

### Syntax

    dctl [global options] network list [arguments...]

### Options

```
  --type <network-type>      The type of network, for example, storage.
```

### Examples

```
// List all networks
dctl network list

// List all storage networks
dctl network list --type storage
```

### Output

```
  Name                       The name of the network.
  Type                       The type of network.
  Start Address              The starting network IP address on the pool.
  Total                      The total number of IP addresses in the network.
  Used                       The number of IP addresses used in the network.
  Gateway                    The IP address of the network gateway.
  VLAN                       The VLAN identifier for the network.
```

## dctl network update

Update a network.

### Syntax

    dctl [global options] network update <network-name> [command options] 
       [arguments...]

### Options

```
  --set-default                                     Set the default network.
  --clear-default                                   Clear the default network.
  --network-group <group-name>, -n <group-name>     The network group name.
  --selectors <selectors>,                          The node selector for 
     --sel <selectors>                              host endpoints.
  --perf-tier <perf-tier>,                          The performance tier for
     -p <perf-tier>                                 host endpoints.
  --end <end-address>                               Update the end address to
                                                    extend the range.
```

### Example

    dctl network update blue --set-default

## dctl network delete

Delete a network.

### Syntax

    dctl [global options] network delete <network-name> [command options] 
       [arguments...]
    
### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl network delete blue

