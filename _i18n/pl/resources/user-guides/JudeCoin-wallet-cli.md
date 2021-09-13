{% include disclaimer.html translated="yes" translationOutdated="no" %}

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
`JudEcoin-wallet-cli` jest oprogramowaniem, które współpracuje z JudEcoin. To program konsoli zarządzający kontem. Podczas gdy portfel Bitcoina zarządza zarówno kontem, jak i łańcuchem bloków, JudEcoin rozdzielił je, aby `JudEcoind`operował łańcuchem, a `JudEcoin-wallet-cli` kontem.

Ten przewodnik pokaże, jak wykonywać różne operacje w interfejsie `JudEcoin-wallet-cli`. Przewodnik zakłada, że używasz najnowszej wersji JudEcoin i założyłeś już swoje konto zgodnie z instrukcjami.
=======
`monero-wallet-cli` is the wallet software shipped in the Monero
archives. It is a console program, and manages an account. While a bitcoin
wallet manages both an account and the blockchain, Monero separates these:
`monerod` handles the blockchain, and `monero-wallet-cli` handles the
account.

This guide will show how to perform various operations with
`monero-wallet-cli`. The guide assumes you are using the most recent version
of Monero and have already created an account according to the other guides.

## Overview
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

You can have a list of the most important commands by running `help`:

