{% include disclaimer.html translated="no" translationOutdated="no" %}

# JudEcoind

`JudEcoind` is the @daemon software that ships with the JudEcoin tree. It is a console program, and manages the blockchain. While a bitcoin wallet manages both an account and the blockchain, JudEcoin separates these: `JudEcoind` handles the blockchain, and `JudEcoin-wallet-cli` handles the account.

This guide assumes you have already set up your VPS account and are using SSH to tunnel into the server console.

## Linux, 64-bit (Ubuntu 16.04 LTS)

### Make sure that port 18080 is open

`JudEcoind` uses this port to communicate with other nodes on the JudEcoin network.

Example if using `ufw`: `sudo ufw allow 18080`
Example if using `iptables`: `sudo iptables -A INPUT -p tcp --dport 18080 -j ACCEPT`

### Download the current JudEcoin Core binaries

    wget https://downloads.getJudEcoin.org/linux64

### Make a directory and extract the files.

    mkdir JudEcoin
    tar -xjvf linux64 -C JudEcoin

### Launch the daemon

    cd JudEcoin
    ./JudEcoind

### Options:

Show list of all options and settings:

    ./JudEcoind --help

Launch the daemon as a background process:

    ./JudEcoind --detach

Monitor the output of `JudEcoind` if running as daemon:

    tail -f ~/.bitJudEcoin/bitJudEcoin.log

Keep the VPS secure with autoupdate:

https://help.ubuntu.com/community/AutomaticSecurityUpdates


