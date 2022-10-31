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

- cpanel (paid services)
  Easy to use, a lot of feature.

- cyberpanel (free) <- i use this.
  Not that easy, but its still good.

## Overall Monitoring

- Webmin
  this is free, a lot of feature to explore.

## Backup

Really, for now i don't understand about how to backup.

I backup manually using hardisk.

I will do it every month. for synchronization.

Using `.sh` script so i just execute it.

make file `backup.sh` then

```bash
chmod +x backup.sh
```

The script is depends on your needs. what you want to backup, here the example from my needs:

## For Assets Backup (Image/Video/etc)

```bash
scp -r YOUR_USERNAME@YOUR_SERVER_IP:/absolute_path/THE_FOLDER_IN_SERVER /absolute_path/YOUR_LOCAL_FOLDER_HERE
```

## For MySQL Database Backup

We must [login to vps whitout password](https://github.com/albirrkarim/how-to-maintenance-server/blob/main/SSH.md).

Now make script for backup MySQL whitout typing a password

Make file `.my.cnf` and fill with

```
[mysqldump]
password=your_password
```

```
mysqldump --defaults-file=/absolute_path_to/.my.cnf -u DB_USERNAME DB_NAME > my_db.sql
```

## For Postgrest Database Backup


Im working on it


This is good article :

1. [Server Backup Methods: Five Ways to Keep Your Data Safe](https://www.novabackup.com/blog/finding-the-right-server-backup-methods)

https://www.digitalocean.com/community/tutorials/how-to-allow-remote-access-to-mysql

## PHP

This is for selecting default php version

```
sudo update-alternatives --config php
```
