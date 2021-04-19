NOTE:  this plugin is be merged into SpamAssassin, so it will no longer be updated here.
========================================================================================

DecodeShortURLs
===============

This is a plugin for SpamAssassin.

This plugin looks for URLs shortened by a list of URL shortening services and
upon finding a matching URL will connect using to the shortening service and
do an HTTP HEAD lookup and retrieve the location header which points to the 
actual shortened URL, it then adds this URL to the list of URIs extracted by 
SpamAssassin which can then be accessed by other plug-ins, such as URIDNSBL.

This plugin also sets the rule ```HAS_SHORT_URL``` if any matching short URLs are 
found.

Regular 'uri' rules can be used to detect and score links disabled by the
shortening service for abuse and ```URL_BITLY_BLOCKED``` is supplied as an example.
It should be safe to score this rule highly on a match as experience shows
that bit.ly only blocks access to a URL if it has seen consistent abuse and
problem reports.

As of version 0.3 this plug-in will follow 'chained' shorteners e.g.

```short URL``` -> ```short URL``` -> ```short URL``` -> ```real URL```

If this form of chaining is found, then the rule ```SHORT_URL_CHAINED``` will be
fired.  If a loop is detected then ```SHORT_URL_LOOP``` will be fired.
This plug-in limits the number of chained shorteners to a maximim of ```10``` at 
which point it will fire the rule ```SHORT_URL_MAXCHAIN``` and go no further.

If a shortener returns a '**404 Not Found**' result for the short URL then the 
rule **'SHORT_URL_404'** will be fired.

If a shortener does not return an HTTP redirect, then a dynamic rule will
be fired: **'SHORT_\<SHORTENER\>_\<CODE\>'** where **\<SHORTENER\>** is the uppercase
name of the shortener with dots converted to underscores.  e.g.:
'SHORT_T_CO_200' This is to handle the case of t.co which now returns an
HTTP 200 and an abuse page instead of redirecting to an abuse page like
every other shortener does...

NOTES
-----

This plugin runs the parsed_metadata hook with a priority of -1 so that
it may modify the parsed URI list prior to the URIDNSBL plugin which
runs as priority 0.

Currently the plugin queries a maximum of 10 distinct shortened URLs with
a maximum timeout of 5 seconds per lookup.  

ACKNOWLEDGEMENTS
----------------

A lot of this plugin has been hacked together by using other plugins as 
examples.  The author would particularly like to tip his hat to Karsten
Bräckelmann for the _add_uri_detail_list() function that he stole from
GUDO.pm for which this plugin would not be possible due to the SpamAssassin
API making no provision for adding to the base list of extracted URIs and 
the author not knowing enough about Perl to be able to achieve this without 
a good example from someone that does ;-)

SOURCE
------

https://github.com/smfreegard/DecodeShortURLs/blob/master/README.md  
https://docs.danami.com/warden/user-guide/antispam-plugins/decodeshorturls  
https://docs.danami.com/warden/settings/antispam/plugin-settings/decodeshorturls

TESTS
-----

| Area | Test name           | Description                                                         | Default scores |
|------|---------------------|---------------------------------------------------------------------|----------------|
| body | HAS_SHORT_URL       | Message contains one or more shortened URLs                         | 0.01           |
| body | SHORT_URL_CHAINED   | Message has shortened URL chained to other shorteners               | 3.0            |
| body | SHORT_URL_MAXCHAIN  | Message has shortened URL that causes more than 10 redirections     | 5.0            |
| body | SHORT_URL_LOOP      | Message has short URL that loops back to itself                     | 0.01           |
| body | SHORT_URL_404       | Message has short URL that returns 404                              | 1.0            |
| body | SHORT_T_CO_200      | Message contains a t.co URL that has a warning due to abuse         | 10.0           |
| body | URI_BITLY_BLOCKED   | Message contains a bit.ly URL that has been disabled due to abuse   | 10.0           |
| body | URI_SIMURL_BLOCKED  | Message contains a simurl URL that has been disabled due to abuse   | 10.0           |
| body | URI_MIGRE_BLOCKED   | Message contains a migre.me URL that has been disabled due to abuse | 10.0           |
| body | URI_TINYURL_BLOCKED | Message contains a tinyurl that has been disabled due to abuse      | 10.0           |
| meta | SHORT_URIBL         | Message contains shortened URL(s) and also hits a URIDNSBL          | 0.01           |


DecodeShortURLs Settings
------------------------

**URL shortener cache** - ```url_shortener_cache```
The full path to a database file to write cache entries to. The database will be created automatically if is does not already exist but the supplied path and file must be read/writable by spamd.  
NOTE: you will need the DBD::SQLite module installed to use this feature.  
Default: /tmp/DecodeShortURLs.sq3  

**URL shortener cache TTL** - ```url_shortener_cache_ttl```
The length of time a cache entry will be valid for in seconds.  
Default: 86400

**URL shortener log** - ```url_shortener_log```
The full path to a log file to be written to. The file will be created if it does not already exist and must be writable by spamd.
Default: empty

**URL shortener log to syslog** - ```url_shortener_syslog```
Log decoded URLs to syslog.  
Default: 0

**URL shorteners** - ```url_shortener```
A list of URL shortener services (one entry per line).  
Default: empty


Install
-------

**Debian / Ubuntu:**

```
mkdir /etc/spamassassin/myplugins
wget https://raw.githubusercontent.com/smfreegard/DecodeShortURLs/master/DecodeShortURLs.pm -P /etc/spamassassin/myplugins/
chmod 644 /etc/spamassassin/myplugins/DecodeShortURLs.pm
```
