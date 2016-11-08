# Vault Installation,Configuration & Management


With the advent of GIT based CI systems, there is a need for a secure place to store application configuration parameters outside of the application. Vault is a service that allows for Secrets to be stored outside of the application, and then retrieved through a variety of authentication methods. The Vault can be accessed via the CLI or its HTTP REST interface. If you want to use the CLI, use the preliminary installation instructions below.

## Download Vault

Vault is available for a variety of platforms, which can all be downloaded from the [Vault Project's Website](https://www.vaultproject.io/downloads.html). You will need download the package for your server, and for the purpose of this book, we will assume that it is a Debian Based Linux System. If it is not, you will need to adapt the Install Procedure to match your system and its requirements.

Once you have downloaded the package, move it to `/usr/bin/` and make sure that it is executable. Vault reads in any properties that are not specified in the command line via arguments from Environment Variables. The most important one is the `VAULT_ADDR` which specifies via what protocol, what address, and what port will be used to communicate with the vault. The `export` command below can be adapted to match your server's specification (which we will be working on in the next sections).

`export VAULT_ADDR='https://127.0.0.1:8200'`

You may want to add this line to your bash profile to keep you from needing to set the Environment Variables after every login. *You will still need to Authenticate with the Vault after every login.*


---

## License

This book is licensed under the MIT License, which is listed below.

Copyright (c) 2016 San Diego State University - Instructional Technology Services

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
