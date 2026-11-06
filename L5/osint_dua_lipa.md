# Fase 1 — Selezione del Target e Raccolta OSINT

**Data:** 6 novembre 2026
**Operatore:** Elia F.
**Target:** Dua Lipa (personaggio pubblico, artista)
**Ambito:** Raccolta OSINT del target

---

## 1. Obiettivo

Effettuare una rapida indagine OSINT su un target di dominio pubblico, identificando:
- attività e movimenti professionali pubblici (tour, collaborazioni),
- progetti e investimenti in corso,
- interlocutori pubblici con cui il target interagisce.

## 2. Fonti consultate

| # | Fonte | Tipo | Note |
|---|-------|------|------|
| 1 | Sito ufficiale dell'artista e canali social verificati (Instagram, X, YouTube) | Fonte primaria | Annunci ufficiali, date tour, collaborazioni |
| 2 | Discografie ufficiali (Spotify, Apple Music, pagine artist Warner Music) | Fonte primaria | Catalogo, date di uscita, certificazioni |
| 3 | Stampa generalista e di settore (riviste musicali, agenzie di stampa, Billboard) | Fonte secondaria | Carriera, premi, attività extra-musicale |
| 4 | Registri premi ufficiali (GRAMMY.com, BRITs) | Fonte secondaria | Riconoscimenti e anni |
| 5 | Siti istituzionali (UN Women, marchi partner) | Fonte secondaria | Ruoli di ambasciatrice, campagne |

### 2.1 Strumenti e tecniche

**Google Dorking** — libreria di query realmente impiegabili, organizzata per obiettivo:

Le 8 famiglie di query, raggruppate in un unico blocco per copia/ripetizione (i commenti `#` segnalano il gruppo e non fanno parte della query):

```
# a) Identità e profilo ufficiale
"Dua Lipa" site:warnermusic.com
"Dua Lipa" site:warnermusic.co.uk
"Dua Lipa" profile site:grammy.com
intitle:"Dua Lipa" bio

# b) Discografia e certificazioni
"Dua Lipa" "Future Nostalgia" tracklist
"Dua Lipa" "Radical Optimism" release
"Dua Lipa" "Levitating" "Billboard Hot 100"
"Dua Lipa" platinum certification site:bpi.co.uk OR site:riaa.com
"Dua Lipa" album chart position UK US

# c) Tour e attività dal vivo
"Dua Lipa" tour 2024 dates
"Dua Lipa" "Radical Optimism World Tour" sold out
"Dua Lipa" "Wembley" OR "Madison Square Garden" 2024
"Dua Lipa" headline set OR opener

# d) Premi e riconoscimenti
"Dua Lipa" Grammy winner year
"Dua Lipa" "Grammy" site:grammy.com
"Dua Lipa" Brit Award site:brits.co.uk
"Dua Lipa" "Video of the Year" VMA

# e) Collaborazioni musicali
"Dua Lipa" "Calvin Harris" "One Kiss"
"Dua Lipa" "Angèle" "Training Season"
"Dua Lipa" "Missy Elliott" collaboration
"Dua Lipa" featuring tracklist

# f) Ruoli istituzionali e brand
"Dua Lipa" site:unwomen.org
"Dua Lipa" "ambassador" "UN Women"
"Dua Lipa" "L'Oréal" campaign
"Dua Lipa" "Fenty Beauty" site:fentybeauty.com
"Dua Lipa" charity OR "charitable work" site:variety.com

# g) Documenti e comunicati
filetype:pdf "Dua Lipa" press kit
filetype:pdf "Dua Lipa" tour
filetype:doc "Dua Lipa"
filetype:xls "Dua Lipa" tour dates

# h) Esclusione del rumore (operatore negativo)
"Dua Lipa" -fanpage -forum -youtube
"Dua Lipa" -fanfic -lyrics -wiki
"Dua Lipa" news -twitter -instagram
```

**Operatori chiave impiegati e perché:**

| Operatore | Funzione | Esempio nel report |
|-----------|----------|--------------------|
| `""` (virgolette) | Ricerca esatta della frase | `"Future Nostalgia" tracklist` |
| `site:` | Limita a un dominio specifico | `site:unwomen.org` |
| `intitle:` | Termine nel titolo della pagina | `intitle:"Dua Lipa" bio` |
| `filetype:` | Cerca documenti specifici | `filetype:pdf "Dua Lipa"` |
| `OR` | Alternative tra termini | `site:bpi.co.uk OR site:riaa.com` |
| `-term` | Esclude un termine/dominio | `-fanpage -forum` |
| `related:` | Siti simili a uno già trovato | `related:grammy.com` |
| `cache:` | Anteprima cache di una pagina | `cache:warnermusic.com` |

**Workflow operativo suggerito:**
1. **Ancorare** — iniziare dalle fonti primarie con `site:` (etichetta, ente istituzionale): riduce il rumore e fissa i fatti di base.
2. **Triangolare** — per ogni fatto raccolto, cercare la stessa informazione su almeno un dominio diverso (es. ruolo ONU: `unwomen.org` + `variety.com`).
3. **Estendere** — usare `OR` e `filetype:` per trovare documenti, certificazioni e comunicati ufficiali.
4. **Pulire** — usare l'operatore negativo (`-`) per scartare fanpage, forum e contenuti non curati.
5. **Registrare** — ogni query che produce un dato utile va annotata insieme alla fonte, per garantire la riproducibilità dell'esercizio.

