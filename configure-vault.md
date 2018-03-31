# Configure Vault

## Configure TLS {#tls}

By default, TLS \(HTTPS\) is disabled for simplicity; however, if we want to ensure the security of our secrets when we access them via the API, we want to encrypt the traffic between our API Client and the Vault Server. You can either use a Certificate/Key set that you already have provisioned for your machine, provided that you use the servers FQDN in your `VAULT_ADDR` environment variable. You may need to add the Root CA to your machine's trusted CA list, which will vary by OS. If you would like to generate your own CA and Certificate/Key pair, Sam Dunne has a great tutorial: [http://dunne.io/vault-and-self-signed-ssl-certificates](http://dunne.io/vault-and-self-signed-ssl-certificates).

In the end, your TCP listener should look something like the following, with the paths and file names adjusted for your specific `crt` and `key`. If you are comfortable at this point, you can expose your server publicly, by replacing `127.0.0.1` with your public IP. _Note, that you will not be able to access the server via localhost, unless you have re-configured your hosts file._

```text
listener "tcp" {
 address = "127.0.0.1:8200"
 tls_cert_file= "/etc/vault/ssl/vault.crt",
 tls_key_file="/etc/vault/ssl/vault.key"
}
```

## Configure Users {#users}

Using tokens is annoying, would it not be simpler to use a username/password combination? Conveniently, Vault supports this feature nativity. To enable, run `vault auth-enable userpass` on your unsealed vault. You can then create new users via the following command, with the respective [Access Policy](access-control.md):

```text
vault write auth/userpass/users/username \
    password=password \
    policies=access_level
```

To login, use the following command, be sure to substitute in your username in the command.

```text
vault auth -method=userpass username=username
```

To change your password, use the following command, subsituting in your username and desired new password.

```text
vault write auth/userpass/users/username password=password
```

## Configure Apps {#apps}

First, we will need to enable "AppRoles" which will allow our apps to authenticate themselves with the Vault. To do this we run `vault auth-enable approle`. Now, we will create as many "AppRoles" as we need. Use the line below as a staring point for your AppRole Creation command:

```text
vault write auth/approle/role/role-name policies=app token_ttl=1200
```

This will create the role, to get the role-id, enter the following command with the `role-name` from the above statement:

```text
vault read auth/approle/role/role-name/role-id
```

We will be using AppRoles in Push mode to simplify the API process, which requires us to have the server set the Secret-id ahead of time. Use the following command to do this:

```text
vault write -f auth/approle/role/role-name/secret-id
```

Make note of both the role-id and the secret-id as both will be needed by the app to request an access token with the previously mentioned policy.

### Provisioning Automation

If you want to speed up this process, you can use a shell script, which can be found on [BitBucket](https://bitbucket.org/snippets/sdsu-its/yyrE5), which takes the app name and ACL Policy as command line arguments and prints out the role and secret ID.

