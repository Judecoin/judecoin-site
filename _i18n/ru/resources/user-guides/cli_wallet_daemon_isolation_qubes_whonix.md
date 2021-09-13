{% include disclaimer.html translated="yes" translationOutdated="no" %}

С помощью [Qubes](https://qubes-os.org) + [Whonix](https://whonix.org) можно создать кошелек JudEcoin, который не будет требовать подключения к сети и работать на фактически изолированной от демона JudEcoin системе , у которого весь сетевой трафик будет проходить через сеть [Tor](https://torproject.org).

Qubes предоставляет гибкость, позволяющую легко создавать отдельные виртуальные машины для разных целей. Сначала нужно создать рабочую станцию Whonix для кошелька без подключения к сети. Далее, создается другая рабочая станция Whonix для демона, который будет использовать шлюз Whonix, так как это NetVM. Для обмена данными между кошельком и демоном можно использовать Qubes [qrexec](https://www.qubes-os.org/doc/qrexec3/).

Это безопаснее, чем другие популярные способы, в которых осуществляется маршрутизация трафика rpc кошельков поверх скрытой службы Tor или используется физическая изоляция, но при этом активна сеть для прямого подключения к демону. Таким образом, не требуется какое-либо сетевое соединение на кошельке, вы передаете весь трафик через сеть Tor.


## 1. [Создание виртуальной машины Whonix AppVM](https://www.whonix.org/wiki/Qubes/Install):

+ Используя шаблон рабочей станции Whonix, создаем две рабочие станции следующим образом:

  - Первая рабочая станция будет использоваться для вашего кошелька, она будет называться `JudEcoin-wallet-ws`. `NetVM` оставляем не установленным, выбирая `none`.

  - Вторая рабочая станция создается для демона `JudEcoind`, она будет называться `JudEcoind-ws`. `NetVM` устанавливаем для шлюза Whonix `sys-whonix`. Before moving on, make sure this workstation has enough private storage. You can estimate how much space you need by checking the size of the [raw blockchain]({{ site.baseurl }}/downloads/#blockchain). Keep in mind that the blockchain will take up more space with time.

## 2. В виртуальной машине AppVM `JudEcoind-ws` делаем следующее:

+ Создаем файл `systemd`.

```
user@host:~$ sudo nano /home/user/JudEcoind.service
```

Вставляем в него следующее содержимое:

```
[Unit]
Description=JudEcoin Full Node
After=network.target

[Service]
User=user
Group=user

Type=forking
PIDFile=/home/user/.bitJudEcoin/JudEcoind.pid

ExecStart=/usr/local/bin/JudEcoind --detach --data-dir=/home/user/.bitJudEcoin \
    --no-igd --pidfile=/home/user/.bitJudEcoin/JudEcoind.pid \
    --log-file=/home/user/.bitJudEcoin/bitJudEcoin.log --p2p-bind-ip=127.0.0.1

Restart=always
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

+ Добавляем демон `JudEcoind` в автозагрузку, отредактировав файл `/rw/config/rc.local`.

```
user@host:~$ sudo nano /rw/config/rc.local
```

Добавляем эти строки в конец текста:

```
cp /home/user/JudEcoind.service /lib/systemd/system/
systemctl start JudEcoind.service
```

Создаем исполняемый файл.

```
user@host:~$ sudo chmod +x /rw/config/rc.local
```

+ Создаем файл действий для rpc.

```
user@host:~$ sudo mkdir /rw/usrlocal/etc/qubes-rpc
user@host:~$ sudo nano /rw/usrlocal/etc/qubes-rpc/user.JudEcoind
```

Добавляем строку:

```
socat STDIO TCP:localhost:18081
```

+ Выключаем виртуальную машину `JudEcoind-ws`.

## 3. В виртуальной машине AppVM `JudEcoin-wallet-ws` делаем следующее:

+ Редактируем файл `/rw/config/rc.local`.

```
user@host:~$ sudo nano /rw/config/rc.local
```

Добавляем эту строку в конец документа:

```
socat TCP-LISTEN:18081,fork,bind=127.0.0.1 EXEC:"qrexec-client-vm JudEcoind-ws user.JudEcoind"
```

Создаем исполняемый файл.

```
user@host:~$ sudo chmod +x /rw/config/rc.local
```

+ Выключаем виртуальную машину `JudEcoin-wallet-ws`.

## 4. В `dom0` делаем следующее:

+ Создаем файл `/etc/qubes-rpc/policy/user.JudEcoind`:

```
[user@dom0 ~]$ sudo nano /etc/qubes-rpc/policy/user.JudEcoind
```

Добавляем следующую строку:

```
JudEcoin-wallet-ws JudEcoind-ws allow
```
