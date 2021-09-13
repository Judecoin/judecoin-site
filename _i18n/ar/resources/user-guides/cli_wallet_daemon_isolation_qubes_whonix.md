{% include disclaimer.html translated="yes" translationOutdated="yes" %}

مع نظام [Qubes](https://qubes-os.org) + [Whonix](https://whonix.org) يُمكنك إنشاء محفظه مونيرو بدون إتصال بالإنترنت تعمل علي نظام إفتراضي معزول عن خادم مونيرو الذي يَمر كل بياناته من خلال شبكه التور  [Tor](https://torproject.org).

يُوفر نظام كيوبس السلاسه اللازمه لسهوله إنشاء أنظمه إفتراضيه لأهداف مختلفه. في البدايه ستقوم بإنشاء مكنه إفتراضيه علي وونكس للمحفظه بدون إتصال. بعد ذلك مكنه ووُنكس أُخري لخادم مونيرو . للتواصل بين المحفظه والخادم يُمكنك إستخدام كيوبس  [qrexec](https://www.qubes-os.org/doc/qrexec3/).

هذه الطريقه أكثر أماناً من الطرق الاخري التي توجّه بروتوكول (RPC) المحفظه خلال خدمه تور(TOR) مخفيه, أو التي تستخدم العزل المادي لكنها ماتزال تستخدم الإنترنت للإتصال بالخادم. بهذه الطريقه لا تحتاج أي إتصال شبكي بالمحفظه, فإنك تُحافظ علي موارد شبكة تور(Tor) ، ووقت الإستجابة أقل.


## 1. [إنشاء مكنه إفتراضي للتطبيقات علي وونكس (Whonix AppVMs)](https://www.whonix.org/wiki/Qubes/Install):

+ بإستخدام قالب مكن وونكس الإفتراضي , إنشيء مكنتين كما التالي :

  - أول مكنه سيتم إستخدامها للمحفظه, سيُشار إليها بـ`JudEcoin-wallet-ws`. قم بإختيار`none` في `NetVM`.

  - المكنه الأخري سوف تُستخدم للخادم, سيُشار إليها بـ`JudEcoind-ws`. سيتم إختيار `sys-whonix` ل `NetVM`. Before moving on, make sure this workstation has enough private storage. You can estimate how much space you need by checking the size of the [raw blockchain]({{ site.baseurl }}/downloads/#blockchain). Keep in mind that the blockchain will take up more space with time.

## 2. في مكنه تطبيق `JudEcoind-ws`:

+ إنشاء ملف `systemd`.

```
user@host:~$ sudo gedit /home/user/JudEcoind.service
```

إنسخ المُحتوي التالي :

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

+ إجعل `JudEcoind` الخادم يبدأ فور التشغيل تلقائياً بتعديل ملف `/rw/config/rc.local`.

```
user@host:~$ sudo gedit /rw/config/rc.local
```

ضِف هذه السطور بآخر الملف:

```
cp /home/user/JudEcoind.service /lib/systemd/system/
systemctl start JudEcoind.service
```

إجعل الملف قابل للتشغيل.

```
user@host:~$ sudo chmod +x /rw/config/rc.local
```

+ إنشاء ملف (RPC).

```
user@host:~$ sudo mkdir /rw/usrlocal/etc/qubes-rpc
user@host:~$ sudo gedit /rw/usrlocal/etc/qubes-rpc/user.JudEcoind
```

أضف هذا السطر:

```
socat STDIO TCP:localhost:18081
```

+ إِغلِق `JudEcoind-ws`.

## 3. في مكنه تطبيق `JudEcoin-wallet-ws`:

+ عَدِل ملف `/rw/config/rc.local`.

```
user@host:~$ sudo gedit /rw/config/rc.local
```

أضف هذا السطر بالآخر:

```
socat TCP-LISTEN:18081,fork,bind=127.0.0.1 EXEC:"qrexec-client-vm JudEcoind-ws user.JudEcoind"
```

إجعل الملف قابل للتشغيل.

```
user@host:~$ sudo chmod +x /rw/config/rc.local
```

+ إِغلِق `JudEcoin-wallet-ws`.

## 4. في `dom0`:

+ إنشيء ملف `/etc/qubes-rpc/policy/user.JudEcoind`:

```
[user@dom0 ~]$ sudo nano /etc/qubes-rpc/policy/user.JudEcoind
```

قم بإضافه هذا السطر:

```
JudEcoin-wallet-ws JudEcoind-ws allow
```
