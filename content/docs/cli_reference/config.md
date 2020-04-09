+++
title = "Configuration commands"
description = ""
weight = 3
+++

<a name="config"></a>

## dctl config

Generate cluster configuration files.

### Syntax

    dctl [global options] config <command> [command options] [arguments...]

### Commands

```
  set-cluster   Set the cluster configuration.
```

### Options

```
  --help, -h    Show help
```

## dctl config set-cluster

Manually generate a configuration file to access the Diamanti cluster. This command is equivalent to the `dctl -s [node ip] cluster info --save` 
command.

### Syntax

    dctl [global options] config set-cluster [command options] [arguments...]

### Options

```
  --api-version <version>                           (Required) The API version 
                                                    for dctl cluster 
                                                    configuration entry. The 
                                                    default is v1.
  --virtual-ip <cluster-virtual-ip>,                (Required) The IP address 
     --vip <cluster-virtual-ip>                     for managing the cluster.
  --certificate-authority <certificate-file>,       (Required) The path to the 
     --ca <certificate-file>                        certificate authority file 
                                                    whose contents are to be 
                                                    embedded in the 
                                                    configuration file.
  --k8s-certificate-authority <certificate-file>,   The path to certificate 
     --k8s-ca <certificate-file>                    authority file whose 
                                                    contents are to be 
                                                    embedded in the 
                                                    .kube/config file.
  --proxy, -p                                       The proxy mode for the 
                                                    Kubernetes API server.
  --insecure, -i                                    Specifies insecure mode 
                                                    for dctl operations 
                                                    (ignore the ca.crt file, 
                                                    if set).
  --dns <domain-name>, -d <domain-name>             The domain name for the 
                                                    cluster API server.
  --server <node-name>, -s <node-name>              The server endpoint to use 
                                                    for dctl operations.
  --server-list <node-name>[,<node-name>,...]       The server endpoint List 
                                                    to use for dctl operations.
```

### Example

    dctl config set-cluster mycluster --api-version v1 --virtual-ip 192.168.30.10 
       --ca /etc/diamanti/certs/ca.crt

<a name="drive"></a>
## dctl drive

Manage drives, including listing and formatting drives.

### Syntax

    dctl [global options] drive <command> [command options] [arguments...]

### Commands

```
  get           Display information about a specific drive.
  list          Display a summary of all drives in a cluster (default) or 
                a specific node.
  format        Format all drives on a specific node.
```

### Options

```
  --help, -h    Show help
```