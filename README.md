# HR Onboarding & Data Distribution Cloud Pipeline 🚀

[![Power Automate](https://img.shields.io/badge/Power%20Automate-0078D4?style=for-the-badge&logo=microsoftpowerautomate&logoColor=white)](https://powerautomate.microsoft.com/)
[![SharePoint](https://img.shields.io/badge/SharePoint-036C70?style=for-the-badge&logo=microsoftsharepoint&logoColor=white)](https://www.microsoft.com/sharepoint)
[![Microsoft Teams](https://img.shields.io/badge/Microsoft%20Teams-6264A7?style=for-the-badge&logo=microsoftteams&logoColor=white)](https://www.microsoft.com/teams)
[![Outlook](https://img.shields.io/badge/Microsoft%20Outlook-0078D4?style=for-the-badge&logo=microsoftoutlook&logoColor=white)](https://outlook.live.com/)

Automatyczny system bezobsługowego wdrażania nowych pracowników (*HR Onboarding*) oraz wielokanałowej dystrybucji danych personalnych, zbudowany w oparciu o chmurowe przepływy **Power Automate Cloud Flows**.

---

## 📌 Problem Biznesowy & Rozwiązanie

Ręczne wprowadzanie danych nowych pracowników, rozsyłanie wniosków do działu IT i sprzętowego oraz wysyłanie pakietów powitalnych generuje znaczne koszty czasowe i ryzyko przeoczenia kluczowych kroków w procesie onboardingowym. 

**HR Onboarding Cloud Pipeline** automatyzuje cały proces: od momentu rejestracji nowego zgłoszenia w systemie HR / na liście SharePoint, przez akceptację przełożonego i automatyczne przygotowanie kont/sprzętu, aż po dystrybucję powiadomień przez Microsoft Teams i Outlook.

---

## 🏗️ Architektura Procesu

```mermaid
graph TD
    A[Formularz HR / Lista SharePoint] -->|Trigger: New Item| B[Power Automate Cloud Flow]
    B -->|Walidacja & Formatowanie| C{Zgoda Przełożonego?}
    C -->|Tak| D[Weryfikacja IT / Przygotowanie Sprzętu]
    C -->|Nie| E[Anulowanie & Odpowiedź do HR]
    D -->|Karta Adaptive Card| F[Powiadomienie MS Teams]
    D -->|Personalizowany e-mail| G[Wiadomość Powitalna Outlook]
    D -->|Update statusu| H[(Centralny Rejestr HR / Dataverse)]
