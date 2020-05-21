## dctl volume

Manage volumes, including creating and deleting volumes, as well as listing volumes and showing information about specific volumes.

### Syntax

    dctl [global options] volume <command> [command options] [arguments...]

### Commands

```
  create                Create a volume.
  list                  Display a summary of all volumes.
  get                   Display information about a specific volume.
  describe              Describe a specific volume.
  update                Update a volume.
  plex-delete           Delete a mirror (plex) associated with a volume.
  restore               Restore a volume from a snapshot.
  rotate-key            Rotate the cluster-wide secure volumes encryption 
                        master key.
  set-transit-key       Set the transit or temporary encryption master key.
  remove-transit-key    Remove the transit or temporary encryption master key.
  delete                Delete a volume.
```

### Options

```
  --help, -h            Show help.
```

## dctl volume create

Create a volume.

### Syntax

    dctl [global options] volume create <volume-name> [command options] 
       [arguments...]

### Options

```
  -vg <volume-group-name>                   The name of the volume group (used
                                            for volume replication).
  --size <size>, -s <size>                  The size of the storage volume, 
                                            notated as nnM or nnG. For 
                                            example, 500M or 1G.
  --selectors <label>, --sel <label>        The node on which to create the 
                                            volume, selected by label using 
                                            the following format: key=value.
  --mirror-count <new-mirror-count>,        The new mirror count when adding  
     -m <new-mirror-count>                  a mirror to a volume (with one or 
                                            two mirrors). This value must be 
                                            one larger than the current mirror 
                                            count. Note that this option is
                                            not available for use with 
                                            Diamanti Virtual Clusters (DVX).
  --perf-tier <perf-tier>, -p <perf-tier>   The performance tier associated 
                                            with the volume.
  --fs-type <filesystem-type>,              The filesystem type for the volume.
     -f <filesystem-type>
  --labels <labels>, -l <labels>            The labels associated with the 
                                            volume, using the following 
                                            format: key=value.
  --source <snapshot-name>,                 The snapshot name to use to create 
     --src <snapshot-name>                  the volume. This option is only
                                            applicable when creating a volume
                                            from a snapshot.
  --alloc-ratio value, -a value             The allocation ratio for the 
                                            volume. This option is only 
                                            applicable when creating a volume 
                                            from a snapshot.
```

```
  --driver <driver>, -d <driver>            The driver for volume life cycle
                                            management.
  --block, -b                               Specifies the volume export mode 
                                            is block.
  --volumeuser <user>, -u <user>            The volume user, for example, 
                                            'kvm'.
  --secure, --sec                           Secures volume data at rest using 
                                            encryption.
```

### Examples

```
// Create a volume with size 1GB
dctl volume create vol01 -s 1Gi

// Create a volume with size 1GB associated with the volgrp01 volume group
dctl volume create vol01 -vg volgrp01 -s 1Gi

// Create a secure volume (with data at rest encrypted)
dctl volume create securevol05 --secure
```
## dctl volume list

Display a summary of all volumes.

### Syntax

    dctl [global options] volume list [command options] [arguments...]

### Options

```
  --labels <labels>, -l <labels>    The labels associated with the volume, 
                                    using the following format: key=value.
```

### Example

    dctl volume list

### Output

```
  Name                  The name of the volume.
  Size                  The size of the volume.
  Node                  The node or nodes (in case of mirroring) on which the 
                        volume resides.
  Labels                The labels associated with the volume.
  Phase                 The phase of the volume, either Pending or Available.
  Attach-Status         The status of the volume, from among the following: 
                          - Busy - attached to a container
                          - Available - for attachment
  Attached-To           The container to which the volume is attached.
  Device-Path           The device-path associated with the volume.
  Age                   The age of the volume.
```

## dctl volume get

Display information about a specific volume.

### Syntax

    dctl [global options] volume get <volume-name> [arguments...]

### Example

    dctl volume get vol01

### Output

```
  Name                  The name of the volume.
  Size                  The size of the volume.
  Node                  The node or nodes (in case of mirroring) on which the 
                        volume resides.
  Labels                The labels associated with the volume.
  Phase                 The phase of the volume, either Pending or Available.
  Attach-Status         The status of the volume, from among the following: 
                          - Busy - attached to a container
                          - Available - for attachment
  Attached-To           The container to which the volume is attached.
  Device-Path           The device-path associated with the volume.
  Age                   The age of the volume.
```

### Example to Identify a Secure Volume

    dctl -o json volume get securevolume01 | jq -r '.spec'

### Output

