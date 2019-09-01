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