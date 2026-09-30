# Testinis promptas

Įklijuok šį promptą GPT agentui. Atsakyme turi būti JSON su santrauka, sąvokomis ir klausimais.

## Promptas

```
Tu esi paskaitų asistentas. Žemiau pateikta paskaitos transkripcija. Sugeneruok:
1. trumpą santrauką (2 sakiniai),
2. 4-5 pagrindines sąvokas,
3. 4 savitikros klausimus.

Atsakyk TIK JSON formatu, lietuvių kalba:
{
  "santrauka": "...",
  "pagrindines_savokos": ["...", "..."],
  "savitikros_klausimai": ["...", "..."]
}

Transkripcija:
Reliacinė duomenų bazė saugo duomenis lentelėse, sudarytose iš eilučių ir stulpelių. Kiekviena eilutė yra atskiras įrašas. Pirminis raktas unikaliai identifikuoja eilutę lentelėje, o išorinis raktas sieja vieną lentelę su kita. Duomenims gauti naudojama SQL kalba, o komanda SELECT leidžia pasirinkti norimus stulpelius. Komanda JOIN sujungia kelias lenteles pagal bendrą raktą. Normalizavimas yra lentelių projektavimo procesas, kuriuo mažinamas duomenų dubliavimas ir išvengiama klaidų atnaujinant informaciją. Transakcijos užtikrina, kad kelių operacijų seka būtų įvykdyta visa arba visai neįvykdyta.
```

## Gautas atsakymas (Gemini)

```json
{
  "santrauka": "Reliacinės duomenų bazės saugo duomenis lentelėse ir naudoja SQL kalbą informacijai pasiekti bei lentelėms sujungti. Jose taip pat taikomas normalizavimas ir transakcijos duomenų vientisumui bei saugumui užtikrinti.",
  "pagrindines_savokos": [
    "Pirminis raktas",
    "Išorinis raktas",
    "SQL kalba",
    "Normalizavimas",
    "Transakcijos"
  ],
  "savitikros_klausimai": [
    "Kam yra naudojamas pirminis raktas reliacinėje duomenų bazėje?",
    "Kokia komanda leidžia sujungti kelias lenteles pagal bendrą raktą?",
    "Ką padeda pasiekti duomenų bazės normalizavimas?",
    "Kokią funkciją atlieka transakcijos?"
  ]
}
```

## Susiję failai
- Įvestis (X): `data/lecture2_input.txt`
- Išvestis (y): `data/lecture2_output.json`

## Pokalbio nuoroda
[Promptas paleistas GPT agentui](https://chatgpt.com/share/6abd695f-afa8-83ed-8629-2f338840403a)