```
{
  "type": "Static",
  "size": 5000000000,
  "fsType": "ext4",
  "volumeMode": "Filesystem",
  "volumeUser": "default",
  "perfTier": "best-effort",
  "plexCount": 3,
  "thinProvision": true,
  "allocRatio": 100,
  "driver": "csi",
  "encryption": true
}
```

**Note:**
The key-value pair "encryption": true indicates a secure volume.

### Example to Get Secure Volume Encryption Configuration Information

The following shows an example of how to get the secure volume encryption information after the volume is attached or re-attached.

    dctl -o json volume get securevolume01 | jq -r '.status.encryptionConfig'

### Ouput

```
{
  "source": "dm-crypt",
  "keyStatus": "Active",
  "keyVersion": "v1",
  "keyDigest": "00d2bbe5b470990d7a916a8300b363b72e544788cbc60507a7dcff226634f3"
}
```

Note the following about the output:

- The keyVersion "v1" could be verified by fetching the Kubernetes secret object corresponding to the cluster-wide secure volumes encryption master key, as described below.
- The keyStatus set to "Active" indicates that the cluster-wide key is already applied against the secure volume. Otherwise, the keyStatus is set to "Pending" to reflect that the current version of cluster-wide key will be applied whenever the volume is attached or re-attached at a later time. 
- The temporary keyStatus setting "Transit" and keyVersion "v0" combination indicates that the secure volume is a candidate for migration from one cluster to another (through volume export and import). For more information about the Secure Volumes feature, refer to the _Diamanti D-Series Feature Guide: Secure Volumes_.

The following shows how to get the Kubernetes secret object corresponding to the cluster-wide secure volumes encryption master key:

```
$ kubectl -n diamanti-system get secrets volume-encryption-masterkey 
   -o json | jq -r '.data'
{
  "v1": "dFBPR1RXUzNiQzRFa0F3TW4xY29wY3V2b3Judk9NRlQ="
}
```

To fetch the cluster-wide secure volumes encryption master key corresponding to key version "v1", use the following command:

```
$ kubectl -n diamanti-system get secrets volume-encryption-masterkey 
   -o json | jq -r '.data.v1' | base64 -d
tPOGTWS3bC4EkAwMn1copcuvornvOMFT
```

To compute the sha256 checksum or digest corresponding to the above key/passphrase (to ensure that the correct key is applied against the secure volume) use the following command:

```
$ echo -n "tPOGTWS3bC4EkAwMn1copcuvornvOMFT" | sha256sum
00d2bbe5b470990d7a916a8300b363b7a72e544788cbc60507a7dcff226634f3  -

```

## dctl volume describe

Describe a specific volume.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume describe <volume-name> [arguments...]

### Example

    dctl volume describe vol01

### Output

```
  General
  Name                  The name of the volume.
  Size                  The size of the volume.
  Encryption            Indicates whether the volume is secured (true) or not
                        (false).
  Node                  The node or nodes (in case of mirroring) on which the 
                        volume resides.
  Labels                The labels associated with the volume.
  Node Selector         The node selector associated with the volume.
  Phase                 The phase of the volume, either Pending or Available.
  Attached-To           The container to which the volume is attached.
  Device-Path           The device-path associated with the volume.
  Age                   The age of the volume.
  Perf-Tier             The performance tier associated with the volume.
  Fs-Type               The type of file system used with the volume.
```

```
  Plexes
  Name                  The name of the plex.
  Nodes                 The nodes associated with the plex.
  State                 The state of the plex.
  Attach-State          The attach state of the plex.
  Condition             The condition of the plex.
  Out-of-sync-age       The out-of-sync age of the plex.
  Resync-Progress       The resynchronization progress of the plex.
```
### Example to Identify a Secure Volume

    dctl volume describe securevolume01

### Output

```
Name                                          : securevolume01
Size                                          : 21.51GB
Encryption                                    : true
Node                                          : [appserv18]
Label                                         : <none>
Node Selector                                 : node=node1
Phase                                         : Available
Status                                        : Available
Attached-To                                   :
Device Path                                   :
Age                                           : 10h
Perf-Tier                                     : best-effort
Mode                                          : Filesystem
Fs-Type                                       : ext4
Scheduled Plexes / Actual Plexes              : 1/1

Plexes:
          NAME                NODES       STATE     CONDITION   OUT-OF-SYNC-AGE   RESYNC-PROGRESS   DELETE-PROGRESS
          ----                -----       -----     ---------   ---------------   ---------------   ---------------
          securevolume01.p0   appserv18   Up        InSync
```

**Note:**
The <code>Encryption : true</code> line indicates a secure volume.

## dctl volume update

Update a volume.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume update <volume-name> [command options] 
       [arguments...]

### Options

