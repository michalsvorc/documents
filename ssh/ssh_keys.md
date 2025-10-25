# SSH Keys

*If possible, prefer storing keys on hardware key devices. This guide is for client desktop stored key.*.

- [Arch Wiki](https://wiki.archlinux.org/title/SSH_keys)
- [ssh-keygen](https://man.archlinux.org/man/ssh-keygen.1)
- [Github Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

The type of key to be generated is specified with the `-t` option.
If invoked without any arguments, ssh-keygen will generate an *Ed25519* key.
*Ed25519* keys have a fixed length and the `-b` (number of bits) flag will be ignored.

```bash
ssh-keygen \
  -t ed25519 \
  -a 100 \
  -o \
  -C "service:user@device" \
  -f ~/.ssh/id_ed25519_github
```

`-t ed25519`: key algorithm; current recommended default.
`-a 100`: KDF (bcrypt) rounds for the private-key passphrase; raises cost for offline brute-force if the file is stolen (trade-off: slower unlock).
`-o`: use the modern OpenSSH private-key format (bcrypt KDF); implied for newer key types but explicit is fine.
`-C <comment>`: put a descriptive, non-sensitive label.
`-f <filepath>`: file path/name for the private key (use distinct names if you maintain multiple keys).

*Recommendations:*
- Use Ed25519 keys for personal/dev machines.
- Use separate keys per device/account, store private keys with chmod 600, and rotate keys if a device is lost.
- Protect the private key with a strong passphrase and use an SSH agent.

## Managing multiple keys

- [Arch Wiki](https://wiki.archlinux.org/title/SSH_keys#Managing_multiple_keys)
- [Best way to use multiple SSH private keys on one client - stackoverflow.com](https://stackoverflow.com/questions/2419566/best-way-to-use-multiple-ssh-private-keys-on-one-client)

You can set different keys to be used for different hosts or remote users by using `~/.ssh/config`.
