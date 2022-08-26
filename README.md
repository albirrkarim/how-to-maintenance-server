# How To Maintenance Server

Hello guys, I will share my notes about maintenance server. Im new in dev ops field.

I think the best method to learn is with write down what you learn and share it to others. so i do this.

I just learn and share what i learn to you. I hope you enjoy it.

This article is about software.

Give me support by start this repo or give donation.

[Paypal](https://paypal.me/AlbirrKarim)

<a href='https://ko-fi.com/Q5Q0BC92X' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi3.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

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


## PHP 

This is for selecting default php version

```
sudo update-alternatives --config php
```


## Composer 

This is for managing php app dependencies