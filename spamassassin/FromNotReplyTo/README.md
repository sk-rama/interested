SOURCE
------

https://cwiki.apache.org/confluence/display/SPAMASSASSIN/FromNotReplyTo


INSTALL
-------

**Debian / Ubuntu:**

```
mkdir /etc/spamassassin/myplugins

wget https://github.com/sk-rama/interested/blob/main/spamassassin/FromNotReplyTo/FromNotReplyTo.pm -P /etc/spamassassin/myplugins/
wget https://github.com/sk-rama/interested/blob/main/spamassassin/FromNotReplyTo/FromNotReplyTo.cf -P /etc/spamassassin/myplugins/

chmod 644 /etc/spamassassin/myplugins/FromNotReplyTo.pm
chmod 644 /etc/spamassassin/myplugins/FromNotReplyTo.cf
```

