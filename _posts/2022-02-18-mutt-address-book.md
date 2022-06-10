---
layout: post
categories: linux
tags:
  - addressbook
  - email
  - mutt

---
An address book for the Mutt Email Client.

<!--more-->

Something I've been meaning to record since [setting up the Mutt email client](/2021/09/19/mutt-email) was how I added an address book.

The simplest option is to use Mutt's alias file. Begin by creating a blank document, `~/.mutt/mutt-alias`.

Next we amend `~/.mutt/muttrc` to include reference to the alias file, by adding the following;

```
# Address Book (using ~/.muttrc/mutt-alias)
source ~/.mutt/mutt-alias
set alias_file = "~/.mutt/mutt-alias"
```

Restart mutt, and highlight one of the messages in your inbox. Tap the letter `a` and at the bottom of the screen you will be asked what alias you want to assign to the sender of that email. Answer the subsequent questions, and save. The next time you want to email that person, at `To:` type in the alias you assigned.
