# SSH Keys (YubiKey)

- [ssh-keygen](https://man.archlinux.org/man/ssh-keygen.1)
- [Securing SSH with the YubiKey](https://developers.yubico.com/SSH/)
- [FIDO commands](https://docs.yubico.com/software/yubikey/tools/ykman/FIDO_Commands.html?)

*Read more:*
- [Git Commit Signing](https://developers.yubico.com/SSH/Securing_git_with_SSH_and_FIDO2.html)
- [passkey / credential storage limits and firmware differences](https://support.yubico.com/hc/en-us/articles/360013790319-How-many-accounts-can-I-register-my-YubiKey-with?utm_source=chatgpt.com)

## Requirements

- OpenSSH client >= 8.2 (8.3+ or 8.9+ recommended for some advanced options).
- Set a FIDO2 PIN: `ykman fido access change-pin`

## Create key pair

### 1. Generate SSH key

```bash
ssh-keygen \
  -t ed25519-sk \
  -O resident \
  -C "service:user@device" \
  -f ~/.ssh/id_ed25519_sk_identifier
```

*Notes:*
`-t ed25519-sk`: FIDO2-backed Ed25519 key. Use ecdsa-sk only if your firmware/device requires it.
`-O resident`: store credential on the YubiKey (makes the key usable on other machines without copying private files). Requires a FIDO2 PIN.
`-C <comment>`: put an identifying comment (email + service + device).
`-f <filepath>`: a small handle file (you can keep it or remove it; keeping it makes using that machine more convenient).

`-O verify-required`: require PIN and physical touch for each operation (DOES NOT work with ssh-agent caching).

### 2. Upload PUBLIC KEY to the service

```bash
cat ~/.ssh/id_ed25519_sk_identifier.pub
```

### 3. Update config entries

Edit `~/.ssh/config`:


```bash
Host <service.com>
  HostName <service.com>
  User git
  IdentityFile ~/.ssh/id_ed25519_sk_identifier
  IdentitiesOnly yes
  AddKeysToAgent yes
```

*Notes:*
- `IdentitiesOnly` yes prevents the client from trying other keys and hitting server-side limits.
- `AddKeysToAgent` yes will add the handle to your agent (and allow caching of PIN in the agent session).

### 4. Test connection

Example:

```bash
ssh -T git@github.com
```

## Agent behaviour and PIN caching

`ssh-add ~/.ssh/id_ed25519_sk_<service>` will add the handle to ssh-agent so the agent can cache the PIN for the session and reduce PIN prompts; touch (user presence) may still be required depending on verify-required. 
Yubico Developers

## Managing multiple SSH keys

You can store multiple resident keys on a single YubiKey. Older YubiKey 5 firmware supported ~25 resident credentials; newer firmware (5.7+) can hold up to 100 discoverable credentials. Check Yubico’s support doc for your firmware. Do not rely on unlimited slots.

List resident credentials with ykman:

```bash
ykman fido credentials list
```

To delete a resident credential:

```bash
ykman fido credentials delete <credential-id>
```

---

Troubleshooting tips

“Agent refused operation” / “signing failed”: ensure the YubiKey is present, the correct handle file (~/.ssh/id_...) is in ssh-agent and you used the correct IdentityFile in ~/.ssh/config. Try ssh-add -D then re-add the specific handle file. 
Yubico Developers

If resident keys don’t appear on another machine, ensure that OpenSSH supports FIDO2 (and your OpenSSH is recent), and that the YubiKey PIN is set and you can touch it. 
Yubico Developers
openssh.com

Quick checklist to run now

ssh -V (confirm OpenSSH >= 8.2)

ykman --version (install ykman if missing)

ykman fido access change-pin (set FIDO2 PIN)

ssh-keygen -t ed25519-sk -O resident -O verify-required -C "github:you@example.com" -f ~/.ssh/id_ed25519_sk_github

cat ~/.ssh/id_ed25519_sk_github.pub → paste into GitHub

Repeat for GitLab with different filename/comment.

Edit ~/.ssh/config, then ssh -T git@github.com and ssh -T git@gitlab.com to test.
