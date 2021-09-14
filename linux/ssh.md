# SSH

- [Arch wiki](https://wiki.archlinux.org/title/OpenSSH)
- [Gentoo wiki](https://wiki.gentoo.org/wiki/SSH) 

## SSH keys

- [Arch wiki](https://wiki.archlinux.org/title/SSH_keys)

Generate default 3072-bit RSA (and SHA256) key.

```console
$ ssh-keygen -C "$(whoami)@$(uname -n)-$(date -I)"
```

Upon issuing the ssh-keygen command, you will be prompted for the desired name and location of your private key.

### Managing multiple keys

- [Arch wiki](https://wiki.archlinux.org/title/SSH_keys#Managing_multiple_keys)
- [Best way to use multiple SSH private keys on one client](https://stackoverflow.com/questions/2419566/best-way-to-use-multiple-ssh-private-keys-on-one-client)

You can set different keys to be used for different hosts or remote users by using `~/.ssh/config`.

## SSH agent

- [Arch wiki](https://wiki.archlinux.org/title/SSH_keys#SSH_agents)

