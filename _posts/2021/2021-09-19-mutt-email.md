---
layout: post
categories:
  - linux
tags:
  - email
  - mutt

---
Configuring the Mutt email client.

<!--more-->

### Contents
{% include toc.html %}

### Introduction
I have been using digital cameras since about 2001, but I have become a little jaded with them. It is just too easy to produce acceptable photographs these days. There are so many filters and special effects that even poorly exposed pictures can be salvaged. Thanks to the instant feedback, there is little in the way of excitement or anticipation when taking shots. And so it was, hankering for the old days of film, I purchased a couple of analogue cameras. It is some time since I have enjoyed photography quite this much.

Maybe it's an age thing, but I am also going *old school* with my computing! I am running Ubuntu 20.04 on my PC, but my window manager is *i3*, my music player is the wonderful *Musikcube*, and most of the system administration is undertaken using a terminal. And now I have discovered the delights of the *Mutt* email client.

As with my photography I was fed up with the endless functions modern email clients come with, most of which I rarely if ever used. Mutt is so much more straightforward. As I have discovered, it does one job and does it well.

I had never used Mutt before, and I spent a lot of time on the internet researching Mutt's configuration. It was a steep learning curve, and had it not been for the following articles, I would have been left scratching my head!

+ [therandymon.com](http://therandymon.com/woodnotes/mutt/node24.html)
+ [www.xmodulo.com](https://www.xmodulo.com/mutt-email-client-encrypted-passwords.html)
+ [jasonwryan.com](http://jasonwryan.com/blog/2012/05/12/mutt/)

My thanks to the authors in each case.

### Muttrc
The first file requiring configuration is `~/.mutt/muttrc`.

```
# ~/.mutt/muttrc

# General settings
set header_cache = "~/.mutt/cache/headers"
set message_cachedir = "~/.mutt/cache/bodies"
set certificate_file = "~/.mutt/certificates"
set signature = "~/.mutt/signature"

set abort_nosubject = yes
set mail_check = 60
set timeout = 10
set sort = "reverse-date-received"
set copy = yes
set editor = nano

# Receiving options (imap)
set imap_user = "[my.name]@[service.com]"
set imap_authenticators =  ""
set folder = "imaps://[my.name]@[service.com]@imap.[service.com]:993"
set spoolfile = "+INBOX"
set postponed = "+Drafts"
set record = "+Sent"

# Sending options (smtp)
set smtp_url = "smtps://[my.name]@[service.com]@smtp.[service.com]:465"
set from= "[my.name]@[service.com]"
set realname = "Paul Durnberger"

# Security
set ssl_starttls = yes
set ssl_force_tls = yes
set crypt_autosign = yes

# Render HTML pages human readable
auto_view text/html                                   # view html automatically
alternative_order text/plain text/enriched text/html  # save html for last
set mailcap_path="~/.mutt/mailcap"                    # so Mutt knows where to find mailcap

# Extract hyperlinks from messages
# The macro sets the key binding control-b to launch urlview
macro index \cb |urlview\n 'call urlview to extract URLs out of a message'

# Encrypted password
source "gpg -d ~/.mutt/password.gpg |"
```

If you use this script yourself remember;

1. To change [my.name] and [service.com] to match your own email settings.
2. Create the directory `~/.mutt/cache/`.
3. Create a file `~/.mutt/signature`. This will be appended to the end of each email you send and can contain your name, telephone number, address, whatever you want.

#### Viewing Hyperlinks
The `~/.mutt/muttrc` file includes;
```
macro index \cb |urlview\n 'call urlview to extract URLs out of a message'
```

This allows you to select links from emails, which can then be opened in your browser. It is very clever; just remember to install `urlview`. When viewing an email, tap `ctrl+b` to bring up a list of the available links. Select a link, hit return and that page will open in your browser.

### Encrypted Password
As per [https://www.xmodulo.com/mutt-email-client-encrypted-passwords.html](https://www.xmodulo.com/mutt-email-client-encrypted-passwords.html), I created a file `~/.mutt/password` into which I typed my passwords;

```
set smtp_pass="XXXXXXX"
set imap_pass="XXXXXXX"
```

I then generated an encrypted `gpg` file using the command `$ gpg -r myemail@email.com -e ~/.mutt/password`. Having done so the original `password` file was deleted.

Finally, I added `source "gpg -d ~/.mutt/password.gpg |"` to the end of `~/.mutt/muttrc` so that Mutt would know where to find the passwords.

With the configuration complete, I started Mutt from the command line. Mutt tried to connect to my email provider, but I kept receiving a message to say that login had failed. It turns out the problem was a pair of quote marks! The passwords in the password file should have been surrounded by single quote marks, not double. The correct configuration is;

```
set smtp_pass='XXXXXXX'
set imap_pass='XXXXXXX'
```

Having recreated `password.gpg`, I was able to log in without a problem.

### Mailcap
```
# ~/.mutt/mailcap

# Render html pages in human readable form
text/html; lynx -dump -force_html  %s;  needsterminal; copiousoutput;

# Dealing with attachments
application/pdf; evince %s
application/msword; antiword %s ; copiousoutput
image/jpeg; eog %s
image/gif; eog %s &
image/GIF; eog %s &
image/JPG; eog %s &
image/jpg; eog %s &
```

#### Stripping HTML
Most emails these days are full of HTML, and when viewing the email using Mutt it is nigh on impossible to find the actual message amongst the detritus. This can be fixed. Begin by adding the following to the file `~/.mutt/mailcap`;

```
text/html; lynx -dump -force_html  %s;  needsterminal; copiousoutput;
```

Then ensure the following appears in `~/.mutt/muttrc`;

```
auto_view text/html
alternative_order text/plain text/enriched text/html
set mailcap_path="~/.mutt/mailcap"
```

Now the emails you view in Mutt will be a whole lot easier to read.

#### Dealing with Attachments
So that Mutt knows how to handle attachments, you can add the following to `~/.mutt/mailcap`;

```
application/pdf; evince %s
application/msword; antiword %s ; copiousoutput
image/jpeg; eog %s
image/gif; eog %s &
image/GIF; eog %s &
image/JPG; eog %s &
image/jpg; eog %s &
```

Make sure you install `evince`, `antiword` and `eog` (or you can of course change these settings to refer to the apps you prefer to use to complete each of these tasks).
