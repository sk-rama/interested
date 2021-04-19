SOURCE
------

https://cwiki.apache.org/confluence/display/SPAMASSASSIN/FromNotReplyTo


INSTALL
-------

**Debian / Ubuntu:**

```
mkdir /etc/spamassassin/myplugins

wget https://raw.githubusercontent.com/sk-rama/interested/main/spamassassin/FromNotReplyTo/FromNotReplyTo.pm -P /etc/spamassassin/myplugins/
wget https://raw.githubusercontent.com/sk-rama/interested/main/spamassassin/FromNotReplyTo/FromNotReplyTo.cf -P /etc/spamassassin/myplugins/

chmod 644 /etc/spamassassin/myplugins/FromNotReplyTo.pm
chmod 644 /etc/spamassassin/myplugins/FromNotReplyTo.cf
```

edit ```/etc/spamassassin/local.cf``` and add this config:

```
include /etc/spamassassin/myplugins/FromNotReplyTo.pm
include /etc/spamassassin/myplugins/FromNotReplyTo.cf
```

NOTE
----

When you include content of ```FromNotReplyTo.cf``` direct to spamassassin **local.cf** file, you must change row

```
loadplugin FromNotReplyTo FromNotReplyTo.pm

to

loadplugin FromNotReplyTo myplugins/FromNotReplyTo.pm
```

