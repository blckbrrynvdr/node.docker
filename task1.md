## Задание 1 - Docker CLI

1. Загрузите образ `busybox` последней версии
```
docker pull busybox:latest
```
```
latest: Pulling from library/busybox
7b2699543f22: Pull complete
Digest: sha256:c3839dd800b9eb7603340509769c43e146a74c63dca3045a8e7dc8ee07e53966
Status: Downloaded newer image for busybox:latest
docker.io/library/busybox:latest

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview busybox:latest
```
2. Запустите новый контейнер `busybox` с командой `ping` сайта `netology.ru`, и количеством пингов 7, поименуйте контейнер `pinger`
```
docker run -d --name pinger busybox ping -c 7 netology.ru
```
```
66b4ac3e892182918242349227b9e35dd9ffbf01d54ac799dc24b9b8b4d6b02b
```
3. Выведите на список всех контейнеров - запущенных и остановленных
```
docker ps -a
```
```
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS                          PORTS     NAMES
66b4ac3e8921   busybox   "ping -c 7 netology.…"   About a minute ago   Exited (0) About a minute ago             pinger
```
4. Выведите на экран логи контейнера с именем `pinger`
```
docker logs pinger
```
```
PING netology.ru (188.114.98.224): 56 data bytes
64 bytes from 188.114.98.224: seq=0 ttl=63 time=9.560 ms
64 bytes from 188.114.98.224: seq=1 ttl=63 time=6.498 ms
64 bytes from 188.114.98.224: seq=2 ttl=63 time=14.671 ms
64 bytes from 188.114.98.224: seq=3 ttl=63 time=10.017 ms
64 bytes from 188.114.98.224: seq=4 ttl=63 time=23.373 ms
64 bytes from 188.114.98.224: seq=5 ttl=63 time=6.250 ms
64 bytes from 188.114.98.224: seq=6 ttl=63 time=7.294 ms

--- netology.ru ping statistics ---
7 packets transmitted, 7 packets received, 0% packet loss
round-trip min/avg/max = 6.250/11.094/23.373 ms
```
5. Запустите второй раз контейнер с именем `pinger`
```
docker start pinger
```
```
pinger
```
6. Выведите на экран список всех контейнеров - запущенных и остановленных
```
docker ps -a
```
```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                      PORTS     NAMES
66b4ac3e8921   busybox   "ping -c 7 netology.…"   5 minutes ago   Exited (0) 44 seconds ago             pinger
```
7. Выведите на экран логи контейнера с именем `pinger`
```
docker logs pinger
```
```
PING netology.ru (188.114.98.224): 56 data bytes
64 bytes from 188.114.98.224: seq=0 ttl=63 time=9.560 ms
64 bytes from 188.114.98.224: seq=1 ttl=63 time=6.498 ms
64 bytes from 188.114.98.224: seq=2 ttl=63 time=14.671 ms
64 bytes from 188.114.98.224: seq=3 ttl=63 time=10.017 ms
64 bytes from 188.114.98.224: seq=4 ttl=63 time=23.373 ms
64 bytes from 188.114.98.224: seq=5 ttl=63 time=6.250 ms
64 bytes from 188.114.98.224: seq=6 ttl=63 time=7.294 ms

--- netology.ru ping statistics ---
7 packets transmitted, 7 packets received, 0% packet loss
round-trip min/avg/max = 6.250/11.094/23.373 ms
PING netology.ru (188.114.99.224): 56 data bytes
64 bytes from 188.114.99.224: seq=0 ttl=63 time=7.245 ms
64 bytes from 188.114.99.224: seq=1 ttl=63 time=7.613 ms
64 bytes from 188.114.99.224: seq=2 ttl=63 time=11.224 ms
64 bytes from 188.114.99.224: seq=3 ttl=63 time=8.323 ms
64 bytes from 188.114.99.224: seq=4 ttl=63 time=8.240 ms
64 bytes from 188.114.99.224: seq=5 ttl=63 time=7.172 ms
64 bytes from 188.114.99.224: seq=6 ttl=63 time=10.194 ms

--- netology.ru ping statistics ---
7 packets transmitted, 7 packets received, 0% packet loss
round-trip min/avg/max = 7.172/8.573/11.224 ms
```
8. Определите по логам общее количество запусков команды `ping` и какое общее количество отправленых запросов
```
(docker logs pinger | select-string -Pattern 'PING' -CaseSensitive -SimpleMatch).count
```
```
2
```
```
(docker logs pinger | select-string -Pattern 'seq' -CaseSensitive -SimpleMatch).count
```
```
14
```
9.  Удалите контейнер с именем `pinger`
```
docker rm pinger
```
```
pinger
```
10. Удалите образ `busybox`
```
docker rmi busybox
```
```
Untagged: busybox:latest
Untagged: busybox@sha256:c3839dd800b9eb7603340509769c43e146a74c63dca3045a8e7dc8ee07e53966
Deleted: sha256:ba5dc23f65d4cc4a4535bce55cf9e63b068eb02946e3422d3587e8ce803b6aab
Deleted: sha256:95c4a60383f7b6eb6f7b8e153a07cd6e896de0476763bef39d0f6cf3400624bd
```
