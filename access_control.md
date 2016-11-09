# Access Control

Access Control Policies allow the Vault to strategically grant access to certain tokens, based on their policy which is defined when the Application, User, Token, etc. is created. Notice, it grants permission, that is because Vault has a whitelist policy on permissions, and defaults to deny all without ACL that grants the desired permissions. *While the default policy allows for some changes to be made, those are necessary to allow the user to renew, request a new token, or revoke their token.*

The Policies can be stored wherever, as the need to be loaded into the Vault before they can be assigned. The command below reads a Policy written in HCL into the Vault with the desired policy name.

`vault policy-write policy-name acl.hcl`

Some of the ACLs that we use are listed below for your reference, and a more detailed list can be found in the [Vault Documentation](https://www.vaultproject.io/docs/concepts/policies.html).

## Sample ACLs
### Admin
```
path "secret/*" {
  policy = "sudo"
}

path "sys/*" {
  policy = "sudo"
}

path "auth/*" {
  policy = "sudo"
}
```

### User
```
path "secrets/*" {
  policy = "write"
}
```

### App
```
path "secret/*" {
 capabilities = ["read", "list"]
}

path "sys/*" {
 capabilities = ["deny"]
}
```