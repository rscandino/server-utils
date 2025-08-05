# :closed_lock_with_key: SSH - Secure SHell
Is a cryptographic network protocol used to securely operate network services, in particular for secure remote login and command-line execution,
providing an encrypted channel between a client and a server. 
This protects against eavesdropping, interception, and other attacks.

An SSH connection is established between a local machine (the **client**) and a remote machine (the **hostname** server). The server must be running an SSH daemon, which listens for incoming connections.
The **client** must have installed the [ssh client package](https://documentation.ubuntu.com/server/how-to/security/openssh-server/index.html).

Check if your system has `ssh` installed by typing in the terminal

```shell
ssh
```
More information about `ssh` and all its commands can be found [here](https://www.ssh.com/academy/ssh/command).

## Access and Setup
Two main way of authenticate exists when using ssh:

- **Password** Authentication: The simplest method, where you use a username and password to log in. This is less secure as passwords can be vulnerable to interception or brute-force attacks.

- **Key-Based** Authentication: A more secure method that uses a public-private key pair. The public key is stored on the server, and the private key is kept securely on the client machine. When a connection is initiated, the server uses the public key to verify the client's identity without requiring a password.

### Password authentication
To authenticate to a machine through password you just have to run 
```shell
ssh username@hostname
```

### Key-Based authentication
To exploit the public-private key pair you must first generate a key for your machine.
Different ssh keys can be generated for different purposes (github access, server access, etc.). 
The default key used by the machine when not specified is `~/.ssh/id_<type_of_key>`, it is important to have a default key generated on your pc in order to not use others.

To generate a key run

```shell
ssh-keygen -f ~/.ssh/<key_name> -t <type_of_key> -C "<comment_to_remember_key_info>"
```

Where:

- <key_name> is the name of the key, I usually specify for which the key is used and the type of encryption (eg. `~/.ssh/myservers_ed25519`)
- <type_of_key> is the encryption used, I recommend `ed25519` but others are [available](https://www.ssh.com/academy/ssh/keygen#choosing-an-algorithm-and-key-size)
- <comment_to_remember_key_info> a comment (plain string) added at the end of the public key to remembering further info, I usually put the account/mail associated with it, where and/or when was generated

This will prompt you to generate a key, you can associate a *passphrase* to it, you can also change it later if you want.
Once generated the key must be added to your host (server) of interest. To do that another ssh command is used

```shell
ssh-copy-id -i ~/.ssh/<keyname> username@hostname
```

You can now access the server by simply tipyng

```shell
ssh -i ~/.ssh/<keyname> username@hostname
```


To summarize, lets say i want a key for my account `riccardo` to access the hostname `machine1.mycompany.it` it will be:

1. Generate key `ssh-keygen -t ed25519 -f ~/.ssh/mycompany_ed25519 -C "riccardo+2025@mycompany.it"`
2. Copy key on machine `ssh-copy-id -i ~/.ssh/mycompany_ed25519 riccardo@machine1.mycompany.it`
3. Access machine `ssh -i ~/.ssh/mycompay_ed25519 riccardo@machine1.mycompany.it`

## Configuration
The *Key-Based* authentication provides a flexible and secure access to your server that coupled with **ssh host configuration** will also results in a simplified login. 
A configuration file can be created at `~/.ssh/config`, it should be configured to have permissions `600` (just run `chmod 600 ~/.ssh/config`).
This file can contain specific hosts configuration, like:

```shell
Host machine1
	Hostname machine1.mycompany.it
	User riccardo
	IdentityFile ~/.ssh/mycompany_ed25519
```

In this way we can access this machine with the specified ssh key by simply typing `ssh machine1`.

If the number of machine of the same **domain** (in the example `.mycompany.it`) are multiple and with the same config you can configure ssh by domain and to look for specific domains:

```shell
CanonicalizeHostname yes                                        # Try to search for hostname in canonical domains
CanonicalDomains mycompany.it mySECONDcompany.bigcompany.it          # here we specified two domains

Host *.mycompany.it                 # Set this user and ssh key for all the machines under this domain
    User riccardo
    IdentityFile ~/.ssh/mycompany_ed25519

Host *.mySECONDcompay.bigcompany.it
    User riccardo
    IdentityFile ~/.ssh/mySECONDcompany_ed25519
```

In this way you don`t have to specify for each server of your company the config to use you just have to type the server name (the one before the domain):

```shell
ssh machine1
ssh machine2
```
