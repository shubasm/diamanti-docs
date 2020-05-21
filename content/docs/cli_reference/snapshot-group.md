## dctl snapshot-group

Manage snapshot groups, including creating, listing, and deleting snapshot groups, as well as displaying information about specific snapshot groups.

### Syntax

    dctl [global options] snapshot-group <command> [command options] [arguments...]
    
### Commands

```
  create            Create a snapshot group.
  list              Display a summary of all snapshot groups.
  get               Display information about a specific snapshot group.
  delete            Delete a snapshot group.
```

### Options

```
  --help, -h        Show help.
```

## dctl snapshot-group create

Create a snapshot group.

### Syntax

    dctl [global options] snapshot-group create <snapshot-group-name> 
       [command options] [arguments...]
    
### Options

```
  --source <volume-group>,             The parent volume group.
     --src <volume-group> 
  --copyParentPlexCount, --cp          Create snapshots with the same plex 
                                       count as the parent volumes. 
```

### Example

    dctl snapshot-group create snaphot-group01 --source vol-group01

## dctl snapshot-group list

Display a summary of all snapshot groups.

### Syntax
    dctl [global options] snapshot-group list [arguments...]

### Example

    dctl snapshot-group list

### Output

```
  Name                  The name of the snapshot group.
  Members               The member volumes in the snapshot group.
  Phase                 The phase of the snapshot group.
  Age                   The age of the snapshot group.
```

## dctl snapshot-group get

Display information about a specific snapshot group.

### Syntax

    dctl [global options] snapshot-group get <snapshot-group-name> 
       [command options] [arguments...]

### Example

    dctl snapshot-group get snapshot-group01

## dctl snapshot-group delete

Delete a snapshot group.

### Syntax

    dctl [global options] snapshot-group delete <snapshot-group-name> 
       [command options] [arguments...]

### Options

```
  --policy <policy>,          Set the delete policy for snapshot group, either 
     -p <policy>              deletemembers or retainmembers. 
  --assume-yes, -y            Assume yes for the confirmation prompt.
```

### Example
    dctl snapshot-group delete snap-group01 -p retain
