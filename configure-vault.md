# Initialize the Vault

Once you have installed and configured the Start Up scripts for both Vault and Consul, you cna start the Vault Configuration procedure. To initialize the vault, you will need to call `vault init`. Vault will likley not know where to find vault, which you can do by setting the `VAULT_ADDR` enviroment variable to point to the URL and Port of which you have configured the Vault. If you are running vault on locahhost, run export `VAULT_ADDR='https://127.0.0.1:8200'`.

You are only able to call `vault init` once on a brand new instance. Vault will initialize, generate encrytioon keys, and root tokens, and rpint out a set of 5 keys and a root token, **SAVE THEM**!

