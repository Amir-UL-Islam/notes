1. **Create a new key without passphrase**:
```shell
    ssh-keygen -t ed25519 -f ~/.ssh/dhc_dev -N ""
```
    
2. **Add public key to server**:
```shell
    ssh-copy-id -i ~/.ssh/dhe_dev root@10.0.40.60
```
2. **Configure SSH to use this key**:
    Add on ~/.ssh/config
```shell
    Host yourserver.example.com
      IdentityFile ~/.ssh/server_specific_key
```