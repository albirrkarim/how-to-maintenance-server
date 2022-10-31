# Login SSH Whitout Password (using RSA Public & Private Key)

```
ssh-keygen
```

Enter file in which to save the key (/Users/susanto/.ssh/id_rsa):

Just fill your with any name. for me i use my website name.

then copy the pub key to your server

```
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```

login to your server using password.
then

```
sudo nano /etc/ssh/sshd_config
```

enable pub key auth

```
PubkeyAuthentication yes
```

restart service

```
sudo systemctl restart sshd
```

Then try to login with RSA private key

```
ssh -i /absolute_path/.ssh/id_rsa user@x.x.x.x
```
