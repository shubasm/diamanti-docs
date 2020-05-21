# Explore the Diamanti CLI

Welcome to the Diamanti D-Series Command Line Interface Guide. This guide provides a comprehensive reference to the Diamanti command
line interface (CLI). The Diamanti CLI offers a set of commands that makes it easy to manage Diamanti D-Series clusters, nodes (appliances),
storage volumes, networks, and more.

**Note:**
Users issue standard Kubernetes commands to manage pods, containers, and other Kubernetes resources in the environment.

For information about installing and configuring the Diamanti appliance, see the _Diamanti D-Series Installation Guide_. Refer to the 
_Diamanti D-Series Quick Start Guide_ for details about creating a Diamanti cluster and performing initial configuration.

For more information about the Diamanti User Interface (UI), see the _Diamanti D-Series User Interface Guide_.

## Overview

The `dctl` utility allows users to configure, manage, and monitor objects in the Diamanti cluster.

**Note:**
Users need to download the Diamanti tools to run the Diamanti CLI on a local machine. For more information about downloading 
the tools, refer to the _Diamanti D-Series User Interface Guide_.

<a name="roles"></a>
### Understand Roles

The Diamanti software uses role-based access control (RBAC) to regulate access to resources within the environment. Users therefore need to be 
assigned specific roles to run `dctl` commands.

Each command described in this chapter includes the role needed to run the command (if applicable). In addition, users need to be assigned the 
following roles to run Kubernetes commands:

- `container-view/namespace` role to run the kubectl get and kubectl describe commands
- `container-edit/namespace` role to run all kubectl commands

Note that Diamanti roles include a qualifier, either view or edit. For example, the roles related to node commands are `node-view` 
and `node-edit`. The view qualifier applies to read-only operations while the edit qualifier indicates a read-write operation 
(such as creating or removing an object). Roles with an edit qualifier include view privileges for an object.

For more information about RBAC, see the `dctl user role` command.

### Synopsis

Configure and control the Diamanti cluster.

    dctl [global options] <command> [command options] [arguments...]

**Note:**
All commands, except the `dctl cluster create` and `dctl cluster info` commands, require users to be logged into the cluster (using the `dctl login` command).

<a name="commands"></a>
### Commands

```
     cluster                Cluster commands
     config                 Config commands
     diagnosticbundle       Diagnostic bundle commands
     drive                  Drive commands
     endpoint               Endpoint commands
     event                  Event commands
     feature                Feature commands
     login                  Provide credentials for authentication
     logout                 Logout from the current user session
     namespace              Manage namespace for the current user context; 
                            see also 'kubectl config current-context'
     network                Network commands
     node                   Node commands
     passwd                 Change password for the logged in user
     perf-tier              Performance tier commands
     snapshot               Snapshot commands
     snapshot-group         Snapshot group commands
     user                   User commands
     volume                 Volume commands
     volume-group           Volume group commands
     whoami                 Display user for the current session
     zone                   Zone commands
     help, h                Shows a list of commands or help for one command
```

### Global Options

```
   --debug                             Print additional information.
   --output <format>, -o <format>      Output response in the specified format,
                                       simple or json The default is 'simple'.
   --server <ip-address>,              The DNS (short) name or IP address of 
      -s <ip-address>                  the Diamanti server that is a member 
                                       of the cluster. Use when running the 
                                       command from a Linux, Windows, or 
                                       Mac-based machine. [$VIRTUAL_IP]
   --ca-cert <path-to-certificate>.    The path to the PEM-formatted 
                                       certificate authority to use for 
                                       server identify validation. 
                                       [$CA_CERT]
   --config <path-to-file>,            The path to the JSON or YAML cluster 
      -c <path-to-file>                creation configuration file 
                                       containing the cluster name, admin 
                                       user password, certificate authority, 
                                       server private key, storage VLAN, 
                                       virtual IP address, and list of nodes.
   --insecure, -i                      Perform operations in insecure mode 
                                       (ignore the ca.crt file).
   --dctlconfig <path>                 The dctl config path. The default is 
                                       /home/diamanti. [$DCTL_CONFIG]
   --timeout <seconds>                 The timeout for any dctl operation 
                                       (in seconds). The default is 30. 
                                       [$DCTL_TIMEOUT]
   --help, -h                          Show help.
   --version, -v                       Print the version.
```
