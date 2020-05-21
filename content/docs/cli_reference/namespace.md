## dctl namespace

Manage the namespace for the current user context.

**Note:**
See also `kubectl config current-context`.

### Syntax

    dctl [global options] namespace <command> [command options] [arguments...]

### Commands

```
  list          List the namespaces for the current user context.
  set           Set the namespace when a user has access to multiple 
                namespaces on the Kubernetes cluster.
  get           Get the namespace for the current user context.
```

### Options

```
  --help, -h    Show help
```

## dctl namespace list

List the namespaces for the current user context.

### Syntax

    dctl [global options] namespace list [arguments...]

### Example

    dctl namespace list
    
### Output

```
  Name            The name of the namespace available to the current user.
```

## dctl namespace set

Set the namespace when a user has access to multiple namespaces on the Kubernetes cluster.

### Syntax

    dctl [global options] namespace set <namespace> [command options] [arguments...]

### Example

    dctl namespace set mynamespace

## dctl namespace get

Get the namespace for the current user context.

### Syntax

    dctl [global options] namespace get [command options] [arguments...]

### Example

    dctl namespace get
