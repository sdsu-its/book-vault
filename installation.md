

# Install Consul {#install-consul}

Before we can install and initialize the vault, we need to install and setup the Secure Key-Store service. In our case this is Consul, which can be downloaded from [https://www.consul.io/](https://www.consul.io/).

We will create an init script in `/etc/init.d` and register it so that the Consul service starts when the server boots. [View the Script.](/consul.txt)

Make the script executable via: `sudo chmod +x consul`

Register the script via: `sudo update-rc.d consul defaults`

You are now ready to install the Vault.

# Install Vault {#install-vault}

Now that we have installed the Key\/Value store, we cna procede with installing the Vault Service. Just like Consul, it can be be downloaded from [https://www.vaultproject.io/](https://www.vaultproject.io).

We will need to create an init script in `/etc/init.d` and register it as well. [View the Script](/vault.txt). You will also need to create a config file in `/etc`: `nano /etc/vault.hcl`. The default values should work weel for our application.

```
backend "consul" {
address = "127.0.0.1:8500"
path = "vault"
}

listener "tcp" {
address = "127.0.0.1:8200"
tls_disable = 1
}
```

Make the script executable via: `sudo chmod +x vault`

Register the script via: `sudo update-rc.d vault defaults`
