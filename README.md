# How To Maintenance Server

Hello guys, I will share my notes about maintenance server. Im new in dev ops field.

I think the best method to learn is with write down what you learn and share it to others. so i do this.

I just learn and share what i learn to you. I hope you enjoy it.

This article is about software.

Give me support by star this repo or give donation.

<a href='https://paypal.me/AlbirrKarim' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://user-images.githubusercontent.com/29292018/186840848-65e25ff9-47e2-424b-bfa0-4ca5d027b346.png' border='0' alt='Donate via paypal' /></a>

<a href='https://ko-fi.com/Q5Q0BC92X' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi3.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

# Choose Right Hosting Service

You have to choose the right hosting service.

For make right decision you must consider your:

1. Apps (What apps you want to hosting)
2. Budget
3. Skill

### A. Shared Hosting

| Aspect        | Description                                                      |
| ------------- | ---------------------------------------------------------------- |
| Apps          | Wordpress hosting, laravel, static pages                         |
| Trafic        | Low                                                              |
| Control Panel | cpanel                                                           |
| Budget        | Low                                                              |
| Skill         | Not a dev ops person. usually you're just programmer making apps |

### B. VPS

| Aspect        | Description                                                                                                    |
| ------------- | -------------------------------------------------------------------------------------------------------------- |
| Apps          | everything (wordpress, node js, phoenix, php, python, static)                                                  |
| Trafic        | Medium - High                                                                                                  |
| Control Panel | In vps you must install your control panel by yourself. so you must choose. see [this section](#control-panel) |
| Budget        | Medium - High                                                                                                  |
| Skill         | Dev ops person.                                                                                                |

# Explanation

## Operating system

I prefer using ubuntu LTS. i haven't try centos.

## Control Panel

In case you are using your server for many website which is PHP website.

You can use:

- [Cpanel](https://cpanel.net/) (paid services)
  Easy to use, a lot of feature.

- [Cyberpanel](https://cyberpanel.net) (free) <- i use this.
  Not that easy, but its still good.

## Overall Monitoring

- [Webmin](https://www.webmin.com/) (Free), Lot of feature to explore.

## Backup

There are method for backup on server or backup on local.

I choose backup on local(OFFLINE). because if my server completely destroyed i still have backup on OFFLINE. I backup using hardisk.

I will do it every month. for synchronization.

Using `.sh` script so i just execute it. and wait the proccess done.

make file `backup.sh` then

```bash
chmod +x backup.sh
```

**The script is depends on your needs. what you want to backup, here the example from my needs:**

### For Assets Backup (Image/Video/etc)

#### Method 1

```
Folder on server -> Send to local -> zip
```

Im not zip and unzip on server for now. because it will take more server resources (HIGH CPU & RAM) and spaces. 

This is the commands for it.

```bash
scp -r YOUR_USERNAME@YOUR_SERVER_IP:/absolute_path/THE_FOLDER_IN_SERVER_YOU_WANT_TO_BACKUP /absolute_path/YOUR_LOCAL_FOLDER_HERE
```

the `-r` mean reqursive (for folder backup).

#### Method 2

```
Folder on server -> zip first -> Send to local -> delete zip on server
```

Maybe i will use zip first then send to local later. after considering many things.

### For MySQL Database Backup

We must [login to vps without password](https://github.com/albirrkarim/how-to-maintenance-server/blob/master/SSH.md#login-ssh-whitout-password-using-rsa-public--private-key).

Now make script for backup MySQL without typing a password

Make file `.my.cnf` and fill with

```
[mysqldump]
password=your_password
```

Then execute backup with this:

```
mysqldump --defaults-file=/absolute_path_to/.my.cnf -u DB_USERNAME DB_NAME > my_db.sql
```

### For PostgreSQL Database Backup

BACKUP
```
pg_dump -U user -h localhost -p 5432 db_name > archive_name.sql
```

RESTORE
```
psql -U user db_name -h localhost -p 5432 < /directory/archive.sql
```

<br>
<br>

## Version Management

### PHP

This is for selecting default php version

```
sudo update-alternatives --config php
```

### Node JS

i use `nvm`

### Elixir and erlang

i use `asdf`

<br>

## References That May be Useful

1. [Server Backup Methods: Five Ways to Keep Your Data Safe](https://www.novabackup.com/blog/finding-the-right-server-backup-methods)
