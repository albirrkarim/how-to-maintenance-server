# How To Maintenance Server

Hello guys, I will share my notes about maintenance server. Im new in dev ops field.

I think the best method to learn is with write down what you learn and share it to others. so i do this.

I just learn and share what i learn to you. I hope you enjoy it.

This article is about software.

Give me support by start this repo or give donation.

[Paypal](https://paypal.me/AlbirrKarim)

<a href='https://ko-fi.com/Q5Q0BC92X' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi3.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

# Choose Right Hosting Service

You have to choose the right hosting service.

For make right decision you must consider your:

1. Apps (What apps you want to hosting)
2. Budget
3. Skill

### A. Shared Hosting

#### Apps

Wordpress hosting, laravel, static pages

### Trafic

Low

### Control Panel

cpanel

#### Budget

low

#### Skill

Not a dev ops person. usually you're just programmer making apps

### B. VPS

#### Apps

everything (wordpress, node js, phoenix, php, python, static)

#### Control Panel:

In vps you must install your control panel by yourself. so you must choose.

Paid: cpanel
Free: Cyberpanel

#### Budget:

medium-high

#### Skill

Dev ops person.

# Any

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

This is good article :

1. [Server Backup Methods: Five Ways to Keep Your Data Safe](https://www.novabackup.com/blog/finding-the-right-server-backup-methods)

## PHP

This is for selecting default php version

```
sudo update-alternatives --config php
```
