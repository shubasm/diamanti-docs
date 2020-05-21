## dctl user role

Manage roles, including listing roles, as well as displaying information about specific roles.

### Syntax

    dctl [global options] user role <command> [command options] [arguments...]

### Commands

```
  get               Display information about a specific role.
  list              Display a summary of all roles.
```

### Options

```
  --help, -h        Show help.
```

## dctl user role get

Display information about a specific role.

### Syntax

    dctl [global options] user group role <role-name> [arguments...]

### Example

    dctl user role get container-edit

### Output

```
  Name                  The name of the built-in or custom role.
  Built-in              Specifies whether the role is built-in (true) 
                        or custom (false).
  Object                The objects for which role methods are defined.
  Methods               The methods associated with the respective object.
```

## dctl user role list

Display a summary of all roles.

### Syntax

    dctl [global options] user role list [arguments...]

### Example

    dctl user role list

### Output

```
  Name                  The name of the built-in or custom role.
  Built-in              Specifies whether the role is built-in (true) 
                        or custom (false).
  Scope                 The scope of the role, either Cluster or Resource.
```
