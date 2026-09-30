# lecture-assistant
# Paskaitų asistentas

Generatyvinio DI sistema, kuri iš paskaitos vaizdo/garso įrašo sukuria transkripciją (Whisper), santrauką, pagrindines sąvokas ir savitikros klausimus (Gemini API).

## Use case diagrama
Rodo pagrindinius naudotojo veiksmus ir sistemos sąveiką su Whisper bei Gemini API.

```mermaid
flowchart LR
    Studentas["Studentas"]
    Destytojas["Dėstytojas"]

    subgraph Sistema["Paskaitų asistentas"]
        UC1["Įkelti paskaitos vaizdo/garso įrašą"]
        UC2["Transkribuoti paskaitą"]
        UC3["Generuoti santrauką"]
        UC4["Išskirti pagrindines sąvokas"]
        UC5["Generuoti savitikros klausimus"]
        UC6["Peržiūrėti transkripciją"]
        UC7["Peržiūrėti santrauką"]
        UC8["Peržiūrėti pagrindines sąvokas"]
        UC9["Peržiūrėti savitikros klausimus"]
    end

    Whisper["Whisper API"]
    Gemini["Gemini API"]

    Studentas --> UC1
    Studentas --> UC6
    Studentas --> UC7
    Studentas --> UC8
    Studentas --> UC9

    Destytojas --> UC1
    Destytojas --> UC6
    Destytojas --> UC7
    Destytojas --> UC8
    Destytojas --> UC9

    UC1 --> UC2
    UC2 --> Whisper

    UC2 --> UC3
    UC2 --> UC4
    UC2 --> UC5

    UC3 --> Gemini
    UC4 --> Gemini
    UC5 --> Gemini
```

## Komponentų diagrama
Rodo pagrindinius sistemos komponentus ir jų sąveiką apdorojant paskaitos įrašą.

```mermaid
flowchart LR
    UI["Naudotojo sąsaja"]
    Backend["Paskaitų asistento backend"]
    Files["Failų valdymas"]
    Transcription["Transkripcijos modulis"]
    Whisper["Whisper API"]
    AI["DI analizės modulis"]
    Gemini["Gemini API"]
    DB[("Duomenų bazė")]

    UI -->|HTTP/HTTPS| Backend
    Backend -->|Įrašų saugojimas| Files
    Backend -->|Garso/vaizdo apdorojimas| Transcription
    Transcription -->|Audio| Whisper
    Whisper -->|Transkripcija| Transcription

    Backend -->|Transkripcijos tekstas| AI
    AI -->|Analizės užklausa| Gemini
    Gemini -->|DI rezultatai| AI

    Backend -->|Išsaugoti duomenis| DB
    DB -->|Nuskaityti duomenis| Backend

    Backend -->|Rezultatai| UI
```

## Sekų diagrama
Rodo paskaitos įrašo apdorojimo seką nuo įkėlimo iki rezultatų pateikimo.

```mermaid
sequenceDiagram
    actor Studentas
    participant UI as Naudotojo sąsaja
    participant Backend as Backend
    participant Whisper as Whisper API
    participant Gemini as Gemini API
    participant DB as Duomenų bazė

    Studentas->>UI: Įkelia paskaitos įrašą
    UI->>Backend: Siunčia įrašą
    Backend->>DB: Išsaugo įrašą

    Backend->>Whisper: Siunčia garso takelį
    Whisper-->>Backend: Grąžina transkripciją

    Backend->>DB: Išsaugo transkripciją

    Backend->>Gemini: Siunčia transkripciją
    Gemini-->>Backend: Grąžina santrauką
    Gemini-->>Backend: Grąžina pagrindines sąvokas
    Gemini-->>Backend: Grąžina savitikros klausimus

    Backend->>DB: Išsaugo DI rezultatus
    Backend-->>UI: Grąžina rezultatus
    UI-->>Studentas: Parodo transkripciją, santrauką, sąvokas ir klausimus
```

## Projekto struktūra
- `data/`: (X, y) pavyzdžiai
- `prompts/`: testinis promptas
- `diagrams/`: PlantUML ir Mermaid kodas
- `chatgpt/`: ChatGPT pokalbis
- `lecture_assistant.ipynb`: Colab prototipas

## ChatGPT pokalbis
[Nuoroda į pokalbį](ČIA_ĮKLIJUOK_SHARE_NUORODĄ)
