## dctl perf-tier

Manage performance tiers, including creating, listing, and deleting templates, as well as displaying information about specific performance tiers.

**Note:** Performance tier commands are not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] perf-tier <command> [command options] [arguments...]

### Commands

```
  create        Create a performance tier.
  delete        Stop and delete the specified performance tier.
  get           Display information about a specific performance tier.
  list          Display a summary of all performance tiers.
```

### Options

```
  --help, -h    Show help.
```

## dctl perf-tier create

Create a performance tier.

### Syntax

    dctl [global options] perf-tier create <perf-tier> [command options] 
       [arguments...]

OPTIONS:

```
  --storage-iops <storage-iops>,        The input/output operations per second 
     -i <storage-iops>                  associated with the performance tier.
  --max-storage-iops <storage-iops>,    The maximum storage IOPS
     -I <storage-iops>                  (in kilobytes).
  --network-bw <network-bandwidth>,     The network bandwidth associated with 
     -b <network-bandwidth>             the performance tier.
  --max-network-bw value,               The maximum network bandwidth
     -B <network-bandwidth>             (in gigabytes).
  --labels <labels>, -l <labels>        The labels associated with the 
                                        performance tier, using the following 
                                        format: key=value.
```

### Example

    dctl perf-tier create perftier01 -i 1k -b 1G -l type=backend

## dctl perf-tier delete

Stop and delete the specified performance tier.

### Syntax

    dctl [global options] perf-tier delete <perf-tier> [command options] 
       [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl perf-tier delete perftier01

## dctl perf-tier get

Display information about a specific performance tier.

### Syntax

    dctl [global options] perf-tier get <perf-tier> [arguments...]

### Example

    dctl perf-tier get perftier01

### Output

```
  Name                      The name of the performance tier.
  Storage IOPS              The input/output operations per second associated 
                            with the performance tier.
  Network Bandwidth         The network bandwidth associated with the 
                            performance tier.
  Max Storage IOPS          The maximum storage IOPS.
  Max Network Bandwidth     The maximum network bandwidth.
  Labels                    The labels associated with the performance tier.
```

## dctl perf-tier list

Display a summary of all performance tiers.

### Syntax

    dctl [global options] perf-tier list [command options] [arguments...]
    
### Options

```
  --labels <labels>, -l <labels>     The labels associated with the 
                                     performance tier, using the following 
                                     format: key=value.
```

### Example

    dctl perf-tier list

### Output

```
  Name                      The name of the performance tier.
  Storage IOPS              The input/output operations per second associated 
                            with the performance tier.
  Network Bandwidth         The network bandwidth associated with the 
                            performance tier.
  Max Storage IOPS          The maximum storage IOPS.
  Max Network Bandwidth     The maximum network bandwidth.
  Labels                    The labels associated with the performance tier.
```
