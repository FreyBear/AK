fi# AK26 Tidsplan

Interaktiv tidsplan for Stavanger Studentsangforening under Akademisk Kortreff (AK) i Trondheim.

Nettsiden er bygget som en enkel statisk HTML-side med innebygd CSS og JavaScript, og fungerer godt på mobil og desktop.

## Innhold

Prosjektet viser:

- Tidslinje fordelt på dager (torsdag til søndag)
- Hendelser med klokkeslett, sted, kartlenker og detaljerte notater
- Automatisk markering av:
	- hva som pågår nå
	- hva som er neste post
	- hvilken dag som er aktiv
- Nedtelling til neste hendelse
- Hurtigknapp for å hoppe til aktuell/neste hendelse
- Nyttig praktisk info (transport, pakkeliste, nåler, annet utstyr)

## Filstruktur

- `index.html`: Hele applikasjonen (markup, stil og logikk)
- `README.md`: Dokumentasjon
- `secrets.example.env`: Eksempel pa variabler for deploy/drift

## Secrets og sikkerhet

Prosjektet bruker GitHub Codespaces Secrets for ekte passord og nøkler.

- Legg hemmeligheter i `Settings -> Secrets and variables -> Codespaces` i GitHub
- Bruk lokale override-verdier i `secrets.env` ved behov
- `secrets.env` er ignorert av git og skal ikke commits
- `secrets.example.env` kan trygt commits som mal uten hemmeligheter

## Kjøring lokalt

Du kan åpne siden direkte i nettleser:

1. Åpne `index.html`

Eller servere mappen lokalt (anbefalt ved videreutvikling):

```bash
python3 -m http.server 8080
```

Deretter åpner du `http://localhost:8080`.

## Hvordan logikken fungerer

JavaScript-koden i `index.html` gjør følgende:

1. Leser alle elementer med `.event[data-datetime]`
2. Konverterer `data-datetime` til tidspunkt (`Date`)
3. Sorterer hendelser kronologisk
4. Finner aktiv hendelse og neste hendelse basert på nåtid
5. Oppdaterer visning med CSS-klasser og badges
6. Oppdaterer nedtelling hvert minutt

Merk: En hendelse regnes som «pågår» i et vindu på 3 timer fra starttid.

## Redigere eller legge til hendelser

Hver hendelse følger denne strukturen:

```html
<div class="event" data-datetime="2026-04-17T16:00">
	<div class="event-time">⏰ 16:00</div>
	<div class="event-title">Tittel på hendelse</div>
	<div class="event-location">
		<span><a href="https://..." target="_blank">Sted</a></span>
	</div>
	<div class="event-notes">📝 Notater</div>
</div>
```

Tips:

- Bruk ISO-format i `data-datetime`: `YYYY-MM-DDTHH:MM`
- Sørg for riktig dato på nattarrangement (for eksempel etter midnatt)
- Test på mobil etter større endringer i innhold

## Forslag til videre funksjonalitet

Hvis dere vil utvide løsningen videre, er dette naturlige steg:

- Filtrering per dag / type aktivitet
- Søk i hendelser og notater
- Favorittmarkering av egne poster
- Eksport til kalender (ICS)
- Språkvalg (norsk/engelsk)
- Ekstern datakilde (JSON) i stedet for hardkodet innhold
- PWA-støtte for offline bruk under arrangement

## Vedlikehold

Siden er statisk og har ingen avhengigheter eller byggetrinn. Det gjør den enkel å drifte, dele og oppdatere raskt underveis i arrangementet.
