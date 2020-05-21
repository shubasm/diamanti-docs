## dctl feature

Manage features, including enabling, diabling, and listing features, as well as displaying information about specific features.

### Syntax

    dctl [global options] feature <command> [command options] [arguments...]
    
### Commands

```
  enable            Enable a feature.
  disable           Disable a feature.
  list              Display a summary of all features.
  info              Display information about a specific feature.
```

### Options

```
  --help, -h        Show help.
```

## dctl feature enable

Enable a feature.

**Note:** The KVM feature is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] feature enable <feature-name>
    
### Supported Features

| Feature  | Feature Name  |
|---|---|
| Helm  | helm  |
| KVM  | kvm  |
| Storage overlay  | storage-overlay  |
| Secure volumes  | secure-volumes  |
    
### Example

    dctl feature enable helm

## dctl feature disable

Disable a feature.

### Syntax

    dctl [global options] feature disable <feature-name>
    
### Supported Features

| Feature  | Feature Name  |
|---|---|
| Helm  | helm  |
| KVM  | kvm  |
| Storage overlay  | storage-overlay  |
| Secure volumes  | secure-volumes  |
    
### Example

    dctl feature disable helm

## dctl feature list

Display a summary of all features.

### Syntax
    dctl [global options] feature list

### Example

    dctl feature list

### Output

```
  Name              The name of the feature.
  State             The state of the feature, either Enabled or Disabled.
```

## dctl feature info

Display information about a specific feature.

### Syntax

    dctl [global options] feature info <feature-name>

### Supported Features

| Feature  | Feature Name  |
|---|---|
| Helm  | helm  |
| KVM  | kvm  |
| Storage overlay  | storage-overlay  |
| Secure volumes  | secure-volumes  |
    
### Example

    dctl feature info secure-volumes
