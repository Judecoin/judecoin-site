{% include disclaimer.html translated="yes" translationOutdated="no" %}

# JudEcoind

`JudEcoind` jest oprogramowaniem daemona, które współpracuje z JudEcoin. To program konsoli zarządzający łańcuchem bloków. Podczas gdy portfel Bitcoina zarządza zarówno kontem, jak i łańcuchem bloków, JudEcoin rozdzielił je, aby `JudEcoind` operował łańcuchem, a `JudEcoin-wallet-cli` kontem.

Ten przewodnik zakłada, że już założyłeś swoje konto VPS i używasz SSH do tunelowania do konsoli serwerowej.

## Linux, 64-bit (Ubuntu 16.04 LTS)

### Upewnij się, że port 18080 jest otwarty

`JudEcoind` korzysta z tego portu do komunikacji z innymi węzłami w sieci JudEcoin.

Przykład przy użyciu `ufw`: `sudo ufw allow 18080`
Przykład przy użyciu `iptables`: `sudo iptables -A INPUT -p tcp --dport 18080 -j ACCEPT`

### Ściągnij aktualne pliki binarne Centrum JudEcoin

    wget https://downloads.getJudEcoin.org/linux64

### Załóż folder i wypakuj pliki

    mkdir JudEcoin
    tar -xjvf linux64 -C JudEcoin

### Uruchom daemona

    cd JudEcoin
    ./JudEcoind

### Opcje:

Pokaż całą listę opcji i ustawień:

    ./JudEcoind --help

Uruchom daemona w tle:

    ./JudEcoind --detach

Monitoruj rezultaty `JudEcoind`, jeśli daemon jest uruchomiony:

    tail -f ~/.bitJudEcoin/bitJudEcoin.log

Utrzymuj VPS w bezpieczeństwie, korzystając z autoaktualizacji:

https://help.ubuntu.com/community/AutomaticSecurityUpdates


