## dctl user auth-server

Manage authentication servers, including creating, listing, and deleting authentication servers, as well as displaying information 
about specific authentication servers.

### Syntax

    dctl [global options] user auth-server <command> [command options] 
       [arguments...]

### Commands

```
  create            Create the specified authentication server.
  edit              Edit the specified authentication server.
  delete            Delete the specified authentication server.
  get               Display information about a specific authentication server.
  list              Display a summary of all authentication servers.
```

### Options

```
  --help, -h        Show help
```

## dctl user auth-server create

Create the specified authentication server.

### Syntax

    dctl [global options] user auth-server create <auth-server-name> 
       --server <dns-name> --port <port-number> 
       --base-dn ‘dc=<name>,[dc=<name>,...]’ 
       --bind-dn 'cn=<name>[,dc=<name>[,dc=<name>...]]' 
       --bind-password '<bind-password>' 
       --user-filter '<filter>' [--group-name-attr ‘<name>’] 
       [--enable] [--usessl] [--cacert <cacert>]

### Options

```
  --server <dns-name> , -S <dns-name>       The DNS name or IP address of the 
                                            authentication server. Use a DNS
                                            name with certificates.
  --port <port-number>, -p <port-number>    The port number of the 
                                            authentication server.
  --base-dn ‘dc=<name>,[dc=<name>,...]’     The list of domain components for 
     -l ‘dc=<name>,[dc=<name>,...]’         the authentication server.
  --bind-dn 'cn=<name>[,dc=<name>           The bind distinguished name (DN)
     [,dc=<name>...]]'                      for the authentication server.
  --bind-password '<bind-password>'         The password for bind.
  --user-filter '<filter>'                  The LDAP query used to identify 
                                            the unique user record.
  --enable                                  Enable the authentication server.
  --usessl                                  Use SSL when communicating with 
                                            the authentication server.
  --cacert <cacert>                         The CA certificate to use to 
                                            connect to the authentication 
                                            server.
```

<div class="pagebreak"></div>
### Example

    dctl user auth-server create ldap-auth -S ds1.example.com --port 636 
       --base-dn 'CN=Users,DC=example,DC=com' 
       --bind-dn 'CN=Administrator,CN=Users,DC=example,DC=com' 
       --bind-password '111Password' --user-filter '(sAMAccountName=%s)' 
       --usessl --cacert windows-ca.crt
       
    // Non-secured example
    dctl user auth-server create ldap-auth -S ds1.example.com --port 389
       --base-dn 'CN=Users,DC=example,DC=com'
       --bind-dn 'CN=Administrator,CN=Users,DC=example,DC=com'
       --bind-password '111Password' --user-filter '(sAMAccountName=%s)'

## dctl user auth-server edit

Create the specified authentication server.

### Syntax

    dctl [global options] user auth-server create <auth-server-name> 
       --server <dns-name> --port <port-number> 
       --base-dn ‘dc=<name>,[dc=<name>,...]’ 
       --bind-dn 'cn=<name>[,dc=<name>[,dc=<name>...]]' 
       --bind-password '<bind-password>' 
       --user-filter '<filter>' [--group-name-attr ‘<name>’] 
       [--enable] [--usessl] [--cacert <cacert>]

### Options

```
  --server <dns-name>                       The DNS name of the authentication 
                                            server.
  --port <port-number>                      The port number of the 
                                            authentication server.
  --base-dn ‘dc=<name>,[dc=<name>,...]’     The list of domain components for 
                                            the authentication server.
  --bind-dn 'cn=<name>[,dc=<name>           The bind distinguished name (DN)
     [,dc=<name>...]]'                      for the authentication server.
  --bind-password '<bind-password>'         (Mandatory) The password for bind.
  --user-filter '<filter>'                  The LDAP query used to identify 
                                            the unique user record.
  --enable                                  Enable the authentication server.
  --usessl                                  Use SSL when communicating with 
                                            the authentication server.
  --cacert <cacert>                         The CA certificate to use to 
                                            connect to the authentication 
                                            server.
```

### Example

    dctl user auth-server edit ldap-auth --port 389 --bind-password 111Password

## dctl user auth-server delete

Delete the specified authentication server.

### Syntax

    dctl [global options] user auth-server delete <auth-server-name> 
       [command options] [arguments...]

### Options

```
  --assume-yes, -y     Assume yes for the confirmation prompt.
```

### Example

    dctl user auth-server delete ldap-auth

## dctl user auth-server get

Display information about a specific authentication server.

### Syntax

    dctl [global options] user auth-server get <auth-server-name> [arguments...]

### Example

    dctl user auth-server get ldap-auth

### Output

```
  Name                  The name of the authentication server.
  Server                The DNS name of the authentication server.
  Port                  The port number of the authentication server.
  Base                  The base domain name of the authentication server.
  BindDN                The bind distinguished name (DN) for the
                        authentication server.
  Filter                The authentication server` filter.
  Reachable             Indicates whether the authentication server is 
                        reachable, either true or false.
```

## dctl user auth-server list

Display a summary of all authentication servers.

### Syntax

    dctl [global options] user auth-server list [arguments...]

### Example

    dctl user auth-server list

### Output

```
  Name                  The name of the authentication server.
  Server                The DNS name of the authentication server.
  Port                  The port number of the authentication server.
  Enable                The current state of every authentication server.
  Domain                The domain for which the authentication server will 
                        authenticate users.
```

