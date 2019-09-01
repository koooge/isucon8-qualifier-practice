# isucon8-qualify-practice

LISTENしてるserviceのport一覧
```
$ ss -lt4n
State       Recv-Q Send-Q     Local Address:Port                    Peer Address:Port
LISTEN      0      100            127.0.0.1:25                                 *:*
LISTEN      0      50                     *:3306                               *:*
LISTEN      0      128                    *:111                                *:*
LISTEN      0      128                    *:80                                 *:*
LISTEN      0      128                    *:8080                               *:*
LISTEN      0      128                    *:22                                 *:*
```

isuconユーザーが起動しているprocess一覧

```
$ ps xu
[isucon@localhost ~]$ ps ux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
isucon     390  0.0  0.0 198392   312 ?        Ss   05:41   0:00 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     449  0.1  0.6 354920  6728 ?        S    05:41   0:05 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     450  0.0  0.0 319236   180 ?        S    05:41   0:03 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     451  0.0  0.1 319216  1976 ?        S    05:41   0:03 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     453  0.0  0.0 318788   232 ?        S    05:41   0:02 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     454  0.0 38.7 752284 393536 ?       S    05:41   0:03 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     455  0.0  0.0 318804   296 ?        S    05:41   0:03 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     456  0.0  0.0 319004   308 ?        S    05:41   0:03 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     458  0.0  0.1 346408  1872 ?        S    05:41   0:04 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     459  0.0  0.0 327188   260 ?        S    05:41   0:02 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon     460  0.0 19.6 751680 199516 ?       S    05:41   0:03 /home/isucon/torb/webapp/perl/local/bin/plackup
isucon    3441  0.0  0.2 116624  2232 pts/1    S    05:43   0:00 -bash
isucon    3829  0.0  0.3  37008  3820 ?        Sl   06:26   0:00 /usr/sbin/h2o -c /etc/h2o/h2o.conf
isucon    4338  0.0  0.1 155360  1876 pts/1    R+   06:55   0:00 ps ux
```

nodejsの参考実装に切り替え
```
$ sudo systemctl stop torb.perl
$ sudo systemctl disable torb.perl
$ sudo systemctl start torb.nodejs
$ sudo systemctl enable torb.nodejs
$ sudo reboot
$ ps ux
[isucon@localhost ~]$ ps ux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
isucon    1034  0.0  0.3  37008  3816 ?        Sl   07:03   0:00 /usr/sbin/h2o -c /etc/h2o/h2o.conf
isucon    1404  4.9  6.5 1030136 66848 ?       Ssl  07:03   0:00 /home/isucon/local/node/bin/node /home/isucon/torb/webapp/nodejs/node_modules/.bin/ts-node index.ts
isucon    1459  0.5  0.2 116376  3032 pts/0    S    07:03   0:00 -bash
isucon    1483  0.0  0.1 155360  1872 pts/0    R+   07:03   0:00 ps ux
```

h2oからnginxに切り替え
```
$ yum check-update
$ sudo yum update
$ sudo yum install nginx
$ sudo systemctl stop h2o
$ sudo systemctl disable h2o
$ sudo systemctl start nginx
$ sudo systemctl enable nginx
$ sudo reboot
$ ps ux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
isucon    1415  0.0  8.0 1034128 81824 ?       Ssl  07:09   0:01 /home/isucon/local/node/bin/node /home/isucon/torb/webapp/nodejs/node_modules/.bin/ts-node index.ts
isucon    1462  0.0  0.3 116720  3532 pts/0    S    07:09   0:01 -bash
isucon    2756  0.0  0.3 125496  3136 ?        S    07:47   0:00 nginx: worker process
isucon    3222  0.0  0.1 155360  1876 pts/0    R+   07:58   0:00 ps ux
```