## Introduction

- `ssh` - secure shell
- SSH is a network protocol that enables secure remote access to a computer over an unsecured network.
    - It is a communication protocol like [[HTTP]], [[HTTPS]] and _FTP_.
- It securely runs a program or opens a shell on a remote system using encrypted traffic
- It replaces file transfer programs, such as FTP, by providing secure file transfer capabilities.
- The most basic use of SSH is to connect to a remote host for a terminal session, where the user is prompted for a password for the account under which the client is running.
- It uses the client-server model, connecting a client application with an SSH server, and often includes support for application protocols used for terminal emulation or file transfers.
- It provides strong encryption, public key authentication, and encrypted data communications between two computers connecting over an open network, such as the internet.

- `ssh` is the client; to use `ssh`, server must have `sshd` (Open SSH Daemon) installed and running.
- It can be authenticated using several ways:
    - password
    - host based - given a list of known hosts
    - public-private key pairs
- `ssh-keygen` generates public-private key pairs located at `~/.ssh/id_rsa` (private key) and `~/.ssh/id_rsa.pub` (public key). The latter is sent to the server's `authorized_keys` file.

## Workflow

- The typical workflow for connecting to a remote host using SSH involves the following steps:
    - Type the `ssh` command followed by the username and hostname of the remote server.
    - If it's the first time connecting to the server, you will be prompted to confirm the authenticity of the server's fingerprint. Type `yes` to continue.
    - Enter password when prompted.
    - Once you are logged in, you can run commands on the remote server as if you were physically present at the console.

## Examples

- Open an SSH session with the remote host and prompt the user for their password:

```bash
ssh user@remote-host
```

- Generate a new RSA key pair for authentication in the default location (`~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`):

```bash
ssh-keygen -t rsa
```

- Run a command on the remote host:

```bash
ssh demo@remote-host "ls -l"
```

- Copy a file from the local machine to the remote host:

```bash
scp /path/to/local/file demo@remote-host:/path/to/remote/directory
```

- Copy a file from the remote host to the local machine:

```bash
scp demo@remote-host:/path/to/remote/file /path/to/local/directory
```

---

## Further

### Learn 🧠

- [SSH Crash Course (YouTube)](https://www.youtube.com/watch?v=hQWRp-FdTpc)