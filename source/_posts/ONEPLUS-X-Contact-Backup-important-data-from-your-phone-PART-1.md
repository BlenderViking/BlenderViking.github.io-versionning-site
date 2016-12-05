---
title: '[Android Backup] Backup important data from your phone - Part 1 : Backup All Contact'
date: 2016-12-05 08:30:13
categories:
    - Custom Android Rom
    - Backup Android
tags: 
    - Android
    - Backup
thumbnail: '/images/ONEPLUS-X-How-to-install-TWRP/backup/contact/logo.png'
---

Hi,

I have a OnePlus X phone, I would change the Oxygen OS to Cyanogen Mod 14 rom aka CM14.
 
So I will give for you the feedback of my phone upgrade, so all the interesting points and problems I have encountered will be listed as well as the solutions.

There is my first post on this interesting saga :-) 

# Backup First dude !
For the first post, I would call to you the probably most important point : **BACKUP, BACKUP, BACKUP** !!!

Change the Rom on your phone `Wipe all important data` like a factory reset. So I encourage you to do as much backup as possible (Photos, SMS, Contacts, ..).

So i going to explain you how to backup with a lot of OpenSource Software ^^ 

## Contact Backup - Vcard

Why choice the Vcard format aka `.vcf` files ?
- This is the standard format : [RFC 6350](https://tools.ietf.org/html/rfc6350) and [RFC 6868](https://tools.ietf.org/html/rfc6350).
- It's supported by a lot of application (Thunderbird, Outlook, Jabber, Skype, iCalendar, etc..)
- It's human readable, here a sample from [Wikipedia](https://en.wikipedia.org/wiki/VCard) :
```
BEGIN:VCARD
VERSION:2.1
N:Gump;Forrest;;Mr.
FN:Forrest Gump
ORG:Bubba Gump Shrimp Co.
TITLE:Shrimp Man
PHOTO;GIF:http://www.example.com/dir_photos/my_photo.gif
TEL;WORK;VOICE:(111) 555-1212
TEL;HOME;VOICE:(404) 555-1212
ADR;WORK;PREF:;;100 Waters Edge;Baytown;LA;30314;United States of America
LABEL;WORK;PREF;ENCODING=QUOTED-PRINTABLE;CHARSET=UTF-8:100 Waters Edge=0D=
 =0ABaytown\, LA 30314=0D=0AUnited States of America
ADR;HOME:;;42 Plantation St.;Baytown;LA;30314;United States of America
LABEL;HOME;ENCODING=QUOTED-PRINTABLE;CHARSET=UTF-8:42 Plantation St.=0D=0A=
 Baytown, LA 30314=0D=0AUnited States of America
EMAIL:forrestgump@example.com
REV:20080424T195243Z
END:VCARD
```
# How to create the .vcf file
Open the contact app and open the setting menu (On the top right)

![Contact menu](/images/ONEPLUS-X-How-to-install-TWRP/backup/contact/1.png "Contact menu")

## 1. Process an export export
Select the `Export to .vcf file` on the settings menu

![Contact menu](/images/ONEPLUS-X-How-to-install-TWRP/backup/contact/2.png "Contact menu")

## 2. Process an import contact
Select the `Import from .vcf file` on the settings menu

![Contact menu](/images/ONEPLUS-X-How-to-install-TWRP/backup/contact/2.png "Contact menu")


This is the end of the first part of the backup important data from your phone ! 
Congratulation you have process a backup reusable for all contact in your phone :-)

See you later for the next part :-) 