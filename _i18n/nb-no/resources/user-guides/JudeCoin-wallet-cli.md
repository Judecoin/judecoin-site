{% include disclaimer.html translated="yes" translationOutdated="no" %}

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
`JudEcoin-wallet-cli` er lommebokprogramvaren som kommer sammen med JudEcoin tree. Det er et konsollprogram og administrerer en konto. Mens en bitcoin-lommebok håndterer både en konto og blokkjeden, separerer JudEcoin disse: `JudEcoind` håndterer blokkjeden, og `JudEcoin-wallet-cli` håndterer kontoen.

Denne veiledningen viser deg hvordan man utfører ulike operasjoner fra `JudEcoin-wallet-cli`-UI-en. Veiledningen antar at du bruker den siste versjonen av JudEcoin og allerede har opprettet en konto i henhold til de andre veiledningene.
=======
`monero-wallet-cli` is the wallet software shipped in the Monero
archives. It is a console program, and manages an account. While a bitcoin
wallet manages both an account and the blockchain, Monero separates these:
`monerod` handles the blockchain, and `monero-wallet-cli` handles the
account.

This guide will show how to perform various operations with
`monero-wallet-cli`. The guide assumes you are using the most recent version
of Monero and have already created an account according to the other guides.
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

## Overview

You can have a list of the most important commands by running `help`:

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
Fordi håndteringen av blokkjeden og lommeboken er separate programmer, må mye av bruken av `JudEcoin-wallet-cli` skje med @daemon. Dette omfatter å se etter innkommende transaksjoner til adressen din.
Når du kjører både `JudEcoin-wallet-cli` og `JudEcoind`, kan du taste inn `balance.`
=======
```
Important commands:
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

"welcome" - Show welcome message.
"help all" - Show the list of all available commands.
"help <command>" - Show a command's documentation.
"apropos <keyword>" - Show commands related to a keyword.

"wallet_info" - Show wallet main address and other info.
"balance" - Show balance.
"address all" - Show all addresses.
"address new [<label text with white spaces allowed>]" - Create new subaddress.
"transfer <address> <amount>" - Send XMR to an address.
"show_transfers [in|out|pending|failed|pool]" - Show transactions.
"sweep_all <address>" - Send whole balance to another wallet.
"seed" - Show secret 25 words that can be used to recover this wallet.
"refresh" - Synchronize wallet with the Monero network.
"status" - Check current status of wallet.
"version" - Check software version.
"exit" - Exit wallet.

"donate <amount>" - Donate XMR to the development team.
```

## Checking your balance

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
## Å sende JudEcoin
=======
Fordi håndteringen av blokkjeden og lommeboken er separate programmer, må
mye av bruken av `monero-wallet-cli` skje med @daemon. Dette omfatter å se
etter innkommende transaksjoner til adressen din.  Når du kjører både
`monero-wallet-cli` og `monerod`, kan du taste inn `balance.`
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

Output:

```
Currently selected account: [0] Primary account
Tag: (No tag assigned)
Balance: 7.499942880000, unlocked balance: 7.499942880000
```

In this example you're viewing the balance of your primary account (with
index `[0]`). `Balance` is your total balance. The `unlocked balance` is the
amount currently available to spend. Newly received transactions require 10
confirmations on the blockchain before being unlocked.

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
Bytt ut `ADDRESS` med adressen du vil sende til, `AMOUNT` med hvor mange JudEcoin du vil sende, og `PAYMENTID` med betalings-ID-en du ble gitt. Betalings-ID-er er valgfrie. Hvis mottakeren ikke trenger en, kan du bare sløyfe det.
=======
## Sending monero
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

You will need the standard address you want to send to (a long string
starting with '4' or a '8'). The command structure is:

```
transfer ADDRESS AMOUNT
```

Replace `ADDRESS` with the address you want to send to and `AMOUNT` with how
many monero you want to send.

## Receiving monero

If you have your own Monero address, you just need to give your address to
someone.

You can find out your primary address with:

```
address
```

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
## Å motta JudEcoin

Hvis du har din egen JudEcoin-adresse, trenger du bare å gi din standardadresse til noen.
=======
Since Monero is anonymous, you won't see the origin address the funds you
receive came from. If you want to know, for instance to credit a particular
customer, you'll have to tell the sender to use a payment ID, which is an
arbitrary optional tag which gets attached to a transaction. It's not
possible to use standalone payment addresses, but you can generate an
address that already includes a random payment ID (integrated addresss)
using `integrated_address`:

```
Random payment ID: <82d79055f3b27f56>
Matching integrated address: 4KHQkZ4MmVePC2yau6Mb8vhuGGy8LVdsZD8CFcQJvr4BSTfC5AQX3aXCn5RiDPjvsEHiJu1TC1ybR8pRTCbZM5bhTrAD3HDwWMtAn1K7nV
```
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

This will generate a random payment ID, and give you the address that
includes your own account and that payment ID. If you want to select a
particular payment ID, you can do that too. Use:

