# Initialize the Vault

Once you have installed and configured the Start Up scripts for both Vault and Consul, you can start the Vault Configuration procedure. To initialize the vault, you will need to call `vault init`. Vault will likely not know where to find vault, which you can do by setting the `VAULT_ADDR` environment variable to point to the URL and Port of which you have configured the Vault. If you are running vault on your local machine (localhost), run `export VAULT_ADDR='https://127.0.0.1:8200'`.

You are only able to call `vault init` once on a brand new instance. Vault will initialize, generate encryption keys, and root tokens, and prints out a set of 5 keys and a root token, **SAVE THEM**! Whenever you restart the Vault, or seal the vault, you will need 3 of the encryption keys to unseal the vault. This is to ensure that a single malicious individual cannot access the vault. Vault recommends that you encrypt \(via PGP\/[Keybase](https://keybase.io/)\) and distribute the keys to 5 different individuals, three of which are  needed to unlock the vault.

# Configure TSL

By default, TSL \(HTTPS\) is disabled for simplicity; however, if we want to ensure the security of our secrets when we access them via the API, we want to encrypt the traffic between our API Client and the Vault Server. You can either use a Certificate/Key set that you already have provisioned for your machine, provided that you use the servers FQDN in your `VAULT_ADDR` environment variable. You may need to add the Root CA to your machine's trusted CA list, which will vary by OS. If you would like to generate your own CA and Certificate/Key pair, Sam Dunne has a great tutorial: [http://dunne.io/vault-and-self-signed-ssl-certificates](http://dunne.io/vault-and-self-signed-ssl-certificates).

In the end, your TCP listener should look something like the following, with the paths and file names adjusted for your specific `crt` and `key`. If you are comfortable at this point, you can expose your server publicly, by replacing `127.0.0.1` with your public IP. *Note, that you will not be able to access the server via localhost, unless you have re-configured your hosts file.*

```
listener "tcp" {
 address = "127.0.0.1:8200"
 tls_cert_file= "/etc/vault/ssl/vault.crt",
 tls_key_file="/etc/vault/ssl/vault.key"
}
```

# Configure Users

Using tokens is annoying, would it not be simpler to use a username/password combination? Conveniently, Vault supports this feature nativity. To enable, run `vault auth-enable userpass` on your unsealed vault. You can then create new users via the following command, with the respective [Access Policy](/access_control.md): 

```
vault write auth/userpass/users/username \
    password=password \
    policies=access_level

```


# Configure Apps

First, we will need to enable "AppRoles" which will allow our apps to authenticate themselves with the Vault. To do this we run `vault auth-enable approle`.
