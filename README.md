# ZVault

Simple file vault written in Zsh.

## Sub-commands

- `store <config file>`: Encrypt files and move to destination dir, as per the config file.
- `install <config file>`: Decrypt files and move to installation dir, as per the config file.

Function pass-through: `decrypt`, `encrypt`. Used for testing.

## Configuration file

Sub-commands which use the configuration file: `store` and `install`.

The configuration file can have as many lines as needed and can be named anyway.

Each line has 3 items separated by whitespace. These 3 items are enough for `zvault` to infer data
required to both store and install. The caret symbol (`~`) can be used for the user home:

1. Full path of encrypted file. Must be suffixed with `.enc`.
2. Full path of dir where to install the decrypted file on running `install`.
3. File permissions used by `chmod`, set on both encrypted and plaintext files.

## Example usage

Given a `config.txt` with this single line:

```text
~/.dotfiles/vault/aws/config.enc ~/.aws 600
```

`zvault store config.txt`:

- Expects `~/.aws/config` to exist, encrypting it to `~/.dotfiles/vault/aws/config.enc` if the
  latter does not exist. If the `.enc` file was created, set its permissions with `chmod`.

`zvault install config.txt`:

- Expects `~/.dotfiles/vault/aws/config.enc` to exist, decrypting it to `~/.aws/config` if the
  latter does not exist. If the plaintext file was created, set its permissions with `chmod`.