```
integrated_address 82d79055f3b27f56
```

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
I og med at JudEcoin er anonymt, vil du ikke se avsenders adresse som midlene du mottok kom fra. Hvis du vil vite det, for eksempel for å kreditere en spesifikk kunde, må du be senderen om å bruke en betalings-ID, som er en vilkårlig og valgfri merkelapp som festes til en transaksjon. For å gjøre livet enklere, kan du generere en adresse som allerede inkluderer en tilfeldig betalings-ID:
=======
Payments made to an integrated address generated from your account will go
to your account, with that payment ID attached, so you can tell payments
apart.
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

### Using subaddresses

It's suggested to use subaddresses (starting with `8`) instead of your main
address (starting with `4`) to receive funds. Run:

```
address new [<label text with white spaces allowed>]
```

This will generate a subaddress and its optional label, which addess you can
share to receive payment on the account it's linked to.  For example,

```
address new github_donations
```

will generate a subaddress and its label 'github_donations'.

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
Hvis du betaler en forhandler og forhandleren påstår å ikke ha mottatt midlene, må du kunne bevise for en tredjepart at du har sendt midlene – eller til og med til forhandleren, dersom det er en ærlig feil. JudEcoin er privat, så du kan ikke bare vise til transaksjonen din i blokkjeden, i og med at man ikke kan fastslå hvem som har sendt det, og hvem som mottok det. Ved å forsyne parten med en «per-transaction»-privat nøkkel, kan den parten si hvorvidt den transaksjonen sendte JudEcoin til den bestemte adressen eller ikke. Merk at å lagre disse «per-transaction»-nøklene er deaktivert som standard, så du må aktivere det før du sender hvis du tror du kan få bruk for det:
=======
To view all generated addresses, run:
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

```
address all
```

## Proving to a third party you paid someone

Hvis du betaler en forhandler og forhandleren påstår å ikke ha mottatt
midlene, må du kunne bevise for en tredjepart at du har sendt midlene –
eller til og med til forhandleren, dersom det er en ærlig feil. Monero er
privat, så du kan ikke bare vise til transaksjonen din i blokkjeden, i og
med at man ikke kan fastslå hvem som har sendt det, og hvem som mottok
det. Ved å forsyne parten med en «per-transaction»-privat nøkkel, kan den
parten si hvorvidt den transaksjonen sendte monero til den bestemte adressen
eller ikke. Merk at å lagre disse «per-transaction»-nøklene er deaktivert
som standard, så du må aktivere det før du sender hvis du tror du kan få
bruk for det:

<<<<<<< HEAD:_i18n/nb-no/resources/user-guides/JudEcoin-wallet-cli.md
Hvis du er tredjeparten (altså om noen vil bevise til deg at de har sendt JudEcoin til en adresse), kan du sjekke det slik:

    check_tx_key TXID TXKEY ADDRESS

Bytt ut `TXID`, `TXKEY` og `ADDRESS` med henholdsvis transaksjons-ID-en, per-transaction-nøkkel og mottakeradressen som ble gitt til deg. JudEcoin-wallet-cli vil sjekke den transaksjonen og gi deg beskjed om hvor mye JudEcoin denne transaksjonen utbetalte til den oppgitte adressen.
=======
```
set store-tx-info 1
```

Du kan finne igjen tx-nøkkelen fra en tidligere transaksjon slik:
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/nb-no/resources/user-guides/monero-wallet-cli.md

```
get_tx_key 1234567890123456789012345678901212345678901234567890123456789012
```

Legg inn transaksjons-ID-en som du ønsker nøkkelen for. Husk at en betaling
må splittes inn i mer enn én transaksjon, så du trenger kanskje flere
nøkler. Du kan deretter sende den nøkkelen eller disse nøklene til hvem nå
enn du vil sende bevis på transaksjonen din til sammen med
transaksjons-ID-en og adressen du sendte til. Merk at denne tredjeparten
også vil kunne se hvor mye veksel som ble sendt tilbake til deg dersom
vedkommende kjenner til din adresse.

Hvis du er tredjeparten (altså om noen vil bevise til deg at de har sendt
monero til en adresse), kan du sjekke det slik:

```
check_tx_key TXID TXKEY ADDRESS
```

Replace `TXID`, `TXKEY` and `ADDRESS` with the transaction ID,
per-transaction key, and destination address which were supplied to you,
respectively. `monero-wallet-cli` will check that transaction and let you
know how much monero this transaction paid to the given address.

## How to find a payment to you

Hvis du har mottatt en betaling ved bruk av en bestemt betalings-ID, kan du
slå den opp:

```
payments PAYMENTID
```

Du kan også gi dem mer enn én betalings-ID.

Mer generelt kan du gjennomgå innkommende og utgående betalinger:

```
show_transfers
```

Du kan gi en valgfri høyde for å kun liste opp nylige transaksjoner og kun
be om innkommende eller utgående transaksjoner.

```
show_transfers in 650000
```

vil for eksempel kun vise innkommende overføringer etter blokk 650 000. Du
kan også gi et høydeintervall.

Hvis du vil utvinne, kan du gjøre det fra lommeboken:

```
start_mining 2
```

Dette setter i gang utvinning på daemonen ved bruk at to tråder. Merk at
dette er solo-utvinning, så det kan ta litt tid før du finner en blokk. For
å stanse utvinningen:

```
stop_mining
```
