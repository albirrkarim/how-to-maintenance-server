# How To Maintenance Server

I will share my notes about maintenance server. Im new in dev ops field.

I think the best method to learn is with write down what you learn and share it to others. so i do this.

I just learn and share what i learn to you. I hope you enjoy it.

This article is about software.

Give me support by star this repo or give donation.

<a href='https://paypal.me/AlbirrKarim' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://user-images.githubusercontent.com/29292018/186840848-65e25ff9-47e2-424b-bfa0-4ca5d027b346.png' border='0' alt='Donate via paypal' /></a>

<a href='https://ko-fi.com/Q5Q0BC92X' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi3.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

# Choose Right Hosting Service

<details>
  <summary>Show detail</summary>
  
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

### My Recommendation

With considering many aspect i choose [domainesia](https://my.domainesia.com/ref.php?u=9015) as my hosting provider.

If you in indonesia, i highly recommended [domainesia](https://my.domainesia.com/ref.php?u=9015) as your hosting provider.

I buy VPS in here, The customer service is fast and helpful. the technical support also solve my problem. Even you can ask them to solve your problem.

The price maybe higher than other hosting provider indonesia. but you will not be disappointed buying here.

</details>

<br>
<br>

# Explanation

<details>
  <summary>Show detail</summary>

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

</details>

<br>
<br>

# Backup

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

Maybe i will use zip first then send to local later. after considering many things such as:

- Is your server have free storage at least one to one of folder you will zip?

Example if your folder size is 3GB so at least your server have 3GB free storage.

### For MySQL Database Backup

We must [login to vps without password](https://github.com/albirrkarim/how-to-maintenance-server/blob/master/SSH.md#login-ssh-whitout-password-using-rsa-public--private-key).

Now make script for backup MySQL without typing a password

Make file `.my.cnf` and fill with

```
[mysqldump]
user=admin
password=your_password
```

Then execute backup with this:

```
mysqldump --defaults-file=/absolute_path_to/.my.cnf -u DB_USERNAME DB_NAME > my_db.sql
```

### For PostgreSQL Database Backup

BACKUP

```
PGPASSWORD=your_password pg_dump -U your_username -h localhost -p 5432 db_name > archive_name.sql
```

<!--
RESTORE
```
PGPASSWORD=your_password psql -U your_username db_name -h localhost -p 5432 < /directory/archive.sql
``` -->

### Bash Script Example

<details>
  <summary>Show code</summary>

```bash

# Procedural Backup Web Storage, Mysql, Postgres
# example.com
# https://github.com/albirrkarim/how-to-maintenance-server

Backup_Folder="/Users/susanto/Downloads"
ServerName="example.com"
Username="root"
ServerIP="xxx.xxx.xxx.xxx"
RSAPrivateKey="/Users/susanto/.ssh/example"

# Timestamp
now="$(date +'%d_%m_%Y_%H_%M_%S')"

echo "Starting Backup for $ServerName with assets, db mysql, db postgres on $now"

# For File Storage Backup
scp -r $Username@$ServerIP:/home/admin/projects/reticulum/storage $Backup_Folder/storage_reticulum
scp -r $Username@$ServerIP:/home/admin/projects/laravel/storage/app/public $Backup_Folder/storage_laravel


BackupDBPathOnServer="/home/admin/backup_db";

# Backup MySQL
db_name_mysql="laravel_db"
db_username_mysql="admin"
filename="db_mysql_"$ServerName"_$now".sql

# for the .my.cnf see https://github.com/albirrkarim/how-to-maintenance-server#for-mysql-database-backup
ssh -i $RSAPrivateKey $Username@$ServerIP "mysqldump --defaults-file=/home/admin/.my.cnf -u $db_username_mysql $db_name_mysql > $BackupDBPathOnServer/$filename"


# Backup Postgres Database
db_name_postgres="ret_prod"
db_username_postgres="postgres"
db_password_postgres="postgres"
filename_postgres="db_postgres_"$ServerName"_$now".sql


ssh -i $RSAPrivateKey $Username@$ServerIP "PGPASSWORD=$db_password_postgres pg_dump -U $db_username_postgres -h localhost -p 5432 $db_name_postgres > $BackupDBPathOnServer/$filename_postgres"

# Download database to local
scp $Username@$ServerIP:$BackupDBPathOnServer/$filename $Backup_Folder/$filename
scp $Username@$ServerIP:$BackupDBPathOnServer/$filename_postgres $Backup_Folder/$filename_postgres


echo "Backup for $ServerName Done"

```

</details>

<br>

## Restore

I haven't test this script yet

### Upload Folder to Server Using SCP

```
scp -r /local_dir user@example.com:/var/www/html/target_dir
```

### For MySQL Database Restore

```
mysql -u [user] -p [database_name] < [filename].sql
```

### For PostgreSQL Database Restore

```
pg_restore -d example_db example_db.sql
```

### Bash Script For Restore

<details>
  <summary>Show code</summary>

```bash
# Procedural Restore Web Storage, Mysql, Postgres
# example.com
# https://github.com/albirrkarim/how-to-maintenance-server


# Setting Up
ZipName="full_backup_31_12_2022"
ZipFilePath="/Users/susanto/Downloads/$ZipName.zip"
ServerName="example"
Username="root"
ServerIP="123.123.123.123"
RSAPrivateKey="/Users/susanto/.ssh/example"
UploadDestinationOnServer="/home/admin/restore"

# The backup folder contains
# storage_A, storage_B, db_mysql_ServerName.sql, db_postgres_ServerName.sql

# Timestamp
now="$(date +'%d_%m_%Y_%H_%M_%S')"

echo "Starting Restore for $ServerName with assets, db mysql, db postgres on $now"

# For Uploading Backup Zip
scp $ZipFilePath $Username@$ServerIP:$UploadDestinationOnServer

# # Extract the zip
ssh -i $RSAPrivateKey $Username@$ServerIP "cd $UploadDestinationOnServer && unzip $ZipName.zip"

# # Copy the storage folder to each destination
ssh -i $RSAPrivateKey $Username@$ServerIP "cp -r $UploadDestinationOnServer/$ZipName/storage_A /absolute_destination_A"
ssh -i $RSAPrivateKey $Username@$ServerIP "cp -r $UploadDestinationOnServer/$ZipName/storage_B /absolute_destination_B"

# Backup MySQL For Laravel
db_name_mysql="laravel_akvirtual"
db_username_mysql="admin"
db_password_mysql="your_password"
filename_mysql="db_mysql_"$ServerName"_"$now".sql"

# Check is mysql config exist on server
MysqlConfigTxt="mysql_config_user_"$db_username_mysql".txt"

if [[ ! -f $UploadDestinationOnServer"/"$MysqlConfigTxt ]]
then
    echo $MysqlConfigTxt" File Doesn't Exist"
    ssh -i $RSAPrivateKey $Username@$ServerIP "cd $UploadDestinationOnServer && echo '[mysqldump]\nuser=$db_username_mysql\npassword=$db_password_mysql' > '$MysqlConfigTxt'"
else
    echo $MysqlConfigTxt" File Exist"
fi

ssh -i $RSAPrivateKey $Username@$ServerIP "mysql --defaults-file=$MysqlConfigTxt -u $db_username_mysql $db_name_mysql < $UploadDestinationOnServer/$ZipName/$filename_mysql"

# Restore Postgres Database For Hubs
db_name_postgres="ret_prod_akvirtual"
db_username_postgres="postgres"
db_password_postgres="postgres"
filename_postgres="db_postgres_"$ServerName".sql"

ssh -i $RSAPrivateKey $Username@$ServerIP "PGPASSWORD=$db_password_postgres pg_restore -U $db_username_postgres -h localhost -p 5432 -d $db_name_postgres $UploadDestinationOnServer/$ZipName/$filename_postgres"

echo "Restore for $ServerName Done"
```

</details>

<br>

## Compiling Web Assets (Dist)

If you want compile webpack asset. so you can serve your web as static file you can do it on local or server. but it comes with pros and cons.

### Compile on local (Laptop/ PC)

**Pros**

- Your server will not be disturbed at all.

**Cons**

- Reupload all `dist` folder to your server require internet data.

### Compile on server

You can automate it with [github action runner](https://github.com/actions/runner).

**Pros**

- Less internet data

**Cons**

- Your server will be disturbed, i mean compiling asset it will takes CPU and RAM a lot. if your server get full user will be disturbed.

<br>
<br>

## Version Management

<details>
  <summary>Show detail</summary>
### PHP

This is for selecting default php version

```
sudo update-alternatives --config php
```

### Node JS

i use `nvm`

### Elixir and erlang

i use `asdf`


</details>
<br>

## References That May be Useful

1. [Server Backup Methods: Five Ways to Keep Your Data Safe](https://www.novabackup.com/blog/finding-the-right-server-backup-methods)
