# Aggiornare il calendario di homis.space

Istruzioni operative, valide per ogni aggiornamento. Si possono incollare in Claude e fargli eseguire il lavoro.

Il sito è una pagina HTML sola, senza compilazione e senza dipendenze. Si modifica il file, si carica qui, e Netlify pubblica da solo in una decina di secondi. Non c'è nessuno zip da fare e nessun pannello da aprire.

Non ridisegnare niente e non riscrivere i testi. Il lavoro è il calendario e le immagini delle serate.

## 1. I file

```
sito/index.html            il sito, l'unico file da modificare
sito/homis-wordmark.png    marchio, non toccare
sito/homis-lockup.png      marchio con la riga Record Store Bar, non toccare
sito/brand/index.html      brand kit su homis.space/brand, non toccare
sito/loc/                  le locandine, una per serata
```

Apri `sito/index.html` e leggilo tutto prima di cominciare. In fondo, dentro il tag `<script>`, c'è la tabella delle serate con sopra un commento che spiega come funziona.

## 2. La tabella delle serate

È l'unica fonte del calendario. Da qui si costruiscono il calendario grande in alto, il muro delle locandine, l'ordine, le serate spente e la riga che dice se il locale è aperto adesso.

```js
const SERATE = [
  {d:'2026-10-01', nome:'Nome della serata', f:'takeover',  sub:'DJ select',       loc:'loc/01-10.jpg'},
  {d:'2026-10-07', nome:'Listening',         f:'listening', sub:'Un disco intero', foto:'loc/07-10-foto.jpg'}
];
```

- **`d`** — data in formato `'AAAA-MM-GG'`. Le righe vanno in ordine di data crescente.
- **`nome`** — il nome della serata, scritto come sta sulla locandina. Se la locandina dice CHAKA, qui va Chaka.
- **`f`** — il formato, decide il colore quando manca la locandina vera. Valori ammessi: `listening` viola, `release` acido, `takeover` magenta, `open` blu.
- **`sub`** — il sottotitolo, anche questo preso dalla locandina. Se dice DJ SELECT, scrivi `DJ select`, non `DJ set`.
- **`loc`** — percorso della locandina vera, relativo alla cartella `sito/`. È il caso normale.
- **`foto`** — alternativa a `loc` quando la locandina manca o non si può usare: costruisce il poster di sistema nel colore del formato e ci mette la foto dentro l'ovale.

Una riga ha `loc` **oppure** `foto`, mai tutti e due.

## 3. Ordine e numero delle serate

L'ordine lo calcola il codice in base al giorno corrente: la serata più vicina va in testa, le passate scendono in fondo in bianco e nero. Basta mettere le righe in ordine di data.

Il muro è a **quattro colonne fisse** da 860 pixel in su, due sotto. Un numero di serate **multiplo di quattro** chiude le righe esatte: otto serate fanno due righe piene, dodici ne fanno tre. Se ne avanzano una o due spaiate, tieni in tabella una serata già passata per pareggiare, oppure togline una vecchia.

A ogni cambio di mese togli dalla tabella le serate del mese precedente, e da `sito/loc/` le immagini che non usa più nessuna riga.

## 4. Le immagini

**Locandine di serata.** Proporzione **4:5 verticale**, obbligatoria: il riquadro è 4:5 e un'immagine di altre proporzioni viene tagliata.

- ridimensiona a **900 pixel di larghezza**, quindi 1125 di altezza
- salva in **JPEG qualità 84**, progressivo, ottimizzato
- ogni file deve stare fra 150 e 250 KB
- nome del file `sito/loc/GG-MM.jpg`, per esempio `sito/loc/07-10.jpg`

**Foto dentro l'ovale**, solo per le serate senza locandina. Proporzione **8:7 orizzontale**, circa 1120 × 980 pixel, JPEG qualità 82, nome `sito/loc/GG-MM-foto.jpg`. Va consegnata **a colori e non trattata**: bianco e nero, contrasto e fusione nel colore della serata li applica la pagina. Soggetti: persone dentro il locale, mani sui piatti, dischi, il bancone, la strada davanti alla porta. Niente volti riconoscibili senza consenso, niente targhe leggibili.

## 5. Gli altri due elenchi nello stesso file

Cambiare solo la tabella rende il sito giusto per chi lo guarda e sbagliato per Google. Nello stesso `index.html` ci sono altri due elenchi, e devono dire le stesse serate.

**Dati strutturati.** Nel `<head>`, dentro `<script type="application/ld+json">`, un array con un evento per serata. Non scriverlo a memoria: copia una voce esistente e cambia data, nome e descrizione. Occhio al fuso orario: fino al **24 ottobre 2026** l'Italia è `+02:00`, dal **25 ottobre** passa a `+01:00`. Una serata del 7 novembre si scrive `2026-11-07T18:00:00+01:00` e finisce `2026-11-08T00:00:00+01:00`.

**Lista statica.** Più in basso, dentro `<noscript>`, una `<ul class="lista-statica">` con una riga per serata.

Alla fine i tre elenchi — tabella, dati strutturati, lista statica — devono contenere le stesse serate. Se non coincidono c'è un errore.

## 6. Regole che non si infrangono

- **La parola jazz non esiste.** Non nei nomi, non nei sottotitoli, non nelle descrizioni. E non si usa una locandina che abbia la parola dentro la grafica: quella serata va messa con `foto` e il poster di sistema. È una decisione di posizionamento della proprietà.
- **"Cocktail" non è una parola HOMIS.** Mai, da nessuna parte.
- **Gli orari sono sempre gli stessi**: da mercoledì a sabato, dalle 18 a mezzanotte, tutte le settimane. Niente che suggerisca apertura saltuaria, a discrezione o temporanea.
- **Mai elencare le etichette del gruppo.** HOMIS è un posto per tutti quelli per cui la musica è un denominatore comune.
- **Non toccare**: il testo lungo della sezione "Il posto", la frase grande sopra di esso, i colori, il calendario grande del mese, il brand kit in `sito/brand/index.html`. Se sembrano da cambiare, fermarsi e chiedere.

## 7. Controllare prima di pubblicare

Apri `sito/index.html` in locale, con doppio clic, e verifica:

- numero delle locandine e ordine, con la serata più vicina in alto a sinistra
- serate passate in bianco e nero, future a colori
- il calendario grande elenca tutte le date e il mese è quello giusto
- cerca "jazz" nella pagina: zero risultati
- riduci la finestra a larghezza telefono: il muro va a due colonne, senza immagini schiacciate

In locale i caratteri possono apparire diversi, perché vengono caricati da internet: non è un problema, si sistema da solo una volta online.

## 8. Pubblicare

Carica i file modificati su questo repository, sul ramo principale. Netlify se ne accorge da solo e pubblica in una decina di secondi.

Se lavori da riga di comando:

```
git add sito
git commit -m "Calendario ottobre"
git push
```

Se lavori dal sito di GitHub: apri la cartella, usa **Add file → Upload files** per le immagini nuove, e la matita per modificare `sito/index.html`. In entrambi i casi scrivi nel messaggio cosa hai cambiato, per esempio "Calendario ottobre": serve a ritrovare la versione giusta se bisogna tornare indietro.

## 9. Verificare online

Dopo un minuto apri `https://homis.space/?v=` seguito da un numero a caso, per saltare la cache, e rifai i controlli del punto 7 sulla versione pubblicata.

Se qualcosa esce male, non si corregge di fretta: si avvisa e si ripristina la versione precedente dallo storico.
