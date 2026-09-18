# Värmefläkt-app

En liten hemmagjord app (PWA) med en knapp som sätter igång värmefläkten/suget
på 40% i 3 timmar via Shelly-enhetens lokala API, och en knapp för att stänga
av direkt. Fungerar på både iPhone och Android genom att du lägger till sidan
på hemskärmen – ingen App Store behövs.

Shellyns IP-adress, sugnivå och antal timmar går att ändra direkt i appen
under "Inställningar", ingen kodändring behövs vid en ny IP-adress.

## 1. Lägg upp koden på GitHub

I Git Bash, i mappen där du vill ha projektet lokalt:

```
gh repo create varmeflakt-app --public --source=. --remote=origin
```

(kör detta inifrån den uppackade `varmeflakt-app`-mappen). Om du hellre vill
skapa repot manuellt på github.com, gör det där och kör sedan:

```
git init
git add .
git commit -m "Första versionen av värmefläkt-appen"
git branch -M main
git remote add origin https://github.com/DITT-ANVANDARNAMN/varmeflakt-app.git
git push -u origin main
```

## 2. Aktivera GitHub Pages (gratis hosting med https)

1. Gå till repot på github.com.
2. Settings → Pages (i vänstermenyn).
3. Under "Build and deployment", välj Source: "Deploy from a branch".
4. Branch: `main`, mapp: `/ (root)`. Klicka Save.
5. Vänta en minut, ladda om sidan. Du får en länk i stil med
   `https://DITT-ANVANDARNAMN.github.io/varmeflakt-app/`.

Det är denna länk du öppnar på telefonerna.

## 3. Installera på iPhone

1. Öppna länken i Safari (måste vara Safari, inte Chrome, för att
   "Lägg till på hemskärmen" ska fungera fullt ut).
2. Tryck på dela-ikonen (fyrkant med pil uppåt) längst ner.
3. Scrolla ner och välj "Lägg till på hemskärmen".
4. Döp den om du vill, tryck "Lägg till".

Nu ligger appen som en egen ikon på hemskärmen och öppnas i fullskärm, utan
webbläsarfält.

## 4. Installera på Android

1. Öppna länken i Chrome.
2. Tryck på de tre punkterna uppe till höger.
3. Välj "Installera app" (eller "Lägg till på startskärmen" om det alternativet visas istället).
4. Bekräfta.

## 5. Justera inställningar

Om Shellyns IP-adress ändras (t.ex. om routern delar ut en ny adress), öppna
appen, tryck på "Inställningar" längst ner, skriv in den nya IP-adressen och
tryck "Spara". Samma ställe används för att ändra sugnivån (standard 40%)
eller hur länge den ska vara på (standard 3 timmar).

## Bra att veta

- Telefonen måste vara på samma wifi-nätverk som Shelly-enheten när du
  trycker på knapparna (precis som när du kom åt inställningssidan i
  webbläsaren tidigare).
- Knapparna öppnar kortvarigt en osynlig flik mot Shellyns egen adress och
  stänger den igen automatiskt – det är en teknisk nödvändighet eftersom
  appen själv körs på en säker (https) adress men Shellyn bara pratar osäker
  (http) lokalt. Du behöver inte göra något åt det, det sker automatiskt.
- "Sug 40% i 3 timmar"-knappen ber Shellyn stänga av sig själv automatiskt
  efter angiven tid (`toggle_after`), så den stängs av även om appen eller
  telefonen är avstängd under tiden.
