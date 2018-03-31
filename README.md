# Introduction

With the advent of GIT based CI systems, there is a need for a secure place to store application configuration parameters outside of the application. Vault is a service that allows for Secrets to be stored outside of the application, and then retrieved through a variety of authentication methods. The Vault can be accessed via the CLI or its HTTP REST interface. If you want to use the CLI, use the preliminary installation instructions below.

## Download Vault

Vault is available for a variety of platforms, which can all be downloaded from the [Vault Project's Website](https://www.vaultproject.io/downloads.html). You will need download the package for your server, and for the purpose of this book, we will assume that it is a Debian Based Linux System. If it is not, you will need to adapt the Install Procedure to match your system and its requirements.

Once you have downloaded the package, move it to `/usr/bin/` and make sure that it is executable. Vault reads in any properties that are not specified in the command line via arguments from Environment Variables. The most important one is the `VAULT_ADDR` which specifies via what protocol, what address, and what port will be used to communicate with the vault. The `export` command below can be adapted to match your server's specification \(which we will be working on in the next sections\).

`export VAULT_ADDR='https://127.0.0.1:8200'`

You may want to add this line to your bash profile to keep you from needing to set the Environment Variables after every login. _You will still need to Authenticate with the Vault after every login._

## License

![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)

This work is licensed under a 

[Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/)

.