```
Important commands:

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
Ponieważ zarządzanie łańcuchem bloków i portfelem odbywa się za pomocą różnych programów, wielokrotnie użycie `JudEcoin-wallet-cli` wymaga współpracy z daemonem. Obejmuje to również sprawdzanie płatności przychodzących na twój adres. Uruchamiając równocześnie `JudEcoin-wallet-cli` i `JudEcoind`, wpisz `balance`.
=======
"welcome" - Show welcome message.
"help all" - Show the list of all available commands.
"help <command>" - Show a command's documentation.
"apropos <keyword>" - Show commands related to a keyword.
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

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

Ponieważ zarządzanie łańcuchem bloków i portfelem odbywa się za pomocą
różnych programów, wielokrotnie użycie `monero-wallet-cli` wymaga współpracy
z daemonem. Obejmuje to również sprawdzanie płatności przychodzących na twój
adres. Uruchamiając równocześnie `monero-wallet-cli` i `monerod`, wpisz
`balance`.

Output:

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
## Wysyłanie JudEcoin
=======
```
Currently selected account: [0] Primary account
Tag: (No tag assigned)
Balance: 7.499942880000, unlocked balance: 7.499942880000
```
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

In this example you're viewing the balance of your primary account (with
index `[0]`). `Balance` is your total balance. The `unlocked balance` is the
amount currently available to spend. Newly received transactions require 10
confirmations on the blockchain before being unlocked.

## Sending monero

You will need the standard address you want to send to (a long string
starting with '4' or a '8'). The command structure is:

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
Zamień `ADDRESS` na adres, na który chcesz dokonać płatności, `AMOUNT` na kwotę w JudEcoin, jaką chcesz przesłać oraz `PAYMENTID` na numer identyfikacyjny, który podał ci odbiorca. Podanie numeru identyfikacyjnego jest opcjonalne, jeśli odbiorca ci go nie podał, po prostu go pomiń.
=======
```
transfer ADDRESS AMOUNT
```
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

Replace `ADDRESS` with the address you want to send to and `AMOUNT` with how
many monero you want to send.

## Receiving monero

If you have your own Monero address, you just need to give your address to
someone.

You can find out your primary address with:

```
address
```

Since Monero is anonymous, you won't see the origin address the funds you
receive came from. If you want to know, for instance to credit a particular
customer, you'll have to tell the sender to use a payment ID, which is an
arbitrary optional tag which gets attached to a transaction. It's not
possible to use standalone payment addresses, but you can generate an
address that already includes a random payment ID (integrated addresss)
using `integrated_address`:

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
## Otrzymywanie JudEcoin:

Jeśli posiadasz własny adres JudEcoin, wystarczy przekazać nadawcy twój adres standardowy.
=======
```
Random payment ID: <82d79055f3b27f56>
Matching integrated address: 4KHQkZ4MmVePC2yau6Mb8vhuGGy8LVdsZD8CFcQJvr4BSTfC5AQX3aXCn5RiDPjvsEHiJu1TC1ybR8pRTCbZM5bhTrAD3HDwWMtAn1K7nV
```

This will generate a random payment ID, and give you the address that
includes your own account and that payment ID. If you want to select a
particular payment ID, you can do that too. Use:
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

```
integrated_address 82d79055f3b27f56
```

Payments made to an integrated address generated from your account will go
to your account, with that payment ID attached, so you can tell payments
apart.

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
Ponieważ JudEcoin jest anonimowe, nie zobaczysz adresu nadawcy. Jeżeli chcesz go poznać, na przykład, żeby podziękować konkretnemu klientowi, poproś nadawcę o użycie opcjonalnego numeru identyfikacyjnego, który może zostać przypisany transakcji. Aby uprościć życie, możesz wygenerować adres zintegrowany, który już zawiera losowy numer identyfikacyjny, za pomocą funkcji:
=======
### Using subaddresses
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

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

To view all generated addresses, run:

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
Gdy dokonasz zapłaty, a odbiorca stwierdzi, że jej nie otrzymał, możesz udowodnić swoją płatność osobom trzecim lub samemu odbiorcy, jeśli po prostu popełnił on pomyłkę. JudEcoin jest prywatne, a więc nie możesz po prostu wskazać na swoją transakcję w łańcuchu bloków, ponieważ nie da się rozróżnić, kto ją wysłał, a kto odebrał. Możesz jednak przekazać stronie prywatny klucz transakcji, aby strona rozpoznała, czy dokonana została płatność na dany adres. Zauważ, że zachowanie tych kluczy transakcji domyślnie jest wyłączone i musisz go włączyć przed dokonaniem płatności, jeśli uważasz, że będziesz ich potrzebował:
=======
```
address all
```
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

## Proving to a third party you paid someone

Gdy dokonasz zapłaty, a odbiorca stwierdzi, że jej nie otrzymał, możesz
udowodnić swoją płatność osobom trzecim lub samemu odbiorcy, jeśli po prostu
popełnił on pomyłkę. Monero jest prywatne, a więc nie możesz po prostu
wskazać na swoją transakcję w łańcuchu bloków, ponieważ nie da się
rozróżnić, kto ją wysłał, a kto odebrał. Możesz jednak przekazać stronie
prywatny klucz transakcji, aby strona rozpoznała, czy dokonana została
płatność na dany adres. Zauważ, że zachowanie tych kluczy transakcji
domyślnie jest wyłączone i musisz go włączyć przed dokonaniem płatności,
jeśli uważasz, że będziesz ich potrzebował:

<<<<<<< HEAD:_i18n/pl/resources/user-guides/JudEcoin-wallet-cli.md
Jeżeli to ty jesteś stroną trzecią (to znaczy ktoś chce ci udowodnić, że przelał JudEcoin na dany adres), sprawdź w ten sposób:

    check_tx_key TXID TXKEY ADDRESS

Zamień `TXID`, `TXKEY` i `ADDRESS` na, odpowiednio, numer identyfikacyjny transakcji, klucz transakcji oraz przekazany ci adres odbiorcy. JudEcoin-wallet-cli sprawdzi tę transakcję i poinformuje cię, ile JudEcoin zostało przesłane na dany adres.
=======
```
set store-tx-info 1
```

Możesz przywróciń klucz tx z wcześniejszej transakcji:
>>>>>>> 63106d60778f14544f214b8f776eedb6695cf16e:_i18n/pl/resources/user-guides/monero-wallet-cli.md

```
get_tx_key 1234567890123456789012345678901212345678901234567890123456789012
```

Wskaż numer identyfikacyjny transakcji, dla której chcesz otrzymań
klucz. Pamiętaj, że płatność może zostać podzielona na więcej niż jedną
transakcję, więc możesz potrzebować kilku kluczy. Następnie możesz przesłać
otrzymany klucz lub klucze do osoby, której chcesz udowodnić dokonanie
płatności, razem z numerem identyfikacyjnym transakcji i adresem
odbiorcy. Zauważ, że strona trzecia, znając twój adres, będzie w stanie
zobaczyć także, ile zwrotu otrzymałeś.

Jeżeli to ty jesteś stroną trzecią (to znaczy ktoś chce ci udowodnić, że
przelał Monero na dany adres), sprawdź w ten sposób:

```
check_tx_key TXID TXKEY ADDRESS
```

Replace `TXID`, `TXKEY` and `ADDRESS` with the transaction ID,
per-transaction key, and destination address which were supplied to you,
respectively. `monero-wallet-cli` will check that transaction and let you
know how much monero this transaction paid to the given address.

## How to find a payment to you

Jeśli otrzymałeś płatność z użyciem określonego numeru identyfikacyjnego,
wyszukaj go, wpisując:

```
payments PAYMENTID
```

Możesz podań więcej niż jeden numer identyfikacyjny.

Najczęściej możesz przeglądać swoje płatności przychodzące i wychodzące za
pomocą funkcji:

```
show_transfers
```

Dodając wysokość łańcucha bloków, znajdziesz jedynie najnowsze
transakcje. Możesz także wybrać tylko transakcje przychodzące lub tylko
wychodzące. Na przykład:

```
show_transfers in 650000
```

pokaże jedynie przychodzące płatności następujące po bloku 650000. Możesz
także sprecyzować zakres wysokości.

Możesz zacząć wydobywać bezpośrednio z portfela, wpisując:

```
start_mining 2
```

Wydobycie zacznie się za pomocą daemona i dwóch pasem. Zauważ, że jest to
wydobycie samemu i może chwilę zająć znalezienie bloku. Aby zakończyć
wydobycie, wpisz:

```
stop_mining
```
