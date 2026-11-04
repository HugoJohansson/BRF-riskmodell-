# BRF-riskmodell

Upplägg för en modell över hur ekonomin i en bostadsrättsförening kan utvecklas under olika framtidsscenarier, vilka risker som kan tvinga fram avgiftshöjningar och vilka investeringar som kan minska dem.

**Status:** Det här är en skiss på upplägget, indata och förhoppningsvis tänkt utdata. Tentaperiod, jobb och annat kom emellan, så ingen kod eller data är gjord än. Underhållsplanen ska uppdateras snart, och det kan vara bra att vänta in den för att få mer data.

Föreningen har 18 lägenheter, värms med fjärrvärme och ligger i Uppsala. Föreningens egna siffror ligger inte i repot.

## Frågor modellen ska besvara

- Hur stor är sannolikheten att avgiften behöver höjas med mer än 10 % inom 5 respektive 10 år?
- Räcker underhållsfonden för de planerade åtgärderna, och hur ser det ut i sämre fall?
- Vilka drivkrafter förklarar mest av osäkerheten: räntor, energipriser eller klimat?
- Lönar sig en värmepump, ett batterilager eller solceller, och håller kalkylen även i de sämre scenarierna?
- Vilka beslut bör styrelsen ta nu, och vilka kan vänta?

## Horisonter

| Horisont | Används till |
|---|---|
| 5 år | Kortsiktig likviditet: räcker fonden och kan lånen betalas? |
| 10 år | Nästa avgiftsbeslut och större underhållscykler |
| 30 år | En full underhållscykel, med fasad, stammar och tak |
| 50 år | Livslängdsfrågor och stora investeringar |

Styrelsen ska först se 5 och 10 år, eftersom de är minst osäkra. För 30 och 50 år används en livslängdsmodell i stället för underhållsplanen, som då är föråldrad. Kostnaderna räknas i framtida kronor med kostnadsinflation.

## Moduler

1. **Risk och scenarier** för hela föreningen. Den görs först.
2. **Dränering:** risken för vattenskador mot kostnaden för att åtgärda nu. Föreningen har prioriterat dränering före fönster.
3. **Fönsterbyte:** energibalans, klimateffekt och återbetalningstid.
4. **Investeringar i energi:** värmepump, batterilager och solceller, se nästa avsnitt.

Modul 2–4 väntar tills riskmodulen fungerar.

## Investeringar

Tre investeringar jämförs mot att fortsätta som i dag, med bara fjärrvärme och köpt el.

| Investering | Vad den ska göra |
|---|---|
| Värmepump | Ta en del av värmen de kallaste timmarna så att fjärrvärmens effekttoppar och effektavgift sänks |
| Batterilager | Flytta elanvändning från dyra till billiga timmar och kapa effekttoppar på elnätet |
| Solceller | Producera el till föreningens gemensamma behov, som tvättstuga, belysning och värmepumpen |

Varje investering bedöms med två mått:

- **Nettonuvärde (NNV):** alla framtida besparingar minus drift och underhåll, diskonterade med en kalkylränta, minus investeringen. Positivt NNV betyder att investeringen lönar sig.
- **Återbetalningstid (payback):** hur många år det tar innan besparingarna har betalat investeringen.

Båda räknas i varje scenario och inte bara i bas. En investering som bara lönar sig när energipriset är högt blir då synlig. Kombinationer prövas också, till exempel solceller med batteri eller värmepump med solceller, eftersom de påverkar varandras lönsamhet.

Indata för investeringarna:

- investeringskostnad och eventuella bidrag, från offerter/onlinekällor
- teknisk livslängd och underhållskostnad
- kalkylränta, kopplad till föreningens låneränta
- fjärrvärmens energi- och effektpris, från fjärrvärmeleverantörens prislista
- föreningens timvisa förbrukning av värme och el, om den går att få ut
- solinstrålning för Uppsala, från SMHI

## Indata

Underhållsplanen är första källan. Varje komponent har samma kolumner, så att en ny plan kan ersätta den gamla rad för rad. 

| Värde | Källa | Osäkerhet |
|---|---|---|
| Lån och räntor | Årsredovisning | Låg |
| Avgiftsintäkter | Årsredovisning | Låg |
| Underhållsåtgärder och kostnader | Underhållsplan, besiktning | Hög |
| Investeringskostnader | Offerter | Medel |
| Fjärrvärmepris och effektavgift | Fjärrvärmeleverantörens prislista | Medel |
| Graddagar och solinstrålning | SMHI | Medel |
| Elpris SE3 | Nord Pool | Hög |
| Styrränta | Riksbanken | Medel |

Varje värde ska ha en källa och en bedömd osäkerhet. Antaganden utan källa markeras.

## Drivkrafter

- **Räntor:** Riksbankens styrränta och bolånemarginaler
- **Inflation:** KPI och byggkostnadsindex
- **Energi:** fjärrvärmepris, effektavgift och elpris i SE3
- **Klimat:** graddagar, värmeböljor, skyfall, vattenskador och försäkringspremier, utifrån SMHI:s scenarier för Uppsala
- **Omvärld:** energichocker och valutaeffekter som slår mot byggpriser och räntor

Klimatprojektioner säger mer om trender och hur ofta något händer än om exakta belopp. De används för att välja scenarier, inte som prognoser.

## Scenarier

| Scenario | Antagande |
|---|---|
| Bas | Historisk trend för räntor, priser och skador |
| Höga räntor | Hög inflation och höga räntor i flera år |
| Energichock | Fjärrvärme och el dubbelt så dyra under en period |
| Klimatskada | Ett skyfall ger en vattenskada och en åtgärd som inte kan vänta |
| Worst case | Höga räntor, energichock och klimatskada samtidigt |

Siffrorna för varje scenario sätts när indata är klara. Höga räntor gör investeringarna mindre lönsamma, medan en energichock gör dem mer lönsamma. Därför prövas investeringarna mot alla scenarier.

## Utdata

- Sannolikheten för en avgiftshöjning på mer än 10 % inom 5 och 10 år, med och utan investeringarna
- Underhållsfondens saldo som percentiler (10:e och 90:e) för varje horisont
- NNV och återbetalningstid för varje investering och kombination, per scenario
- En känslighetsanalys som visar hur mycket av utfallet varje drivkraft förklarar

## AI-användning

Se [`AI-DEKLARATION.md`](AI-DEKLARATION.md).
