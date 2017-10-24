# Config files, etc., for R4L memcache server

## Memcache services

***Important: before starting the `memcached` services on the host, edit the `/etc/sysconfig/memcached.xxxxx` files to listen to the host's private IP***


``` bash
# Clone the repo
git clone https://github.com/junemedia/memcached.recipe4living.com.git /srv

# link config files
ln -s /srv/etc/sysconfig/memcached.12590 /etc/sysconfig/memcached.12590
ln -s /srv/etc/sysconfig/memcached.12591 /etc/sysconfig/memcached.12591
ln -s /srv/etc/sysconfig/memcached.12595 /etc/sysconfig/memcached.12595

# link unit files
ln -s /srv/etc/systemd/system/memcached-12590.service /etc/systemd/system/memcached-12590.service
ln -s /srv/etc/systemd/system/memcached-12591.service /etc/systemd/system/memcached-12591.service
ln -s /srv/etc/systemd/system/memcached-12595.service /etc/systemd/system/memcached-12595.service

# let systemd know about the new files
systemctl daemon-reload

# start the memcached services
systemctl start memcached-12590.service
systemctl start memcached-12591.service
systemctl start memcached-12595.service

# enable services at boot
systemctl enable memcached-12590.service
systemctl enable memcached-12591.service
systemctl enable memcached-12595.service
```

In a pinch, these can just be run from the command line:

```
/usr/bin/memcached -u nobody -d -c 5000 -m 1024 -l 10.209.68.182 -p 12590 -v 2 >> /tmp/memcache.12590.log
/usr/bin/memcached -u nobody -d -c 5000 -m 1024 -l 10.209.68.182 -p 12591 -v 2 >> /tmp/memcache.12591.log
/usr/bin/memcached -u nobody -d -c 5000 -m 64 -l 10.209.68.182 -p 12595 -v 2 >> /tmp/memcache.12595.log
```

