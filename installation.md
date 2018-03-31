# Installation

## Install Vault {#install}

Now that we have installed the Key/Value store, we cna procede with installing the Vault Service. Just like Consul, it can be be downloaded from [https://www.vaultproject.io/](https://www.vaultproject.io).

We will need to create an init script in `/etc/init.d` and register it as well. [View the Script](https://bitbucket.org/snippets/sdsu-its/66bEM). You will also need to create a config file in `/etc`: `nano /etc/vault/config.hcl`. The default values should work well for our application.

```text
backend "file" {
 path = "/etc/vault/data"
}

listener "tcp" {
 address = "127.0.0.1:8200"
 tls_disable = 1
}
```

Make the script executable via: `sudo chmod +x vault`

Register the script via: `sudo update-rc.d vault defaults`

Once you have finished the instalation and configuration, you will go back and edit the tcp listner to allow it to bind to a public ip, if desired, to allow outside requests to your vault.

## Initialize the Vault {#initialize}

Once you have installed and configured the Start Up scripts for both Vault and Consul, you can start the Vault Configuration procedure. To initialize the vault, you will need to call `vault init`. Vault will likely not know where to find vault, which you can do by setting the `VAULT_ADDR` environment variable to point to the URL and Port of which you have configured the Vault. If you are running vault on your local machine \(localhost\), run `export VAULT_ADDR='https://127.0.0.1:8200'`.

You are only able to call `vault init` once on a brand new instance. Vault will initialize, generate encryption keys, and root tokens, and prints out a set of 5 keys and a root token, **SAVE THEM**! Whenever you restart the Vault, or seal the vault, you will need 3 of the encryption keys to unseal the vault. This is to ensure that a single malicious individual cannot access the vault. Vault recommends that you encrypt \(via PGP\/[Keybase](https://keybase.io/)\) and distribute the keys to 5 different individuals, three of which are needed to unlock the vault.

## Your First Secret {#secret}

Now that you have initialized your Vault, lets add your first secret. Unseal the Vault using the `vault unseal` command and 3 of the 5 keys that your were provided with during the initialization; you will need to do this everytime your seal, or restart the vault. Next, login via the `vault auth` command and use the root token you were provieded along with your keys. You can now access and modify the vault, as well as it's settings.

Let's add your first secret, which is often used to test connection and Access Control Policies in your vault.

```text
vault write secret/hello value=world
```

It's that easy!

