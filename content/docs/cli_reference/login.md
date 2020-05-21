## dctl login

Log in to a cluster (from any node in the cluster) to perform authenticated operations.

There are two ways to log in to a cluster:

- Insecure mode — Use when user-supplied certificates were used to create the cluster and the certificate authority (ca.crt) is not available for the 
  user. This allows the user to configure `dctl` to ignore server certificate validation. This is the default login mode.
- Kubernetes proxy mode — In certain environments (such as with an SSL passthrough load-balancer), `kubectl` commands are not properly relayed to the 
  API server causing `kubectl` commands to fail with an error message. In these cases, use the proxy option, which relays `kubectl` commands through 
  the Diamanti server.

**Note:**
Before logging in to the cluster for the first time, users need to save the cluster configuration using the `dctl cluster info --save` command.
The command only works using the VIP or FQDN. When specifying the FQDN, DNS needs to be enabled in your environment. (See the [Examples](#examples) section.)

### Syntax

    dctl login [command options] [arguments...]

### Options

```
  --username <username>, -u <username>        The user name. The default 
                                              is "admin".
  --password <password>, -p password>         The password associated with 
                                              the user name.
  --namespace <namespace>, -n <namespace>     The namespace for the kubectl 
                                              context.
  --quiet, -q                                 Run the command in quiet mode.
  --proxy, --proxy-k8s                        Log in to the cluster using 
                                              Kubernetes proxy mode. The 
                                              default is false.
  --insecure                                  Enable insecure mode for 
                                              appliance API server requests. 
                                              The default is false.
  --insecure-k8s                              Enable insecure mode for 
                                              Kubernetes API server requests.
                                              The default is false.
```

### Example

    dctl login --user myuser --password myPassw0rd!

