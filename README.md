# BraKet
*Autorzy: Mikołaj Gawor, Michał Kubalewski, Szymon Pawlak, Mateusz Cioch, Joanna Kościółek*

To repozytorium zawiera dokumentację projektu Braket. Plik który właśnie czytasz opisuje architekturę systemu i jego komponenty. Szczegółowe instrukcje jak uruchomić projekt znajdują się w folderze `devops` tego repozytorium.

# Osoby kontaktowe
- Aplikacja mobilna / web -> Mikołaj Gawor ( mikgaw@st.amu.edu.pl )
- Backend -> Michał Kubalewski ( mickub18@st.amu.edu.pl )
- Symulator QKD -> Szymon Pawlak ( szypaw4@st.amu.edu.pl )

# Elementy systemu
## Kanał kwantowy
Kanał kwantowy jest fizycznym połączeniem światłowodowym łączącym palcówki UAM i PCSS. Na każdym z końców tego światłowodu znajduje się urządzenie do kwantowej dystrybucji klucza (zwane dalej QKD -> Quantum Key Distribution). Urządzenia wykorzystują właściwości cząstek kwantowych aby w bezpieczny sposób ustalić między sobą klucz do szyfrowania symetrycznego. Ustalanie klucza odbywa się za pośrednictwem protokołu BB84.

Ze względu na czynniki zewnętrzne, na które nie mieliśmy wpływu uzyskanie dostepu do prawdziwego kanału kwantowego oraz urządzeń QKD nie powiodło się. Sytuacja ta była jednym z ryzyk zidentyfikowanym na etapie tworzenia dokumentu projektowego. Zostało wdrożone działanie mitygacyjne, polegające na stworzeniu symulatora QKD. Symulator jest zintegrowany z API. Osobne repozytorium skupiające się na symulacji kwantowej wymiany klucza:\
https://github.com/BraKet-PBR/QKD

## Serwer + baza danych
Api wraz z instrukcją uruchomienia oraz dokumentacją znajduje się w repozytorium:
<TODO link do repo>

## Aplikacja mobilna
Komponent ten wykorzystywany jest przez użytkowników końcowych do przesyłania szyfrowanych wiadomości.
Aplikacja mobilna wraz z instrukcją uruchomienia oraz dokumentacją znajduje się w repozytorium:\
https://github.com/BraKet-PBR/mobile-app-braket


## Cel projektu
*Krótki opis problemu, zakresu projektu i najważniejszych rezultatów.*

Celem projektu było zaprojektowanie prostej w obsłudze warstwy użytkownika, umożliwiającej wysyłanie szyfrowanych wiadomosci korzystając z klucza szyfrowania uzyskanego z urządzeń QKD. Wartość projektu jest ściśle naukowa - jego zastosowanie z biznesie jest ograniczone. 


## Wymagania
Wymagania sprzętowe i programowe, np. system operacyjny, wersje języków, biblioteki, Docker, GPU, dostęp do usług zewnętrznych.

## Instalacja i konfiguracja
*Kroki potrzebne do przygotowania środowiska.*

## Uruchomienie demonstracji
*Polecenia uruchamiające projekt lub jego demonstracyjną wersję.*

## Oczekiwany wynik
*Informacja, po czym poznać, że projekt uruchomił się poprawnie.*

Projekt działa poprawnie, jeśli dwie instancje aplikacji mobilnej (podpięte do jednego API) są w stanie nawiązać wspólną sesje oraz przesłać między sobą wiadomość tekstową.

## Dane
*Informacja, jakie dane są potrzebne, skąd je pobrać, gdzie je umieścić i jakie są ograniczenia dostępu.*

## Reprodukcja lub weryfikacja wyników
*Instrukcja odtworzenia albo sprawdzenia najważniejszych wyników, artefaktów, metryk, raportów lub modeli.*

## Testy

## Dokumentacja
*Odnośniki do dokumentacji użytkownika, konserwacyjnej i architektury.*

## Ograniczenia
*Znane problemy, wymagania niestandardowe, elementy niedokończone lub zależne od usług zewnętrznych.*
Projekt nie zapewnia zaawansowanego interfejsu użytkownika, a proces nawiązywania sesji i wysyłania wiadomości może zdawać się czasochłonny. Głównym celem projektu nie było zapewnienie najlepszego UX, a stworzenie POC warstwy użytkownika do wykorzystania kwantowej dystrybucji klucza. 



