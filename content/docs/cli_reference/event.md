## dctl event

Display events, and configure and show event policies.

### Syntax

    dctl [global options] event <command> [command options] [arguments...]

### Commands

```
  list              Display events. By default, the 50 most recent events 
                    are displayed.
  status            Display event policies.
  configure         Configure policies for events, such as the event retention 
                    period (in days).
```

### Options

```
  --help, -h        Show help
```

## dctl event list

Display events, and configure and show event policies.

### Syntax

    dctl [global options] event list [command options] [arguments...]

### Options

```
  --namespace <namespace>,             Display events related to the specified 
     --ns <namespace>                  namespace.
  --node <node-name>, -n <node-name>   Display events related to the specified 
                                       node (or "all" nodes).
  --pod <pod-name>, -p <pod-name>      Display events related to the specified 
                                       pod (or "all" pods).
  --volume <volume-name>,              Display events related to the specified 
     -v <volume-name>                  volume (or "all" volumes).
  --source <source-name>,              Display events related to the specified 
     -s <source-name>                  source, for example "scheduler".
  --severity <value>, --sev <value>    Filter by severity, for example "ERROR".
  --limit <number-of-events>,          Limit the number of events displayed, 
     -l <number-of-events>             up to 1000. The default value is 50.
  --offset <offset-value>,             Set the offset to start displaying 
     -o <offset-value>                 events from the number specified by 
                                       offset-value. For example, an 
                                       offset-value of 500 starts displaying 
                                       the 500th most recent event. The 
                                       default value is 0.
```

### Example

    dctl event list
    
### Output

```
  First-seen                When the event was first seen.
  Last-seen                 When the event was last seen.
  Count                     The number of times the event was seen.
  Severity                  The severity of the event.
  Name                      The name of entity responsible for the event.
  UUID                      The universally unique identifier of the entity.
  Kind                      The kind of event.
  Host                      The host on which the event occurred.
  Component                 The component related to the event.
  Reason                    The reason for the event.
  Message                   The event message.
```

## dctl event status

Display event policies.

### Syntax

    dctl [global options] event status [arguments...]

### Example

    dctl event status

### Output

```
  Retention Days            The number of days that events are retained.
  SNMP Enabled              Indicates whether SNMP is enabled.
```

## dctl event configure

Configure policies for events, such as the event retention period (in days).

### Syntax

    dctl [global options] event configure [command options] [arguments...]

### Options

```
  --retention-days <n>              The number of days to retain events. By 
                                    default, events are retained for 30 days.
  --snmp-enable=<true|false>        Enable SNMP traps (true or false). When 
                                    enabled, the Diamanti appliance 
                                    generates SNMPv2 traps containing all 
                                    information from event records. In 
                                    addition, the appliance supplies a 
                                    MIB file to install on the receiver to 
                                    interpret the traps (available at /usr/
                                    share/diamanti/mibs/DW-EVENT-MIB.txt).
  --snmp-community “<string>”       The SNMP community string (in double 
                                    quotes). The default is "public".
  --snmp-receiver=<ip-address-1     The IP addresses of the SNMP receivers 
     [,ip-address-2,ip-address-3]>  (up to three, separated by commas). This 
                                    is required when SNMP traps are enabled.
```

### Example

```
dctl event configure --retention-days 60 --snmp-enable=true 
   --snmp-receiver=172.16.6.105
   
dctl event configure --retention-days 30 --snmp-enable=true 
   --snmp-receiver=172.16.6.105,172.16.6.106,172.16.6.107
```
