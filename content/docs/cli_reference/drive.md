## dctl drive

Manage drives, including listing and formatting drives.

### Syntax

    dctl [global options] drive <command> [command options] [arguments...]

### Commands

```
  get                  Display information about a specific drive.
  list                 Display a summary of all drives in a cluster (default)
                       or a specific node.
  format               Format all drives on a specific node.
  rotate-key           Rotate the cluster-wide drive key.
  set-transit-key      Set the transit key on all self-encrypting drives
                       in the specified node.
  remove-transit-key   Remove the transit key on all self-encrypting drives
                       in the specified node.

```

### Options

```
  --help, -h    Show help
```

## dctl drive get

Display information about a specific drive.

### Syntax

    dctl [global options] drive get [command options] [arguments...]

### Options

```
  --node <node-name>, -n <node-name>         (Required) The name of the node.
  --slot <slot-number>, -s <slot-number>     The slot number for the drive.
```

### Example

    dctl drive get -n node01 -s 0

## dctl drive list

Display a summary of all drives in a cluster (default) or a specific node.

### Syntax

    dctl [global options] drive list [command options] [arguments...]

### Options

```
  --node <node-name>, -n <node-name>        The name of the node.
```

### Example

    dctl drive list -n node01
    
### Output

```
  Node                The node associated with the drive.
  Slot                The slot in which the drive resides.
  S/N                 The serial number of the drive.
  Driveset            The drive set with which the drive is associated.
  Raw Capacity        The raw capacity of the drive.
  Usable Capacity     The usable capacity of the drive.
  Allocated           The current allocation of the drive.
  Firmware            The firmware of the drive.
  State               The state of the drive, from among the following:
                        - Up            — The drive is up.
                        - Down          — The drive is down because of 
                                          some failure.
                        - Missing       — The drive is missing from the 
                                          node (the drive was part of the 
                                          node, but was removed).
                        - Uninitialized — The drive is uninitialized. This 
                                          can happen when a new drive is 
                                          inserted in the server but has 
                                          not been added to Diamanti 
                                          storage.
                        - Foreign       — A drive from another node is 
                                          discovered in the node.
                        - Formatting    — The drive is being formatted.
  Self-Encrypted       The encryption state on the drive, among the following:
                         - No       - The drive does not support encryption.
                         - Locked   - Encryption configured, but read/write 
                                      access is disabled.
                         - Unlocked - Encryption configured, but read/write 
                                      access is enabled.
                         - Inactive - Encryption is supported by the drive, 
                                      but not configured.

```

## dctl drive format

Format all drives on a specific node.

**Note:** In the case of self encrypting drives (SED), the drives must be in factory reset state before using this command.

### Syntax

    dctl [global options] drive format [command options] [arguments...]

### Options

```
  --node <node-name>, -n <node-name>   (Required) The name of the node.
  --all, -a                            Format all drives on the node.
  --assume-yes, -y                     Assume yes for the confirmation prompt.
```

### Example

    dctl drive format -n node01 --all
    
### Performing an SED Factory Reset

Self encrypting drives must to be in factory reset state before formating the drives. To perform a factory reset of a drive, use the PSID password printed on the drive and enter the following command: 

    # sudo dstool -c "sedutil --factory_reset --drive <drive-slot> 
       --userid PSID --password <PSID-password>"

For example:

    # sudo dstool -c "sedutil --factory_reset --drive 0 
       --userid PSID --password A16C8E9B664A42C3328B033A7E800000"

## dctl drive rotate-key

Rotate the cluster-wide drive encryption master key.

### Syntax

    dctl [global options] drive rotate-key [command options] [arguments...]

### Options

```
  --key-file value, --kf value      The file name containing the drive key. 
                                    The key must be at least 8 characters 
                                    and less than 65 characters.
  --autogen, -a                     Auto-generate a new drive key.

```

### Example

```
// Rotate the cluster-wide drive key without an admin-supplied key
$ dctl drive rotate-key --autogen
// Alternatively...
$ dctl drive rotate-key

// Rotate the cluster-wide drive key using a valid admin-supplied key
$ cat /tmp/keyfile
ks7Pl6hiBbrrueo3245D0PJ9vaHq3EFu
$ dctl drive rotate-key --key-file /tmp/keyfile
```

**Note:**
The key file should not contain a newline character, and the key length should be a minimum
of 8 characters and a maximum of 64 characters. Diamanti recommends using the pwgen utility to generate the secure key or passphrase with the required length. The following shows an example, for reference:

```
$ printf "%s" $(pwgen -s 32 1) > /tmp/keyfile 2>&1
$ cat /tmp/keyfile
ks7Pl6hiBbrrueo3245D0PJ9vaHq3EFu
```

## dctl drive set-transit-key

Set the transit or temporary drive key to allow node migration from one cluster to other.

### Syntax

    dctl [global options] drive set-transit-key [command options] [arguments...]

### Options

```
  --key-file value, --kf value      The file name containing the new drive 
                                    key. The key must be at least 8 
                                    characters and less than 65 characters.
  --node <node-name>                The name of the node.

```

### Example

```
// Set the transit or temporary drive key for all drives in the migrating node.
$ printf "%s" $(pwgen -s 32 1) > /tmp/transitkey-file 2>&1
$ cat /tmp/transitkey-file
TysniXNOrrkU8MnSKRgFwDn8VwoQvVVA

$ dctl drive set-transit-key --key-file /tmp/transitkey-file --node node01
```

## dctl drive remove-transit-key

Remove the transit or temporary key, and set the cluster drive key on all drives in the specified node.

**Note:** The transit key set on drives in the source cluster needs to be supplied by the target cluster administrator.

### Syntax

    dctl [global options] drive remove-transit-key [command options] [arguments...]

### Options

```
  --key-file value, --kf value      The file name containing the transit
                                    drive key. The key must be at least 8
                                    characters and less than 65 characters.
  --node <node-name>                The name of the node.
```

### Example

```
// Remove the transit or temporary key, and set the cluster drive key on 
// all drives specified in the node.
$ cat /tmp/transitkey-file
TysniXNOrrkU8MnSKRgFwDn8VwoQvVVA

$ dctl drive remove-transit-key --key-file /tmp/transitkey-file --node node01
```
