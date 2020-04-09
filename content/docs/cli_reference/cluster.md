+++
title = "Cluster commands"
description = ""
weight = 2
+++
## dctl cluster

Manage clusters, including creating and destroying clusters. Use also to add and remove nodes in a cluster, as well as display the status 
of a cluster, among other operations.

### Syntax

    dctl [global options] cluster <command> [command options] [arguments...]

### Commands

```
  create            Create a cluster. Use only once in the lifecycle 
                    of the cluster.
  add               Add one or more nodes to the cluster.
  update            Update one or more nodes in the cluster.
  remove            Remove one or more nodes from the cluster.
  etcd-add          Add one or more nodes to the etcd cluster.
  etcd-remove       Remove one or more nodes from the etcd cluster.
  configure         Configure the cluster.
  export            Export the cluster configuration (JSON output format).
  destroy           Destroy the cluster. The command prompts for confirmation. 
                    Use with care; this action cannot be undone.
  status            Display basic cluster information and statistics of 
                    the cluster.
  info              Display minimal information about the cluster (for 
                    unauthenticated users).
```

### Options

```
  --help, -h        Show help
```
## dctl cluster create

Create a cluster.

### Syntax

    dctl cluster create <cluster-name> <node-name>[,<node-name>,...] 
       [command options] [arguments...]

### Options

```
  --virtual-ip <cluster-virtual-ip>,                 (Required) The IP address
     --vip <cluster-virtual-ip>                      for managing the cluster.
  --poddns-domain <cluster-name>[.company.domain],   (Required) The domain name
     --poddns <cluster-name>[.company.domain]        for the SkyDNS service for
                                                     all containers deployed 
                                                     in the cluster. The 
                                                     default is domain.com.
  --storage-vlan <vlan-id>, --svlan <vlan-id>        (Required) The virtual 
                                                     LAN ID (for intra-cluster 
                                                     storage communication, 
                                                     with jumbo frames 
                                                     enabled). The default 
                                                     value is 0 (disabled).
  --admin-password <password>, -p <password>         The password for the admin
                                                     user. If a password is not
                                                     specified in the command 
                                                     line, the command prompts 
                                                     for a password. The 
                                                     password needs to meet the
                                                     Unicode standard, and must
                                                     consist of at least 8 
                                                     characters, including at 
                                                     least one special 
                                                     character, one upper and 
                                                     lowercase character, and 
                                                     one number.
  --ca-cert <path-to-certificate>                    The certificate authority 
                                                     for the cluster.
  --tls-cert <path-to-certificate>                   The TLS certificate for 
                                                     the cluster.
  --tls-key <path-to-key-file>                       The TLS private key for 
                                                     the cluster.
  --multizone value                                  Enable or disable 
                                                     multizone support.
```

### Example

    dctl cluster create mycluster node-01,node-02,node-03 --vip 192.168.30.10 
       --poddns mycluster.diamanti.com --storage-vlan 2

## dctl cluster add

Add one or more nodes to the cluster.

### Syntax

    dctl [global options] cluster add <node-name>[,<node-name>,...] 
       [command options] [arguments...]

### Example

    dctl cluster add node-04

## dctl cluster update certificate

Update user-supplied certificates in a cluster.

### Syntax

    dctl [global options] cluster update certificate [command options] 
       [arguments...]

### Options

```
 --ca-cert <absolute-path>              (Required) The absolute path of the 
                                        certificate.
 --server-cert <absolute-path>          (Required) The absolute path of the 
                                        server certificate.
 --server-key <absolute-path>           (Required) The absolute path of the 
                                        key for the server certificate.
```

### Example

    $ dctl cluster update certificate --ca-cert sample_certs1/ca.crt 
       --server-key sample_certs1/server.key --server-cert sample_certs1/server.crt

## dctl cluster update software

Update the Diamanti software in the cluster.

### Syntax

    dctl [global options] cluster update software [command options] [arguments...]

### Options

```
 --image value, -i <file-path>             (Required) The absolute path of the 
                                           RPM image file on the master node.
 --node-list <node-list>, -l <node-list>   The list of nodes to update.
 --force, -f                               Force the software update.
 --no-reboot, --nr                         Skip reboot after the software 
                                           update.
 --abort-on-failure, -t                    Abort on software update failure.
 --no-drain, --nd                          Skip draining pods during software 
                                           update.
 --parallel-count <count>, -p <count>      The number of nodes to activate 
                                           image in parallel. The default is 1.
```

### Example

    dctl cluster update software --image 
       "/home/diamanti/diamanti-cx-2.0.1-1.x86_64.rpm"

## dctl cluster update status

Display the status of a Diamanti software update.

### Syntax

    dctl [global options] cluster update status [command options] [arguments...]

### Example

    dctl cluster update status

## dctl cluster remove

Remove one or more nodes from the cluster.

