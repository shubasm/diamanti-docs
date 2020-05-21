## dctl zone

Manage zones, including listing and updating zones, as well as displaying information about specific zones.

### Syntax

    dctl [global options] zone <command> [command options] [arguments...]
    
### Commands

```
  list              Display a summary of all zones.
  get               Display information about a specific zone.
  update            Update a zone.
```

### Options

```
  --help, -h        Show help.
```

## dctl zone list

Display a summary of all zones.

### Syntax
    dctl [global options] zone list [arguments...]

### Example

    dctl zone list

### Output

```
  Name                  The name of the zone.
  Capability            The capability of the zone.
```

## dctl zone get

Display information about a specific zone.

### Syntax

    dctl [global options] zone get <volume-group-name> [command options] 
       [arguments...]

### Example

    dctl zone get zone01

## dctl zone update

Update a zone.

### Syntax

    dctl [global options] zone update <zone-name> [command options] [arguments...]

### Options

```
  --capability value, -c value.        The capability of the zone.
```

### Supported Capability Values

| Capability  | Supported Values  |
|---|---|
| storage-scope  | isolated-node \| isolated-zone \| shared  |
| master-enabled  | true \| false  |
| storage  | true \| false  |

### Example

    dctl zone update zone1 --capability storage-scope=shared,
       master-enabled=true,storage=true
