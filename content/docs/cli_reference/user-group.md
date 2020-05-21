## dctl user group

Manage groups, including creating, editing, listing, and deleting groups, as well as displaying information about specific groups.

### Syntax

    dctl [global options] user group <command> [command options] [arguments...]

### Commands

```
  create            Create a group.
  edit              Edit a group.
  delete            Delete a group.
  get               Display information about a specific group.
  list              Display a summary of all groups.
```

### Options

```
  --help, -h        Show help.
```

## dctl user group create

Create a group.

### Syntax

    dctl [global options] user group create <group-name> --role-list <role-list> --external-group <external-group>

### Options

```
  --role-list <role-list>,            (Optional) The list of roles associated
     -r <role-list>                   with the group, separated by commas.
  --external-group <external-group>   (Optional) The principal group name 
                                      of the externally authenticated and
                                      managed group whose users, when
                                      authenticated, are associated with 
                                      the user group.
```

### Example

    dctl user group create group01 
       --role-list network-view,container-edit/namespace01

## dctl user group edit

Edit a group.

### Syntax

    dctl [global options] user group edit <group-name> --role-list <role-list> --external-group <external-group>

### Options

```
  --role-list <role-list>,            (Optional) The list of roles associated
     -r <role-list>                   with the group, separated by commas.
  --external-group <external-group>   (Optional) The principal group name 
                                      of the externally authenticated and
                                      managed group whose users, when
                                      authenticated, are associated with 
                                      the user group.
```

### Example

    dctl user group edit group01 --role-list cluster-view,user-edit

## dctl user group delete

Delete a group.

### Syntax

    dctl [global options] user group delete <group-name> [command options] 
       [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl user group delete group01

## dctl user group get

Display information about a specific group.

### Syntax

    dctl [global options] user group get <group-name> [arguments...]

### Example

    dctl user group get group01

### Output

```
  Name                  The name of the group.
  Built-in              Specifies whether the group is built-in/local (true) 
                        or custom (false).
  Role List             The list of roles associated with the group.
  External Group        The externally managed and authenticated group in
                        principal name format.
```

## dctl user group list

Display a summary of all groups.

### Syntax

    dctl [global options] user group list [arguments...]

### Example

    dctl user group list

### Output

```
  Name                  The name of the group.
  Built-in              Specifies whether the group is built-in/local (true) 
                        or custom (false).
  Role List             The list of roles associated with the group.
  External Group        The externally managed and authenticated group in
                        principal name format.

```
