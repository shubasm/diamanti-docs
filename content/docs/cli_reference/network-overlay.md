## dctl network overlay

Manage private networks, including creating, listing, and deleting networks, as well as displaying information about specific private networks.

### Syntax

    dctl [global options] network overlay <command> [command options] [arguments...]

### Commands

```
  create                Create a private network.
  get                   Display information about a specific private network.
  list                  Display a summary of all private networks.
  join-namespaces       Merge namespaces.
  isolate-namespaces    Unmerge and isolate namespaces.
  list-namespaces       Display a summary of the namespaces.
  update                Update a private network.
  delete                Delete a private network.
```

### Options

```
  --help, -h    Show help
```

## dctl network overlay create

Create a private network.

### Syntax

    dctl [global options] network overlay create <overlay-network-name> 
       [command options] [arguments...]

### Options

```
  --subnet <subnet/class>, -s <subnet/class>   (Required) The subnet for 
                                               the network (in CIDR format).
  --overlay-nw=<network-name>                  The network on which to overlay
                                               the private network.
  --overlay-nw-group=<group-name>,             The network group name.
     -n=<group-name>
  --isolate-ns=<true|false>                    (Optional) Specifies whether to
                                               isolate the private network. 
                                               The default is true.
```

### Example

    dctl network overlay create pvt-network-1 --subnet 172.30.0.0/16
       --overlay-nw=blue --overlay-nw-group=group-blue --isolate-ns=false
       
**Note:**
The network specified for the overlay-nw parameter should already be created and have host-network enabled for it.

## dctl network overlay get

Display information about a specific private network.

### Syntax

    dctl [global options] network overlay get <network-name> [arguments...]

### Example

    dctl network overlay get pvt-network-1
    
### Output

```
  Name               The name of the network.
  Type               The type of network, either public or private.
  Subnet             The network subnet.
  Overlay-NW         The name of the overlay network.
  Isolate-NS         Indicates whether the namespace is isolated.
  Network-Group      The group associated with the network.  
```

## dctl network overlay list

Display a summary of all private networks.

### Syntax

    dctl [global options] network overlay list [arguments...]

### Example

    dctl network overlay list

### Output

```
  Name               The name of the network.
  Type               The type of network, either public or private.
  Subnet             The network subnet.
  Overlay-NW         The name of the overlay network.
  Isolate-NS         Indicates whether the namespace is isolated.
  Network-Group      The group associated with the network.  
```

## dctl network overlay join-namespaces

Policy to enable traffic forwarding across pods in the specified namespaces with overlay network interfaces.

### Syntax

    dctl [global options] network overlay join-namespaces <overlay-network-name> 
       <namespace-name-1>,<namespace-name-2>[,<namespace-name-3>] [command options]
       [arguments...]

### Example

    dctl network overlay join-namespaces pvt-network-1 ns1,ns2,ns3

## dctl network overlay isolate-namespaces

Policy to disable traffic forwarding across pods in the specified namespaces with overlay network interfaces.

### Syntax

    dctl [global options] network overlay isolate-namespaces 
       <overlay-network-name> <namespace-name> [command options] [arguments...]

### Example

    dctl network overlay isolate-namespaces pvt-network1 ns1

## dctl network overlay list-namespaces

Display the networking forwarding policy for namespaces using the overlay network.

### Syntax

    dctl [global options] network overlay list-namespaces <network-name> 
       [arguments...]

### Example

    dctl network list-namespaces pvt-network-1

### Output

```
  Name          The name of the namespace.
```

## dctl network overlay update

Update a private network.

### Syntax

    dctl [global options] network overlay update <overlay-network-name> 
       [command options] [arguments...]

### Options

```
  --set-default               Set the default private network.
  --clear-default             Clear the default private network.
```

### Example

    dctl network update overlay pvt-network-1 --set-default

## dctl network overlay delete

Delete a private network.

### Syntax

    dctl [global options] network overlay delete <network-name> [command options] 
       [arguments...]
    
### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl network overlay delete pvt-network-1