**Maltego** — utile per costruire un grafo di associazioni a livello **organizzativo** (non personale). Entità e collegamenti identificati:
```
[Dua Lipa] ──interpreta──▶ [Warner Music UK]
     │
     ├──collabora musicalmente──▶ [Calvin Harris] [Angèle] [Missy Elliott]
     │
     ├──ambasciatrice──▶ [UN Women]
     │
     └──campagne pubbliche──▶ [L'Oréal] [Fenty Beauty]
```
Ogni arco del grafo è supportato da almeno una fonte documentata: questo è il punto di forza del tool rispetto alla sola ricerca testuale.

## 3. Metodo

1. **Definizione scope** — target, perimetro (solo pubblico/professionale), criteri di esclusione espliciti.
2. **Raccolta** — interrogazioni con operatori di ricerca; ogni dato verificato su almeno due fonti indipendenti (es. ruolo ONU confermato sia da comunicato istituzionale sia da stampa).
3. **Correlazione** — costruzione di una timeline di carriera e di una mappa delle relazioni organizzative.
4. **Documentazione** — tabella fonti; ogni dato ha una fonte associata.
5. **Reperibilità** — le query utilizzate sono riportate in §2.1 per riprodurre l'esercizio.

## 4. Risultati

### 4.1 Profilo base (dati di dominio pubblico)
- Nata il **22 agosto 1995** a **Pristina (Kosovo)**; famiglia di origine albanese.
- Cresciuta a **Londra**, dove si trasferisce in giovane età.
- Padre musicista (bandleader/backing vocalist): influenza musicale dichiarata in interviste pubbliche.
- In attività dal 2015; firma con **Warner Music UK** nel 2015.

### 4.2 Timeline attività professionale

| Periodo | Evento |
|---------|--------|
| 2015 | Esordi su SoundCloud/YouTube; firma con Warner Music UK |
| 2016 | Primi singoli *New Love*, *Blow Your Mind (Mja Ikj)* (brano in albanese, omaggio alle origini kosovare) |
| 2017 | Album d'esordio ***Dua Lipa*** (2017); *Hotter than Hell* (feat. Nicki Minaj); ***New Rules*** — successo internazionale, #1 UK, oltre un miliardo di streaming |
| 2018 | *One Kiss* (con **Calvin Harris**) — #1 in decine di paesi; *Electricity*; nomination **Brit Award Best British Female** (2019, per *New Rules*) |
| 2019 | *Don't Start Now*; *Homesick* |
| 2020 | ***Future Nostalgia*** — #1 UK, #2 Billboard 200; 14 brani, sound funk/dance |
| 2020–2021 | *Break My Heart*; **MTV VMA Video of the Year** (*Break My Heart*, 2020) |
| 2021 | ***Levitating*** — #1 Billboard Hot 100; **Grammy 2021**: Best Pop Vocal Album e Best Dance/Electronic Album (*Future Nostalgia*); **Grammy 2022**: Record of the Year per *Levitating* |
| 2022 | Tour mondiale *Future Nostalgia* (Europa, Nord America, Asia, Australia); *Training Season* (con **Angèle**) |
| 2023 | ***Radical Optimism*** — #1 UK; *Houdini* (#1 UK), *Illusion*, *End of the World*; *We Can't Be Friends* (con **Missy Elliott**) |
| 2023–2024 | ***Radical Optimism World Tour*** — date a sold out in Nord America e Europa |

### 4.3 Discografia (album studio)

| Anno | Album | Posizionamenti principali |
|------|-------|---------------------------|
| 2017 | *Dua Lipa* | #1 UK, top 10 US |
| 2020 | *Future Nostalgia* | #1 UK, #2 Billboard 200 |
| 2023 | *Radical Optimism* | #1 UK |

Tutti e tre multiplatino in diversi mercati (certificazioni visibili sui portali discografici ufficiali).

### 4.4 Premi principali (registri pubblici)
- **Grammy:** 4 (2021 ×2, 2022 ×2)
- **Brit Awards:** Best British Female (2019)
- **MTV VMA:** Video of the Year (2020)
- Nomination/multipli riconoscimenti: American Music Awards, Billboard Music Awards, iHeartRadio Awards

### 4.5 Progetti e attività in corso (pubblici)
- **Attività discografica e touring** continua (ultimo tour: Radical Optimism World Tour 2023–2024).
- **UN Women** — ruolo di ambasciatrice (annunciato nel 2021); partecipazione a eventi pubblici dell'ente.
- **Campagne commerciali pubbliche:** L'Oréal Paris, Fenty Beauty — comunicate sui canali ufficiali e sulla stampa.

### 4.6 Interlocutori pubblici
| Entità | Tipo di relazione | Fonte |
|--------|-------------------|-------|
| Warner Music (UK/internazionale) | Etichetta discografica | Contratti pubblici, crediti |
| Calvin Harris | Collaborazione musicale (*One Kiss*) | Crediti discografici |
| Angèle | Collaborazione musicale (*Training Season*) | Crediti discografici |
| Missy Elliott | Collaborazione musicale (*We Can't Be Friends*) | Crediti discografici |
| Nicki Minaj | Collaborazione (*Hotter than Hell*) | Crediti discografici |
| UN Women | Ambasciatrice | Comunicati istituzionali |
| L'Oréal, Fenty Beauty | Campagne pubbliche | Comunicazione brand |
