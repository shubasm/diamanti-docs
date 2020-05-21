## dctl passwd

Change the password of the logged in user.

### Syntax

    dctl [global options] passwd [command options] [arguments...]

### Options

```
  --current-password <password>             The current password.
  --password <password>, -p <password>      The new password.
```

### Example

    dctl passwd --current-password myPassw0rd! --password newPassw0rd!