```
  --size <size>, -s <size>                 The new size of the volume.
  --mirror-count <new-mirror-count>,       The new mirror count when adding a 
     -m <new-mirror-count>                 mirror to a volume (with one or two 
                                           mirrors). This value must be one 
                                           larger than the current mirror count.
  --overwrite, -o                          Overwrite labels.
  --selectors <labels>, --sel <labels>     The labels associated with the 
                                           volume, using the following 
                                           format: key=value.
  --cancel resize                          Cancel a resize operation.
  --fs-type <type>, -f <type>              The filesystem type for the volume 
                                           being exported in filesystem mode.
  --volumeuser <user>, -u <user>           The volume user, for example, 'kvm'.
```

**Note:**
Diamanti volumes need to be offline (detached) before resizing a volume. The volume remains in Pending state if the Diamanti node does not have enough storage to complete the operation. In this case, issue another volume update command to cancel the resize operation.

### Example

    dctl volume update vol01 -m 2 --sel label -s 2G

## dctl volume plex-delete

Delete a mirror (plex) associated with a volume.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume plex-delete <volume-name> p<plex-number> 
       [arguments...]

### Example

    dctl volume plex-delete vol01 p0

## dctl volume restore

Restore a volume from a valid point-in-time snapshot.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume restore [command options] [arguments...]

### Options

```
  --latest-snapshot, -l                 Restore a volume from the latest 
                                        snapshot. 
  --source-snapshot <snapshot-name>,    The source snapshot for the volume 
     -s <snapshot-name>                 restore.
  --assume-yes, -y                      Assume yes for the confirmation prompt.
```

### Examples

```
dctl volume restore vol01 --latest-snapshot
dctl volume restore vol02 --source-snapshot snap02
```    

**Note:** Diamanti volumes need to be offline (detached) before restoring from any point-in-time snapshot. All snapshots created after the snapshot being used for the volume restore are deleted after the restore operation has successfully completed. Volumes retain their size, in case the volume size is different from the snapshot size due to a volume resize operation.

## dctl volume rotate-key

Rotate the cluster-wide secure volumes encryption master key.

### Syntax

    dctl [global options] volume rotate-key [command options] [arguments...]

### Options

```
  --key-file value, --kf value      The file name containing the new secure 
                                    volumes encryption master key. The key 
                                    must be at least 8 characters and less 
                                    than 65 characters.
  --autogen, -a                     Auto-generate a new secure volumes 
                                    encryption master key.
```

### Examples

```
// Rotate the cluster-wide encryption master key without an admin-supplied key
$ dctl volume rotate-key --autogen
$ dctl -o json volume get securevolume01 | jq -r '.status.encryptionConfig'
// Alternatively...
$ dctl volume rotate-key
$ dctl -o json volume get securevolume01 | jq -r '.status.encryptionConfig'

// Rotate the cluster-wide encryption master key using a valid 
// admin-supplied key
$ cat /tmp/keyfile
ks7Pl6hiBbrrueo3245D0PJ9vaHq3EFu
$ dctl volume rotate-key --key-file /tmp/keyfile
```

**Note:**
The key file should not contain a newline character, and the key length should be a minimum
of 8 characters and a maximum of 64 characters. Diamanti recommends using the pwgen utility to generate the secure key or passphrase with the required length. The following shows an example, for reference:

```
$ printf "%s" $(pwgen -s 32 1) > /tmp/keyfile 2>&1
$ cat /tmp/keyfile
ks7Pl6hiBbrrueo3245D0PJ9vaHq3EFu
```

## dctl volume set-transit-key

Set the transit or temporary encryption master key to allow secure volume export or migration from a source cluster.

### Syntax

    dctl [global options] volume set-transit-key [command options] [arguments...]

### Options

```
  --key-file value, --kf value      The file name containing the new volume 
                                    encryption master key. The key must be 
                                    at least 8 characters and less than 65 
                                    characters.
```

### Example

```
// Set the transit or temporary encryption key against the secure 
// volume to migrate
$ printf "%s" $(pwgen -s 32 1) > /tmp/transitkey-file 2>&1
$ cat /tmp/transitkey-file
TysniXNOrrkU8MnSKRgFwDn8VwoQvVVA

$ dctl volume set-transit-key securevolume01 --key-file /tmp/transitkey-file
```

**Note:**
Setting a transit key against a secure volume results in the transit key being applied to all associated mirrors (plex). After a transit key is set on the volume, the volume cannot be accessed or attached in the same source cluster unless the transit key is removed and the cluster-wide encryption master key is re-applied. Setting a transit key against a secure volume means that it is a candidate for migration and is no longer needed in the original (source) cluster.

After setting the transit key, check the key status and version using the following command:

