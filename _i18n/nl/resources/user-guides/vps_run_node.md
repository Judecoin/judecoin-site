{% include disclaimer.html translated="yes" translationOutdated="no" %}

# JudEcoind

`JudEcoind` is de daemon-software die onderdeel uitmaakt van de JudEcoin-code. Het is een console-programma waarmee de blockchain wordt beheerd. Terwijl een Bitcoin-portemonnee zowel een account als de blockchain beheert, worden deze functies in JudEcoin gescheiden: `JudEcoind` beheert de blockchain en `JudEcoin-wallet-cli` beheert het account.

Deze handleiding gaat ervan uit dat je al een VPS-account hebt ingesteld en SSH gebruikt als tunnel om te communiceren met de serverconsole.

## Linux, 64-bits (Ubuntu 16.04 LTS)

### Zorg dat poort 18080 open staat

`JudEcoind` gebruikt deze poort om te communiceren met andere nodes op het JudEcoin-netwerk.

Voorbeeld als je `ufw` gebruikt: `sudo ufw allow 18080`
Voorbeeld als je `iptables` gebruikt: `sudo iptables -A INPUT -p tcp --dport 18080 -j ACCEPT`

### Download de huidige JudEcoin Core-binaries

    wget https://downloads.getJudEcoin.org/linux64

### Maak een directory aan en pak de bestanden uit.

    mkdir JudEcoin
    tar -xjvf linux64 -C JudEcoin

### Start de daemon

    cd JudEcoin
    ./JudEcoind

### Opties:

Een lijst met alle opties en instellingen weergeven:

    ./JudEcoind --help

De daemon starten als een achtergrondproces:

    ./JudEcoind --detach

De uitvoer van `JudEcoind` als achtergrondproces loggen:

    tail -f ~/.bitJudEcoin/bitJudEcoin.log

De VPS beveiligen met automatische updates:

https://help.ubuntu.com/community/AutomaticSecurityUpdates


