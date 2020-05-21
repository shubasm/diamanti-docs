## dctl user

Manage users, including creating, editing, listing, and deleting users.

### Syntax

    dctl [global options] user <command> [command options] [arguments...]

### Commands

```
  create            Create a user.
  edit              Edit a user.
  delete            Delete a user.
  get               Display information about a specific user.
  list              Display a summary of all users.
  role              Role commands.
  group             Group commands.
  auth-server       Authentication server commands.
```

### Options

```
  --help, -h        Show help.
```

## dctl user create

Create a user.

### Syntax

    dctl [global options] user create <user-name> [command options] [arguments...]

### Options

```
  --local-auth                           Specifies that the user is to be 
                                         authenticated locally by validating 
                                         a supplied password against 
                                         credentials stored in the local 
                                         configuration. The default is false.
  --password <password>, -p <password>   The password associated with the user.
  --group-list <group-list>,             The list of groups to which the 
     -g <group-list>                     user belongs.
```

Note: Local groups defined in the Diamanti system are used to give users specific permissions. In contrast, remote groups are simply a collection of users and do not give users specific permissions. 

### Example

    dctl user create user01 --local-auth --password myPassw0rd! 
       --group-list group01,group02

## dctl user edit

Edit a user.

### Syntax

    dctl [global options] user edit <user-name> [command options] [arguments...]

### Options

```
  --local-auth                           Specifies that the user is to be 
                                         authenticated locally by  validating 
                                         a supplied password against 
                                         credentials stored in the local 
                                         configuration. The default is false.
  --reset-password, -r                   Reset password from input.
  --password <password>, -p <password>   The password associated with the user.
  --group-list <group-list>,             The list of groups to which the 
     -g <group-list>                     user belongs.
```

Note: Local groups defined in the Diamanti system are used to give users specific permissions. In contrast, remote groups are simply a collection of users and do not give users specific permissions.

### Example

    dctl user edit user01 --local-auth --group-list group01,group02 
       --reset-password --password myPassw0rd!

## dctl user delete

Delete a user.

### Syntax

    dctl [global options] user delete <user-name> [command options] [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl user delete myuser

## dctl user get

Display information about a specific user.

### Syntax

    dctl [global options] user get <user-name> [arguments...]

### Example

    dctl user get user01

### Output

```
  Name                  The name of the built-in or custom user.
  Built-in              Specifies whether the user is built-in (true) or 
                        custom (false).
  Local Auth            Indicates whether the user is authenticated locally 
                        by validating a supplied password against credentials 
                        stored in the local configuration.
  Group List            The list of groups associated with the user.
```

## dctl user list

Display a summary of all users.

### Syntax

    dctl [global options] user list [arguments...]

### Example

    dctl user list

### Output

```
  Name                  The name of the built-in or custom user.
  Built-in              Specifies whether the user is built-in (true) or 
                        custom (false).
  Local Auth            Indicates whether the user is authenticated locally 
                        by validating a supplied password against credentials 
                        stored in the local configuration.
  Group List            The list of groups associated with the user.
```

