# Paskaitų asistentas: multimodalinis duomenų išgavimas iš video

Šiame projekte iš paskaitų video išgaunami keli duomenų tipai, kurie vėliau naudojami generatyvaus DI užduotims: kalbos atpažinimui (audio → tekstas) ir paveikslėlių aprašymui (kadras → tekstas).

## Užduotys ir duomenų poros

| Užduotis | Įvestis (X) | Išvestis (y) | Įrankis |
|---|---|---|---|
| Kalbos atpažinimas | Audio (`.mp3`) | Transkripcija (`.txt`) | Whisper (`medium`) |
| Paveikslėlio aprašymas | Vidurinis video kadras (`.jpg`) | Aprašymas (`.txt`) | Gemini API |

Poros sutampa pagal numerį, pavyzdžiui:
- `data/audio_data/1.mp3` → `data/text_data/1.txt`
- `data/frame_data/1.jpg` → `data/image_descriptions/1.txt`

## Procesas

```
Paskaitos video (.mp4, 1 min. fragmentas)
        │
        ├──► audio (.mp3) ──► Whisper ──► transkripcija (.txt)
        │
        └──► vidurinis kadras (.jpg) ──► Gemini ──► aprašymas (.txt)
```

1. **`01_data_preparation.ipynb`**: video fragmentų atsisiuntimas, audio išgavimas (`moviepy`), transkripcija (Whisper), vidurinio kadro išgavimas.
2. **`02_image_description.ipynb`**: kadrų aprašymų generavimas per Gemini API.

**Pastaba dėl Gemini modelių.** Dėl laikinų serverių perkrovų (503) antrame notebook'e kodas automatiškai kartoja užklausas ir, jei reikia, pereina prie atsarginių modelių, todėl skirtingi kadrai gali būti aprašyti skirtingais Gemini modeliais. Naudotas modelis matomas notebook'o išvestyje.

## Duomenų šaltinis

- **Kursas:** MIT OpenCourseWare, *6.0001 Introduction to Computer Science and Programming in Python* (Fall 2016)
- **Paskaitos:** Lecture 1, 2, 3, 5 ir 6 (naudota po 1 min. fragmentą, pradedant nuo 2:00 min.)
- **Autoriai:** Dr. Ana Bell, Prof. Eric Grimson, Prof. John Guttag
- **Kurso puslapis:** https://ocw.mit.edu/courses/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/
- **Licencija:** Creative Commons BY-NC-SA 4.0 (https://creativecommons.org/licenses/by-nc-sa/4.0/)

Šiame repozitorijuje esantys video fragmentai, audio failai, kadrai, transkripcijos ir aprašymai yra išvestinė medžiaga. Ji naudojama tik mokymosi tikslais, nekomerciškai ir platinama ta pačia licencija.

## Repozitorijos struktūra

```
nlp-video-multimodal-extraction/
├── README.md
├── 01_data_preparation.ipynb
├── 02_image_description.ipynb
└── data/
    ├── video_data/          # 5 video fragmentai (.mp4)
    ├── audio_data/          # X: garso failai (.mp3)
    ├── text_data/           # y: Whisper transkripcijos (.txt)
    ├── frame_data/          # X: vidurinių kadrų paveikslėliai (.jpg)
    └── image_descriptions/  # y: Gemini aprašymai (.txt)
```

## Kaip paleisti

1. Atidaryk notebook'ą per Google Colab.
2. Pirmam notebook'ui pasirink **Runtime → Change runtime type → T4 GPU** (greitesnė Whisper transkripcija).
3. Antram notebook'ui Colab **Secrets** (🔑) pridėk `GOOGLE_API_KEY` (Gemini API raktas iš [Google AI Studio](https://aistudio.google.com)) ir įjunk **Notebook access**.
4. Paleisk langelius iš eilės. Pirmo notebook'o rezultatai (`frame-data.zip`) įkeliami į antrą notebook'ą per `files.upload()`.

## Naudotos technologijos

- Python, Google Colab
- `moviepy`, `ffmpeg`: darbas su video ir audio
- OpenAI Whisper: kalbos atpažinimas
- Google Gemini API: paveikslėlių aprašymai
