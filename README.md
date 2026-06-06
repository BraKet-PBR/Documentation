# BraKet
*Autorzy: Mikołaj Gawor, Michał Kubalewski, Szymon Pawlak, Mateusz Damian Cioch, Joanna Kościółek*

To repozytorium zawiera dokumentację projektu Braket. Plik który właśnie czytasz opisuje architekturę systemu i jego komponenty. Zawarta jest także skrócona instrukcja uruchomienia, po więcej szczegółów zapraszamy do odpowiednich repozytoriów, które są wskazane w następnej sekcji.

# Repozytoria
- Link do całej organizacji Github - https://github.com/BraKet-PBR
- Startowe repozytorium z dokumentacją - https://github.com/BraKet-PBR/Documentation
- Frontend, aplikacja android/web - https://github.com/BraKet-PBR/mobile-app-braket
- Backend, serwer API połączony z symulatorem QKD - https://github.com/BraKet-PBR/braket-api

# Osoby kontaktowe
- Aplikacja mobilna / web - Mikołaj Gawor ( mikgaw@st.amu.edu.pl )
- Backend - Michał Kubalewski ( mickub18@st.amu.edu.pl )
- Symulator QKD - Szymon Pawlak ( szypaw4@st.amu.edu.pl )

# Architektura systemu
## Kanał kwantowy
Kanał kwantowy jest fizycznym połączeniem światłowodowym łączącym palcówki UAM i PCSS. Na każdym z końców tego światłowodu znajduje się urządzenie do kwantowej dystrybucji klucza (zwane dalej QKD -> Quantum Key Distribution). Urządzenia wykorzystują właściwości cząstek kwantowych aby w bezpieczny sposób ustalić między sobą klucz do szyfrowania symetrycznego. Ustalanie klucza odbywa się za pośrednictwem protokołu BB84.

>Ze względu na czynniki zewnętrzne, na które nie mieliśmy wpływu uzyskanie dostepu do prawdziwego kanału kwantowego oraz urządzeń QKD nie powiodło się. Sytuacja ta była jednym z ryzyk zidentyfikowanym na etapie tworzenia dokumentu projektowego. Zostało wdrożone działanie mitygacyjne, polegające na stworzeniu symulatora QKD. Symulator jest zintegrowany z API. 

Osobne repozytorium skupiające się na symulacji kwantowej wymiany klucza i eksperymentach z nią związanych: https://github.com/BraKet-PBR/QKD

## Serwer + baza danych
Api wraz z instrukcją uruchomienia oraz dokumentacją znajduje się w repozytorium: https://github.com/BraKet-PBR/braket-api

## Aplikacja mobilna
Komponent ten wykorzystywany jest przez użytkowników końcowych do przesyłania szyfrowanych wiadomości.
Aplikacja mobilna wraz z instrukcją uruchomienia oraz dokumentacją znajduje się w repozytorium:\
https://github.com/BraKet-PBR/mobile-app-braket

# Cel projektu
Celem projektu było zaprojektowanie prostej w obsłudze warstwy użytkownika, umożliwiającej wysyłanie szyfrowanych wiadomosci korzystając z klucza szyfrowania uzyskanego z urządzeń QKD. Wartość projektu jest ściśle naukowa - jego zastosowanie z biznesie jest ograniczone. 

# Szybkie uruchomienie

## Wymagania
- Docker, Docker Compose
- Flutter SDK
- Przegladarka, np. Google Chrome
- Git
- [Opcjonalne] Telefon/emulator z systemem android

Ponadto upewnij się, że masz wolne porty ```6767``` i ```8080```, a przy pierwszym build'dzie ```docker compose build``` masz dostęp do sieci.

## Instalacja i konfiguracja
1. Sklonuj oba repozytoria komendami:
```bash
git clone https://github.com/BraKet-PBR/braket-api.git
git clone https://github.com/BraKet-PBR/mobile-app-braket.git
```
Po pobraniu kodu struktura twojego folderu nadrzędnego powinna wyglądać podobnie do:
```text
braket/
├── <repozytorium api>
└── <repozytorium mobile>
```
2. Przejdź w terminalu do repozytorium z aplikacją mobilną i potwierdź poprawność instalacji Fluttera:
```bash
flutter doctor
```
3. W tej samej lokalizacji zainstaluj zależności Flutter:
```bash
flutter pub get
```
4. Przejdź w oddzielnym terminalu do repozytorium api i za pomocą preferowanej przez siebie metody upewnij się, że posiadasz instalację docker compose, można to zrobić na przykład tak:
```bash
docker compose version
```
## Uruchomienie demonstracji
> Przed uruchomieniem api upewnij się, że twój docker engine działa.
1. Przejdź w terminalu do repozytorium api. Tam zbuduj i uruchom obraz poleceniami:
```bash
docker compose build
docker compose up
```
2. Przejdź w innym terminalu do repozytorium aplikacji mobilnej. Uruchom Flutter web server:
```bash
flutter run -d web-server --web-hostname 127.0.0.1 --web-port 8080
```
3. Otwórz pierwsze okno przeglądarki i przejdź pod adres ```http://127.0.0.1:8080```.
4. Otwórz drugie okno przeglądarki, tym razem w trybie **incognito** i przejdź pod adres z punktu **3**.
5. W obu instancjach frontendu w polu "API Url" wpisz ```http://127.0.0.1:6767```, i zaloguj się na udostępnione konta użytkowników.

## Oczekiwany wynik
Projekt działa poprawnie, jeśli dwie instancje aplikacji mobilnej (podpięte do jednego API) są w stanie nawiązać wspólną sesje oraz przesłać między sobą wiadomość tekstową.

# Testy
Dokładne testy opisane są w plikach README repozytoriów, tj:
- API - https://github.com/BraKet-PBR/braket-api/blob/main/README.md - sekcja "Reprodukcja i weryfikacja działania"
- Aplikacja - https://github.com/BraKet-PBR/mobile-app-braket/blob/main/README.md - sekcja "Test działania aplikacji - prosty  scenariusz testowy"

# Ograniczenia
- Projekt nie zapewnia zaawansowanego interfejsu użytkownika, a proces nawiązywania sesji i wysyłania wiadomości może zdawać się czasochłonny. Głównym celem projektu nie było zapewnienie najlepszego UX, a stworzenie POC warstwy użytkownika do wykorzystania kwantowej dystrybucji klucza. 
- Niezależną od nas przeszkodą jest brak fizycznego urządzenia QKD. Ze względu na koszt, czas montażu i dostępność zapewnienie go na własną rękę było dla nas niemożliwe
