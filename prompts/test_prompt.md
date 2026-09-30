# Testinis promptas

Įklijuok šį promptą GPT agentui. Atsakyme turi būti JSON su santrauka, sąvokomis ir klausimais.

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

## Tikėtinas atsakymas
Atitinka `data/lecture2_output.json`.
