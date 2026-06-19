Automatyzacja Procesu Onboardingu i Dystrybucji Danych (HR Cloud Flow)

Rozwiązanie klasy Business Process Automation (BPA) zrealizowane w ekosystemie Microsoft Power Platform. Projekt automatyzuje powtarzalny proces rejestracji nowych pracowników, kategoryzacji sprzętowej na podstawie działu oraz dystrybucji zadań do odpowiednich jednostek wsparcia (IT/BHP), eliminując pracę ręczną i ryzyko błędów ludzkich (human error).

📋 Opis Problemu Biznesowego (Business Case)

W tradycyjnym modelu dział HR po zatrudnieniu nowego pracownika musiał ręcznie:

Odczytać dane z formularza zgłoszeniowego.

Ocenić, jakiego sprzętu i licencji potrzebuje pracownik (np. specjalistycznych licencji deweloperskich dla inżynierów danych).

Wysłać ręczne maile do działu IT oraz BHP.

Przepisać dane do głównego rejestru zatrudnienia w arkuszu Excel.

Wąskie gardła (Bottlenecks): Opóźnienia w przygotowaniu stanowisk pracy, błędy w przepisywaniu danych, brak spójności w archiwizacji dokumentacji oraz marnowanie czasu wykwalifikowanych pracowników HR na zadania administracyjne.

🛠️ Wykorzystane Technologie

Power Automate Cloud Flows (orkiestracja procesu, wyzwalacze zdarzeniowe, logika warunkowa).

OneDrive for Business / SharePoint (repozytorium dokumentów i bezpieczna strefa wymiany danych).

Excel Online (Business API) (dynamiczny odczyt tabelaryczny i aktualizacja baz danych strukturalnych).

Office 365 Outlook (komunikacja wewnętrzna i powiadomienia e-mail).

⚙️ Architektura i Przepływ Procesu (System Architecture)

[Nowy plik Excel (.xlsx) w folderze 'Nowe_Wnioski'] 
                      │
                      ▼
        [Wyzwalacz: OneDrive Trigger]
                      │
                      ▼
       [Warunek: Filtrowanie nazwy pliku] (Zabezpieczenie przed procesowaniem niechcianych plików)
                      │
         ┌────────────┴────────────┐
         ▼ (Prawda)                ▼ (Fałsz)
[Odczyt danych z Excela]     [Zakończenie pracy bota]
(Dynamiczne ID + Tabela_Nowy)
                      │
                      ▼
           [Warunek: Analiza Działu]
         ┌────────────┴────────────┐
         ▼ (IT / Analiza Danych)   ▼ (Inne Działy)
[Mail do IT: Specjalistyczny]  [Mail do IT: Standardowy]
(Licencje Python/SQL/RPA)    (Podstawowy pakiet biurowy)
         └────────────┬────────────┘
                      │
                      ▼
    [Aktualizacja Bazy Głównej (Excel)] 
 (Dopisanie wiersza ze statusem "W toku")
                      │
                      ▼
[Wysyłka spersonalizowanego regulaminu PDF do pracownika]


🚀 Kluczowe Rozwiązania Techniczne i Funkcje (Hard Skills)

1. Dynamiczne Przetwarzanie Plików (Dynamic File Handling)

Zamiast twardego kodowania ścieżek dostępu, przepływ wykorzystuje metadane wyzwalacza chmurowego (File Identifier). Bot jest w stanie otworzyć i sprocesować dowolny plik spełniający kryteria nazewnictwa, pobierając jego unikalne ID w czasie rzeczywistym.

2. Bezpieczna Integracja z API Excela (Table-Level Operations)

Odczyt i zapis danych realizowany jest wyłącznie na poziomie ustrukturyzowanych obiektów tabeli Excel (Table Object), co gwarantuje spójność typów danych i odporność na uszkodzenia struktury arkusza.

3. Zabezpieczenie Procesu (Input Validation & Filtering)

Wprowadzono filtrację na poziomie bramki wejściowej (warunek początkowy sprawdzający maskę nazwy pliku: starts with 'Nowy_Pracownik_'). Zapobiega to przypadkowemu uruchomieniu bota dla plików o innej strukturze.

🧠 Wyzwania Techniczne i Rozwiązane Problemy (Troubleshooting & Debugging)

Podczas wdrożenia i testów rozwiązano kluczowe problemy techniczne, co pozwoliło zoptymalizować działanie bota pod kątem niezawodności w środowisku produkcyjnym:

Błąd 404: "Nie znaleziono tabeli o nazwie Tabela_Nowy"

Przyczyna: Power Automate odczytywał strukturę pliku jako surowy arkusz roboczy, a nie sformatowany obiekt tabeli bazodanowej w Excelu.

Rozwiązanie: Zaimplementowano ustrukturyzowane formatowanie tabeli (Ctrl + T) oraz nadano unikalny identyfikator obiektu bezpośrednio we właściwościach projektu tabeli w Excel Online.

Konflikty dostępu do plików (File Locking & Concurrency)

Przyczyna: Występowanie błędu blokady pliku przez OneDrive podczas jednoczesnej próby edycji pliku przez użytkownika i bota.

Rozwiązanie: Przełączono formaty wejściowe z archiwalnych .xls na nowoczesne .xlsx w celu lepszej obsługi metadanych oraz zaimplementowano zasadę automatycznego zamykania aktywnych sesji przed uruchomieniem procesu automatyzacji.

📈 Wartość Biznesowa i ROI (Return on Investment)

Oszczędność czasu (Time Saved): Skrócenie czasu procesowania jednego wniosku onboardingowego z 15 minut (praca ręczna) do mniej niż 10 sekund (czas wykonania bota).

Redukcja błędów (Error Reduction): 100% poprawności przy przepisywaniu danych do bazy głównej – eliminacja ryzyka literówek w nazwiskach czy adresach e-mail.

Szybkość operacyjna (Operational Speed): Natychmiastowe (w czasie rzeczywistym) powiadomienie działu IT o potrzebie przygotowania sprzętu, co skraca czas wdrożenia nowego pracownika i zapobiega jego przestojom w pierwszym dniu pracy.