```
dctl -o json volume get <secure-vol-name> | jq -r
```

For example:

```
$ dctl -o json volume get securevolume01 | jq -r '.status.encryptionConfig'
{
  "source": "dm-crypt",
  "keyStatus": "Transit",
  "keyVersion": "v1",
  "keyDigest": "406bb007851e2f091fe5f98bd979fa937ae36940d7292712d8c86b23a0f536d9"
}
```

At this point, if the volume is not in Attached state, attach/re-attach the volume by starting/restarting the corresponding pod. This applies the transit key against the secure volume selected for migration. 

After attaching/re-attaching the volume, check the key status and version again using the same command as in the previous step. For example:

```
$ dctl -o json volume get securevolume01 | jq -r '.status.encryptionConfig'
{
  "source": "dm-crypt",
  "keyStatus": "Transit",
  "keyVersion": "v0",
  "keyDigest": "df172f1f3070617ac7950205d5509bc5de267f2273054f6a5da4187789d8390e"
}
```

Verify that the keyStatus indicates Transit and that the corresponding keyVersion is set to v0.

## dctl volume remove-transit-key

Remove the transit or temporary encryption master key to allow secure volume import on a target cluster.

**Note:** The transit key set against the secure volume in the source cluster needs to be supplied by the target cluster administrator.

### Syntax

    dctl [global options] volume remove-transit-key [command options] [arguments...]

### Options

```
  --key-file value, --kf value      The file name containing the new volume
                                    encryption master key. The key must be at 
                                    least 8 characters and less than 65 
                                    characters.
```

### Example

```
// Remove the transit or temporary key against the secure volume to be imported
// on the target cluster.
$ cat /tmp/transitkey-file
TysniXNOrrkU8MnSKRgFwDn8VwoQvVVA

$ dctl volume remove-transit-key securevolume01 --key-file /tmp/transitkey-file
$ dctl -o json volume get securevolume01 | jq -r '.status.encryptionConfig'
```

## dctl volume delete

Delete a volume.

### Syntax

    dctl [global options] volume delete [command options] [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
  --force, -f          Force delete the volume.
```

### Example

    dctl volume delete vol01

<a name="volume-group"></a>
## dctl volume-group

Manage volume groups, including creating, listing, and deleting volume groups, as well as displaying information about specific volume groups. In addition, you can add and remove volumes in volume groups.

**Note:** Volume group commands are not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume-group <command> [command options] 
       [arguments...]
    
### Commands

```
  create            Create a volume group.
  list              Display a summary of all volume groups.
  get               Display information about a specific volume group.
  add               Add volumes to an existing volume group.
  remove            Remove volumes from an existing volume group.
  delete            Delete a volume group.
```

### Options

```
  --help, -h        Show help.
```

## dctl volume-group create

Create a volume group.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume-group create <volume-group-name> 
       [command options] [arguments...]
    
### Options

```
  --members value, --mem value.        The member volumes.
  --source <snapshot-group>,           The source snapshot group.
     --src <snapshot-group> 
  --readonly, --ro                     Read-only member volumes. 
```

### Example

    dctl volume-group create vol-group01 --members vol01,vol02

## dctl volume-group list

Display a summary of all volume groups.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax
    dctl [global options] volume-group list [arguments...]

### Example

    dctl volume-group list

### Output

```
  Name                  The name of the volume group.
  Members               The member volumes in the volume group.
  Phase                 The phase of the volume group.
  Age                   The age of the volume group.
```

## dctl volume-group get

Display information about a specific volume group.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume-group get <volume-group-name> 
       [command options] [arguments...]

### Example

    dctl volume-group get volume-group01

## dctl volume-group add

Add volumes to an existing volume group.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume-group add <volume-group-name> 
       <volume-name>[,<volume-name>,...] [command options] [arguments...]
    
### Example

    dctl volume-group add vol-group01 vol01,vol02

## dctl volume-group remove

Remove volumes to an existing volume group.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume-group remove <volume-group-name> 
       <volume-name>[,<volume-name>,...] [command options] [arguments...]
    
### Example

    dctl volume-group remove vol-group01 vol01,vol02

## dctl volume-group delete

Delete a volume group.

**Note:** This command is not available for use with Diamanti Virtual Clusters (DVX).

### Syntax

    dctl [global options] volume-group delete <volume-group-name> 
       [command options] [arguments...]

### Options

```
  --assume-yes, -y            Assume yes for the confirmation prompt.
  --policy <policy>,          Set the delete policy for volume group, either 
     -p <policy>              deletemembers or retainmembers.    
```

### Example
    dctl volume-group delete vol-group01
