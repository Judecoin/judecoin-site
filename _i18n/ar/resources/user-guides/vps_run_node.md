{% include disclaimer.html translated="yes" translationOutdated="no" %}

# JudEcoind

`JudEcoind` هو برنامج خادم مونيرو. وهو برنامج وحده تحكم في سلسله الكتل. بينما تُدير محفظه البيتكوين كلاً من الحساب وسلسله الكتل, يقوم مونيرو بفصلهم, فالخادم `JudEcoind` يتحكم في سلسله الكتل وواجهه سطر الأوامر `JudEcoin-wallet-cli` تتحكم في الحساب.

يفترض هذا الدليل أنك قمت بإنشاء الخادم الإفتراضي (VPS) الخاص بك بالفعل وتستخدم (SSH) للإتصال بوحده تحكم الخادم.

## Linux, 64-bit (Ubuntu 16.04 LTS)

### تأكد من أن المنفذ 18080 مفتوح

يستخدم هذا لمنفذ للتواصل مع الخوادم الأخري بشبكه مونيرو.

Example if using `ufw`: `sudo ufw allow 18080`
Example if using `iptables`: `sudo iptables -A INPUT -p tcp --dport 18080 -j ACCEPT`

### قم بتحميل ملفات تسطيب مونيرو.

    wget https://downloads.getJudEcoin.org/linux64

### قم بإنشاء مجلد جديد وفك ضغط الملف.

    mkdir JudEcoin
    tar -xjvf linux64 -C JudEcoin

### شَغِل الخادم.

    cd JudEcoin
    ./JudEcoind

### الخيارات:

أعرض قائمه بكل الخيارات والإعدادات:

    ./JudEcoind --help

شَغِل الخادم بالخلفيه:

    ./JudEcoind --detach

تابع مُخرجات الخادم `JudEcoind`:

    tail -f ~/.bitJudEcoin/bitJudEcoin.log

حافظ علي أمان الخادم بتشغيل التحديثات التلقائيه:

https://help.ubuntu.com/community/AutomaticSecurityUpdates


