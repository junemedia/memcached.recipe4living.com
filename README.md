# Config files, etc., for R4L memcache server

## Memcache services

***Important: before starting the `memcached` services on the host, edit the `/etc/sysconfig/memcached.xxxxx` files to listen to the host's private IP***


``` bash
# Clone the repo
cd ~
git clone https://github.com/junemedia/memcached.recipe4living.com.git ./memcached
cd memcached

# ---------------------------------------------------------------------
# Important: Edit etc/sysconfig/memcached.xxxxx files to listen on
# the host's private IP
# ---------------------------------------------------------------------

# copy config files
sudo cp etc/sysconfig/memcached.12590 /etc/sysconfig/
sudo cp etc/sysconfig/memcached.12591 /etc/sysconfig/
sudo cp etc/sysconfig/memcached.12595 /etc/sysconfig/

# copy unit files
sudo cp etc/systemd/system/memcached-12590.service /etc/systemd/system/
sudo cp etc/systemd/system/memcached-12591.service /etc/systemd/system/
sudo cp etc/systemd/system/memcached-12595.service /etc/systemd/system/

# let systemd know about the new files
sudo systemctl daemon-reload

# start the memcached services
sudo systemctl start memcached-12590.service
sudo systemctl start memcached-12591.service
sudo systemctl start memcached-12595.service

# enable services at boot
sudo systemctl enable memcached-12590.service
sudo systemctl enable memcached-12591.service
sudo systemctl enable memcached-12595.service
```

In a pinch, these can just be run from the command line:

```
sudo /usr/bin/memcached -u nobody -d -c 5000 -m 1024 -l 10.209.68.182 -p 12590 -v 2 >> /tmp/memcache.12590.log
sudo /usr/bin/memcached -u nobody -d -c 5000 -m 1024 -l 10.209.68.182 -p 12591 -v 2 >> /tmp/memcache.12591.log
sudo /usr/bin/memcached -u nobody -d -c 5000 -m 64 -l 10.209.68.182 -p 12595 -v 2 >> /tmp/memcache.12595.log
```

