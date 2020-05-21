## dctl diagnosticbundle

Manage Diamanti diagnostic bundles, including creating, deleting, and listing bundles, as well as displaying information about specific diagnostic bundles.

### Syntax

    dctl [global options] diagnosticbundle  <command> [command options] 
       [arguments...]
    
### Commands

```
  create            Create a diagnostic bundle.
  list              Display a summary of all diagnostic bundles.
  info              Display information about a specific diagnostic bundle.
  delete            Delete a diagnostic bundle.
```

### Options

```
  --help, -h        Show help.
```

## dctl diagnosticbundle create

Create a Diamanti diagnostic bundle.

### Syntax

    dctl [global options] diagnosticbundle create <issue> [command options] 
       [arguments...]
    
### Options

```
  --node value, -n value        Create a diagnostic bundle for a specific node.
```

### Example

    dctl diagnosticbundle create issue32

## dctl diagnosticbundle list

Display a summary of all diagnostic bundles.

### Syntax
    dctl [global options] diagnosticbundle list

### Example

    dctl diagnosticbundle list

### Output

```
  Name              The name of the diagnostic bundle.
  Labels            The labels associated with the diagnostic bundle.
```

## dctl diagnosticbundle info

Display information about a specific diagnostic bundle.

### Syntax

    dctl [global options] feature diagnosticbundle <bundle-name>

### Example

    dctl diagnosticbundle info issue32

## dctl diagnosticbundle delete

Delete a diagnostic bundle.

### Syntax

    dctl [global options] diagnosticbundle delete <bundle-name>
    
### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl diagnosticbundle delete issue32
