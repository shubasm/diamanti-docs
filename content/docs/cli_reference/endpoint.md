## dctl endpoint

Manage endpoints, including listing and deleting endpoints, as well as displaying information about specific endpoints.

**Note:** Endpoint commands are not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] endpoint <command> [command options] [arguments...]
    
### Commands

```
  create            Create a persistent endpoint.
  list              Display a summary of all endpoints.
  get               Display information about a specific endpoint.
  delete            Delete an endpoint.
```

### Options

```
  --help, -h        Show help.
```

## dctl endpoint create

Create a persistent endpoint. Note that creating a persistent endpoint does not assign a MAC address, SR-IOV Virtual Functions, or node. These settings are populated when the endpoint is attached to a container.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] endpoint create <endpoint-name> [command options] 
       [arguments...]
    
### Options

```
  --ip <ip-address>, -i <ip-address>            The IP address.
  --network <network-name>, -n <network-name>   The name of the network 
                                                associated with the endpoint.
  --labels <label>, -l <label>                  The labels associated with 
                                                the node.
  --namespace <namespace>, --ns <namespace>     The namespace for the 
                                                endpoint. The default value 
                                                is “default”.
```

### Example

    dctl endpoint create ep1 -n blue -ns default

## dctl endpoint list

Display a summary of all endpoints.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax
    dctl [global options] endpoint list [arguments...]

### Example

    dctl endpoint list

### Output

```
  Name                  The name of the endpoint.
  Namespace             The namespace associated with the endpoint.
  Container             The container associated with the endpoint.
  Network               The network associated with the endpoint.
  IP                    The IP address of the endpoint.
  MAC                   The MAC address of the endpoint.
  Gateway               The gateway associated with the endpoint.
  VLAN                  The VLAN associated with the endpoint.
  VF                    The virtual function associate with the endpoint.
  Node                  The node associated with the endpoint.
  Labels                The labels associated with the endpoint.
```

## dctl endpoint get

Display information about a specific endpoint.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] endpoint get <endpoint-name> [command options] 
       [arguments...]

### Options
```
  --namespace <namespace>,     The namespace for the endpoint. The default 
     --ns <namespace>          value is “default”.
```

### Example

    dctl endpoint get endpoint01

### Output

```
  Name                  The name of the endpoint.
  Namespace             The namespace associated with the endpoint.
  Container             The container associated with the endpoint.
  Network               The network associated with the endpoint.
  IP                    The IP address of the endpoint.
  MAC                   The MAC address of the endpoint.
  Gateway               The gateway associated with the endpoint.
  VLAN                  The VLAN associated with the endpoint.
  VF                    The virtual function associate with the endpoint.
  Node                  The node associated with the endpoint.
  Labels                The labels associated with the endpoint.
```

## dctl endpoint delete

Delete an endpoint.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] endpoint delete <endpoint-name> [command options] 
       [arguments...]

### Options

```
  --assume-yes, -y            Assume yes for the confirmation prompt.
  --force, -f                 Force delete the endpoint.
  --namespace <name>,         The namespace for the endpoint. The default 
     --ns <name>              value is “default”.
```

### Example
    dctl endpoint delete endpoint01
