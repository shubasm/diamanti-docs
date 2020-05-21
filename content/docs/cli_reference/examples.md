# Examples

This section provides example configuration files that can be used with dctl commands.

## Cluster Configuration File

This following is an example of a configuration file that can be used with the `dctl cluster create` command.

```
{
  "name": "cluster",
    "spec": {
        "config": {
            "adminUserPassword": "Fk#$yt+ew$KuHG*hvF",
            "certificateAuthority": "-----BEGIN CERTIFICATE-----
\nMIIFVTCCAz2gAwIBAgIJAP21KXcASURQMA0GCSqGSIb3DQEBCwUAMCUxIzAhBgNV\nBAMMGmRpYW1hbnRpLXNpZ25lckA
xNTI0NjQ1NzY5MB4XDTE4MDQyNTA4NDI0OVoX\nDTI4MDQyMjA4NDI0OVowJTEjMCEGA1UEAwwaZGlhbWFudGktc2lnbmVy
QDE1MjQ2\nNDU3NjkwggIiMA0GCSqGSIb3DQEBAQUAA4ICDwAwggIKAoICAQDbyFuhuRCVbqmj\nEqdVdqo3fQ0MsCchmn6
.
.
.
ltNTlNhIfosw4LdIUBSsMwNkyRPr5+Joccz5jlSQ4h4h2o\nkXuLa07f7pPK7tQjhfki4aKwZJxSV9CeTbxKYRMvLICdkf3
hDYLDmEaSNiWy8FDG\n76VeG6ZBZhT/9CM77HaqqCbZ/+GZRn3Mzg==\n-----END CERTIFICATE-----",
"podDnsDomain": "cluster.local",
"serverCertificate": "-----BEGIN CERTIFICATE-----
\nMIIE3DCCAsSgAwIBAgIBATANBgkqhkiG9w0BAQsFADAlMSMwIQYDVQQDDBpkaWFt\nYW50aS1zaWduZXJAMTUyNDY0NTc
2OTAeFw0xODA0MjUwODQzMDBaFw0yODA0MjIw\nODQzMDBaMBIxEDAOBgNVBAMMB2NsdXN0ZXIwggEiMA0GCSqGSIb3DQEB
AQUAA4IB\nDwAwggEKAoIBAQC6s8gcGvwhzsr0giTQHs40NRgpt6CfPmZLYkHRVV5Byk/
.
.
.
Um4h6cHBX64LijqCgfFcb+sG7sp+8SWvMDILaPqhnxq+lkUDZRKwXNwWpH+\nVCxl51Wz3COHJEuMhoquht2CV451bXF6vD
Ph2tFsdfrt60OQbvXVZ94Dd6ZMH78F\nVEcTEFsxkT0jn1rslxgdYkST93CpqvNfzL+WP1uzB0ee0N/
uB1cFFxZYekmJJMMc\n-----END CERTIFICATE-----",
"serverPrivateKey": "-----BEGIN PRIVATE KEY-----
\nMIIEvwIBADANBgkqhkiG9w0BAQEFAASCBKkwggSlAgEAAoIBAQC6s8gcGvwhzsr0\ngiTQHs40NRgpt6CfPmZLYkHRVV5
Byk/4giqRV351HPiE8vgbEwnCQ+MFF6haF+0n\nRbtZKm0wE5uxy7nSwTCeOjNOXf82xZ9YZKSJrXosF+7mkk9/
u1hNVn423MVeNsMj\nREmUjnF+SCohbL4TgPDySWartQxfmcYZr3BEjK8Ahy3ox16hQeyh5+95PTO7tOxD\na+TfwTXnULm
AyN2YPy+PJYu6KmbO3H048AeKkjBdSS8IDIzwYXr5GXVQlGIIR9KL\nbxcjKBCd54VtAJiG5JlWByISVRvtqHpooBM8DE8J
.
.
.
DWDvA1bdYn0pwNxWwXhtYuYQYmST2lx8o5tcENAowVAZx1u+dyt4ijH5U\nJQPCBEYIaPSW1w6Vp1jRSiKeINN2OUFqdYXy
CqAaYDoIntT+uiaBisX6A1eoblTt\nX7dnJDxU49hPl0C5QhImlIUcYQ==\n-----END PRIVATE KEY-----",
            "storageVlan": 500,
            "virtualIP": "172.16.20.251"
        },
        "nodes": [
            "appserv76",
            "appserv77",
            "appserv78"
        ]
      }
}
```
