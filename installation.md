# Install Vault {#install-vault}

Now that we have installed the Key/Value store, we cna procede with installing the Vault Service. Just like Consul, it can be be downloaded from [https://www.vaultproject.io/](https://www.vaultproject.io).

We will need to create an init script in `/etc/init.d` and register it as well. [View the Script](/vault.txt). You will also need to create a config file in `/etc`: `nano /etc/vault/config.hcl`. The default values should work well for our application.

```
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
