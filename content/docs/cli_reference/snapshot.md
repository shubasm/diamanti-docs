## dctl snapshot

Manage snapshots, including listing and deleting snapshots, as well as displaying information about specific snapshots.

**Note:** Snapshot commands are not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] snapshot <command> [command options] [arguments...]
    
### Commands

```
  create            Create a snapshot.
  list              Display a summary of all snapshots.
  get               Display information about a specific snapshot.
  delete            Delete a snapshot
```

### Options

```
  --help, -h        Show help.
```

## dctl snapshot create

Create a snapshot.

### Syntax

    dctl [global options] snapshot create <snapshot-name> [command options] 
       [arguments...]
    
### Options

```
  --source <volume>, --src <volume>     The source volume for the snapshot.
  --mirror-count <value>, -m <value>    The mirror count. The default is 1.
  --prefix <prefix>, -p <prefix>        The prefix to add to the snapshot name.
  --selectors <value>, --sel <value>    The selectors to constrain the node 
                                        selection, using the following format: 
                                        [key|key=val][,key|key=val]*
```

### Example

    dctl snapshot create [snap1 | --prefix snap1] --src vol01

## dctl snapshot list

Display a summary of all snapshots.

### Syntax
    dctl [global options] snapshot list [arguments...]

### Example

    dctl snapshot list -s vol01

### Output

```
  Name        The name of the snapshot.
  Size        The size of the snapshot.
  Node        The node associated with the snapshot.
  Labels      The labels associated with the snapshot.
  Parent      The parent of the snapshot.
  Phase       The phase of the snapshot.
  Age         The age of the snapshot.
```

## dctl snapshot get

Display information about a specific snapshot.

### Syntax

    dctl [global options] snapshot get <snapshot-name> [command options] 
       [arguments...]

### Example

    dctl snapshot get snap01

### Output

```
  Name        The name of the snapshot.
  Size        The size of the snapshot.
  Node        The node associated with the snapshot.
  Labels      The labels associated with the snapshot.
  Parent      The parent of the snapshot.
  Phase       The phase of the snapshot.
  Age         The age of the snapshot.
```

## dctl snapshot delete

Delete a snapshot.

### Syntax

    dctl [global options] snapshot delete <snapshot-name> [command options] 
       [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example
    dctl snapshot delete snap01