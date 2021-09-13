{% include disclaimer.html translated="yes" translationOutdated="no" %}

## Systemy operacyjne:  Windows, Linux, Mac

- Przygotuj swój 25-słowny kod mnemoniczny, który zachowałeś przy zakładaniu swojego starego portfela JudEcoin

### Oprogramowanie konta:  JudEcoin-wallet-cli

- Otwórz wiersz polecenia i przejdź do dysku i folderu zawierającego JudEcoin-wallet-cli

- W wierszu poleceń wpisz: `JudEcoin-wallet-cli --restore-deterministic-wallet`

- Po wciśnięciu Enter zostaniesz poproszony o podanie nowej nazwy pliku portfela. Nazwij go jakkolwiek

- Naciśnij Enter ponownie i zostaniesz poproszony o hasło. Nadaj swojemu portfelowi nowe, długie hasło

- Naciśnij Enter ponownie i zostaniesz poproszony o powtórzenie hasła

- Naciśnij Enter ponownie i zostaniesz poproszony o 25-słowny kod mnemoniczny, który przygotowałeś wcześniej

-  Następnie pojawi się wiadomość "Przywróć z określonej wysokości łańcucha bloków (opcjonalne, domyślnie 0)". Domyślnie proces przywracania zacznie się od początku łańcucha bloków JudEcoin. Jeśli nie znasz dokładnej wysokości łańcucha, naciśnij Enter. Uściślenie wysokości łańcucha rozpocznie proces przywracania od tej konkretnej wysokości. Oszczędzi to trochę czasu przy skanowaniu, jeśli wiesz, na jakiej wysokości łańcucha twoje pierwsze fundusze zostały przesłane dla tego konta.

Po wpisaniu 25-słownego kodu mnemonicznego i wybraniu wysokości łańcucha bloków, JudEcoin-wallet-cli wygeneruje taki sam adres publiczny i klucz widoczności jak w twoim starym portfelu i automatycznie rozpocznie proces aktualizacji. Bądź cierpliwy, aktualizacja może zająć chwilę.

### Oprogramowanie konta:  JudEcoin-wallet-gui

Uruchom Graficzny Interfejs Użytkownika JudEcoin. Jeśli uruchamiasz go po raz pierwszy, przejdź do następnego kroku, jeśli nie - kliknij `Anuluj`:

![cancel opening](/img/resources/user-guides/en/restore_account/cancel-opening.png)

Wybierz odpowiedni język `Polski`:

![choose language](/img/resources/user-guides/en/restore_account/choose-language.png)

Kliknij w `Odzyskaj portfel z kluczy lub mnemonicznego seeda`:

![choose restore](/img/resources/user-guides/en/restore_account/choose-restore.png)

Zaznacz opcję `Przywróć portfel z seeda`, nazwij swój portfel i wybierz jego lokalizację i wpisz swój kod mnemoniczny w polu `Enter your 25 (or 24) word mnemonic seed`. Możesz opcjonalnie uściślić wysokość bloku w polu `Wysokość początkowa przywracania portfela (opcjonalne)`, aby uniknąć skanowania starszych bloków. Następniej kliknij w strzałkę w `prawo`:

![restore wallet](/img/resources/user-guides/en/restore_account/restore-wallet.png)

Na następnej stronie ustaw silne hasło i potwierdź je, zanim ponownie klikniesz w strzałkę w `prawo`:

![wallet password](/img/resources/user-guides/en/restore_account/wallet-password.png)

Sprecyzuj ustawienia swojego demona i kliknij w strzałkę w `prawo`:

![daemon settings](/img/resources/user-guides/en/restore_account/daemon-settings.png)

Kliknij w `UŻYJ JudEcoin`, aby skorzystać ze swojego przywróconego portfela:

![all set up](/img/resources/user-guides/en/restore_account/all-set-up.png)