### Syntax

    dctl [global options] cluster remove <node-name>[,<node-name>,...] 
       [command options] [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl cluster remove node-04

## dctl cluster etcd-add

Add one or more nodes to the etcd cluster.

### Syntax

    dctl [global options] cluster etcd-add <node-name>[,<node-name>,...] 
       [command options] [arguments...]

### Example

    dctl cluster etcd-add node-04

## dctl cluster etcd-remove

Remove one or more nodes from the etcd cluster.

### Syntax

    dctl [global options] cluster etcd-remove <node-name>[,<node-name>,...] 
       [command options] [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Examples

    dctl cluster etcd-remove node-04

## dctl cluster configure

Configure the cluster.

### Syntax

    dctl [global options] cluster configure [command options] [arguments...]

### Options

```
  --storage-vlan [vlan-id],       (Required) The virtual LAN ID (for intra-
     --svlan [vlan-id]            cluster storage communication, frames 
                                  enabled). The default value is 0 (disabled).
  --master [new-node]             Migrate the master to a different node in 
                                  the cluster.
  --assume-yes, -y                Assume yes for the confirmation prompt.
```

### Examples

```
dctl cluster configure --svlan 22
dctl cluster configure --master appserv73
```
    

## dctl cluster export

Export the cluster configuration (in JSON file format).

### Syntax

    dctl [global options] cluster export [arguments...]
    
### Example

    dctl -o json cluster export

## dctl cluster destroy

Destroy the cluster. The command prompts for confirmation. Use with care; this action cannot be undone.

### Syntax

    dctl [global options] cluster destroy [command options] [arguments...]
    
### Options

```
  --delete-volumes     Delete the volumes on the cluster. If the volumes are 
                       not deleted, the volumes are imported when the cluster 
                       is next created.
```

### Example

    dctl cluster destroy 2d708d7d-dc20-11e6-84ea-a4bf01147774
    
## dctl cluster status

Display the status of the cluster.

### Syntax

    dctl [global options] cluster status [arguments...]

### Example

    dctl cluster status
    
### Output

```
  Cluster status
  Name                  The name of the cluster.
  UUID                  The universally unique identifier of the cluster.
  State                 The state of the cluster.
  Version               The Diamanti software version.
  Master                The name of the cluster master.
  Etcd State            The state of the quorum, from among the following:
                          - Healthy — The number of healthy quorum members is 
                               greater than the quorum size and the number of 
                               members in the etcd cluster is odd.
                          - Degraded — The number of healthy quorum members is 
                               greater than the quorum size and the number of 
                               members in the etcd cluster is even.
                          - NoFaultTolerance — The number of healthy quorum 
                               members is equal to the quorum size.
  Virtual IP            The cluster virtual IP address.
  Storage VLAN          The virtual LAN ID.
  Pod DNS Domain        The DNS server for the pod.
  
  Nodes status
  Name                  The DNS (short) name of the node.
  Node-Status           The status of the node.
  K8S-Status            The Kubernetes status of the node.
  Millicores            The used and available physical CPU cores (times 1000).
  Memory                The used and available memory.
  Storage               The used and available storage.
  IOPS                  The used and available input/output operations 
                        per second.
  VNICS                 The number of used and available virtual network 
                        interfaces.
  Bandwidth             The used and available bandwidth.
  Storage Controllers   The number of used and available storage controllers.
  (Total, Remote)
  Labels                The labels associated with the node.
```

## dctl cluster info

Report and save information about the cluster.

### Syntax

    dctl [global options] cluster info [command options] [arguments...]
    
### Options

```
  --quiet, -q                         Run the command in quiet mode.
  --save, -s                          Save the cluster and certificate 
                                      information, storing the 
                                      information in the .dctl.d and 
                                      .kube directories of the logged-in 
                                      user on the local machine. In 
                                      addition, the certificate authority 
                                      is embedded in the ~/.dctl.d/config 
                                      and ~/.kube/config files.
  --insecure,                         Skip verification of server certificate.
     --insecure-skip-tls-verify, -i   This indicates that user-supplied
                                      certificates were used to create the 
                                      cluster and the certificate authority 
                                      (ca.crt) is not available for the user. 
                                      This allows the user to configure dctl 
                                      to ignore server certificate validation 
                                      when issuing the dctl login command.
  --proxy, -p                         Configure proxy mode for Kubernetes.
  --assume-yes, -y                    Assume yes for the confirmation prompt.
  --ca-cert                           Display the CA certificate used by dctl.
  --k8s-ca-cert                       Display the CA certificate used by 
                                      kubectl.
   --all-servers                      Display a list of all cluster endpoints.
```

**Note:**
The command only works using the VIP or FQDN. When specifying the FQDN, DNS needs to be enabled in your environment. Note also that users can save the cluster and certification information for a single Diamanti D-Series appliance only at any given time.
