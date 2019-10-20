## TP3 Linux

- Connectez vous au host "proxy" avec vagrant et vérifier Comment est configuré le resolver dns du système ?  
Le fichier resolver dns est dans le fichier 
```
/etc/resolve.conf
```   
Les iPs dans ce fichier sont celle des machines recursive  


- Retrouvez l'adresse ip du host wiki.lab.local avec la commande dig.
```
vagrant@proxy:/etc$ dig wiki.lab.local +short
192.168.56.11
```

- Connectez vous au host auth-1, quels sont les services réseaux qui sont en fonctionnement actuellement quels sont leur socket d'écoute ?  
```sudo netstat -pauntl | grep -v ESTABLISHED``` pour afficher les ports en en attente de connexion
```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      6357/mysqld
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/systemd
tcp        0      0 192.168.33.31:80        0.0.0.0:*               LISTEN      6408/httpd
tcp        0      0 0.0.0.0:53              0.0.0.0:*               LISTEN      6426/pdns_server
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      2373/sshd
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      2630/master
tcp6       0      0 :::111                  :::*                    LISTEN      1/systemd
tcp6       0      0 :::53                   :::*                    LISTEN      6426/pdns_server
tcp6       0      0 :::22                   :::*                    LISTEN      2373/sshd
tcp6       0      0 ::1:25                  :::*                    LISTEN      2630/master
udp        0      0 0.0.0.0:996             0.0.0.0:*                           1302/rpcbind
udp        0      0 0.0.0.0:53              0.0.0.0:*                           6426/pdns_server
udp        0      0 127.0.0.1:323           0.0.0.0:*                           1365/chronyd
udp        0      0 0.0.0.0:68              0.0.0.0:*                           6465/dhclient
udp        0      0 0.0.0.0:12632           0.0.0.0:*                           6426/pdns_server
udp        0      0 0.0.0.0:111             0.0.0.0:*                           1/systemd
udp6       0      0 :::996                  :::*                                1302/rpcbind
udp6       0      0 :::14600                :::*                                6426/pdns_server
udp6       0      0 :::53                   :::*                                6426/pdns_server
udp6       0      0 ::1:323                 :::*                                1365/chronyd
udp6       0      0 :::111                  :::*                                1/systemd
```
On peut voir des services tourner comme Mysql, chron

- Connectez vous au host recursor-1,  quels sont les services réseaux qui sont en fonctionnement actuellement quels sont leur socket d'écoute ?
```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      1/systemd
tcp        0      0 192.168.33.21:53        0.0.0.0:*               LISTEN      6012/pdns_recursor
tcp        0      0 127.0.0.1:53            0.0.0.0:*               LISTEN      6012/pdns_recursor
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      2374/sshd
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      2612/master
tcp6       0      0 :::111                  :::*                    LISTEN      1/systemd
tcp6       0      0 :::22                   :::*                    LISTEN      2374/sshd
tcp6       0      0 ::1:25                  :::*                    LISTEN      2612/master
udp        0      0 0.0.0.0:996             0.0.0.0:*                           1300/rpcbind
udp        0      0 192.168.33.21:53        0.0.0.0:*                           6012/pdns_recursor
udp        0      0 127.0.0.1:53            0.0.0.0:*                           6012/pdns_recursor
udp        0      0 127.0.0.1:323           0.0.0.0:*                           1490/chronyd
udp        0      0 0.0.0.0:68              0.0.0.0:*                           6023/dhclient
udp        0      0 0.0.0.0:111             0.0.0.0:*                           1/systemd
udp6       0      0 :::996                  :::*                                1300/rpcbind
udp6       0      0 ::1:323                 :::*                                1490/chronyd
udp6       0      0 :::111                  :::*                                1/systemd
```
Ici on peut voir des services touner comme pdns_recursor, Chron

- Où sont configuré chacuns de ces composants ?  
pour trouver les composants modifié, on cherche les fichier contenant ".orig" qui signifie que quelqu'un a modifier ce fichier et garder une copie de l'originale dans le .orig



- Qu'est ce qui est configuré sur les serveurs recursifs pour le domaine lab.local ? (Important pour les Actions qui suivent)


- Comment mettre en évidence le fait que le récurseurs ne répondent que sur l’interface du réseaux back (192.168.33.0/24) ?


- Comment est sécurisé l’accès à mysql ?