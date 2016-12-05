---
title: '[Android Backup] Backup important data from your phone - Part 2 : SMS / MMS / Phone call'
date: 2016-12-05 12:30:13
categories:
    - Custom Android Rom
    - Backup Android
tags: 
    - Android
    - Backup
thumbnail: '/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/logo.png'
---

Hi,

There is my second post about Android Backup on my way to upgrade my OnePlus X from OxygenOS to CM14. 

In the first part, we talk about [Contact Backup](/2016/12/05/ONEPLUS-X-Contact-Backup-important-data-from-your-phone-PART-1/), for the second part, we going to talk about SMS / MMS / Phone call historic backup :-)

# SMS / MMS / Phone call log Backup - SMS Backup+
For the sms backup a recommend to use this OpenSource app : [SMS Backup+](https://github.com/jberkel/sms-backup-plus)

The concept of this app is simple, it's use an IMAP Server for backup / restore all sms on your device.

Here some features provide by SMS Backup+ extract from the GitHub app:

- New restore feature. SMS stored on Gmail can be transferred back to the phone. This even works for users who have already created their backups with older versions of SMS Backup. Note: MMS are currently not restored.
- XOAuth: SMS Backup+ will never ask you for your Gmail password. Instead it uses XOAuth to get access to your data. You can revoke the access rights at any time.
- MMS backup support (since 1.1), only available on Android 2.x
- Call log backup (since 1.2), with Google Calendar integration (since 1.3.) and restore (since 1.4).
- Batch size limits removed.
- Works with any IMAP server (but defaults to Gmail).

# Backup Items

## Using your own IMAP Server

Go to `Advanced setting > IMAP server` setting for configure your IMAP Server config

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/0.png "SMS Backup+")

## Using Gmail

If you using a Gmail account, you just need to clic on the Connect section in center of the screen :

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/1.png "SMS Backup+")

### Select your account

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/2.png "SMS Backup+")

### Allow it your Gmail access

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/3.png "SMS Backup+")

### Add begin the backup

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/4.png "SMS Backup+")

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/5.png "SMS Backup+")

# Restore Items

You just need to click on restore button and define temporary the backup app as your sms app.

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/6.png "SMS Backup+")

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/7.png "SMS Backup+")

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/8.png "SMS Backup+")


And you have correctly restore you items, see the notification area popup a lot of old message restored

![SMS Backup+](/images/ONEPLUS-X-How-to-install-TWRP/backup/sms/9.png "SMS Backup+")

And we have now a backup for your SMS / MMS / Phone Call log.

Enjoy !
