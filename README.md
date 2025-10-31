# Tytuł projektu

Krótki opis problemu i celu rozwiązania (1–3 zdania). Co otrzymuje użytkownik końcowy (API + UI).

---

### SPIS TREŚCI
(Spis sekcji z linkami do nagłówków – opcjonalnie)

---

### CEL I ZAKRES
Co projekt ma osiągnąć, dla kogo jest przeznaczony, jakie są ograniczenia/wyzwania.

---

### ARCHITEKTURA (HIGH-LEVEL)
Krótki opis lub diagram: źródło danych → potok (Kedro) → trening → model → API (FastAPI) → UI (Streamlit) → (opcjonalnie) baza danych. Informacja o W&B i GCP Cloud Run.

---

### DANE
Źródło danych, licencja, rozmiar, data pobrania, wstępny opis cech i targetu. Informacja o PII (brak/anonimizacja).

---

### POTOK (KEDRO)
Jak uruchomić `kedro run`. Co robią główne nody i pipeline’y. Gdzie jest `conf/base/catalog.yml` i `conf/base/parameters.yml`. Gdzie zapisywane są artefakty (processed, model, metrics).

---

### EKSPERYMENTY I WYNIKI (W&B)
Link do projektu W&B. Główna metryka, podsumowanie eksperymentów, tabelka najlepszych runów. Wskazanie modelu „Production” i aliasu artefaktu.

---

### MODEL I MODEL CARD
Typ modelu, najważniejsze metryki na zbiorze testowym, znane ograniczenia. Link do `docs/model_card.md`. Sekcja o wersjonowaniu (artifact, git SHA, image tag).

---

### ŚRODOWISKO I INSTALACJA
Wymagania (Python, system). Jak utworzyć środowisko (np. `conda env create -f environment.yml`) i dodać kernel Jupyter. Lista kluczowych zależności.

---

### URUCHOMIENIE LOKALNE (BEZ DOCKERA)
Komendy startowe dla API i UI:
- API (FastAPI + Uvicorn): jak uruchomić, port, przykładowe `curl` do `/healthz` i `/predict`.
- UI (Streamlit): jak uruchomić i jak wskazać `API_URL`.

---

### DOCKER I DOCKER-COMPOSE
Jak zbudować obrazy (`docker build …`) i jak uruchomić cały stack (`docker compose up --build`). Wymienione usługi i porty (API 8000, UI 8501). Skąd UI bierze `API_URL`.

---

### WDROŻENIE W CHMURZE (GCP CLOUD RUN)
Kroki wdrożenia: push obrazów do Artifact Registry, `gcloud run deploy` dla API i UI, ustawienie `API_URL`. Linki do działających usług. Parametry kosztowe (min-instances=0, CPU/RAM, timeout).

---

### KONFIGURACJA: ENV I SEKRETY
Jakie zmienne środowiskowe obsługuje projekt (`API_URL`, `MODEL_PATH`, `DATABASE_URL`, `WANDB_API_KEY`, itp.). Zasady: sekrety w **Secret Manager**, lokalnie `.env` (nie commitować).

---

### API (FASTAPI)
Lista endpointów:
- `GET /healthz` – status usługi.
- `POST /predict` – schemat wejścia/wyjścia (JSON), przykładowy payload.
Wzmianka o CORS (kiedy potrzebny i jakie domeny są dozwolone).

---

### UI (STREAMLIT)
Jak korzystać z interfejsu: jakie pola odpowiadają cechom modelu, skąd pobiera adres API (`API_URL`). Jak uruchomić lokalnie i w chmurze.

---

### BAZA DANYCH (OPCJONALNIE)
Jaki silnik lokalnie (SQLite/Postgres). Minimalny schemat (np. tabela `predictions`: timestamp, payload, prediction, model_version). Jak podejrzeć rekordy.

---

### MONITORING I DIAGNOSTYKA
Jak sprawdzić "health check" (`/healthz`), jak wykonać testową predykcję w chmurze. Gdzie są logi (Cloud Logging) i jak je filtrować. Najczęstsze błędy i szybkie wskazówki naprawy.

---

### TESTY I JAKOŚĆ
Jak uruchomić testy (`pytest -q`) i precommit (`pre-commit run -a`). Co testujemy (nody potoku, ewaluacja, podstawowy test API).

---

### STRUKTURA REPOZYTORIUM
Skrótowe drzewko katalogów z opisem ról:
```
src/ # kod (pakiet aplikacji: potok, API, UI)
notebooks/ # analizy/EDA (nieprodukcyjne) - o ile nie zostały wyrzucone/zarchiwizowane
conf/ # Kedro: catalog.yml, parameters.yml, lokalne nadpisania
data/ # próbki/artefakty (bez pełnego zbioru danych i sekretów)
tests/ # testy jednostkowe/integracyjne
docs/ # dokumentacja (np. model_card.md, diagramy)
```

### ZAŁĄCZNIKI / LINKI
Linki: W&B project, artefakt modelu, prezentacja, diagram architektury, dokumenty z ASI.


