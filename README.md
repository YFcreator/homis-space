# homis.space

Sito di HOMIS Record Store Bar, Via Thaon di Revel 3, Isola, Milano.

Pagina HTML sola, senza compilazione e senza dipendenze. Ogni modifica caricata sul ramo principale viene pubblicata da Netlify in una decina di secondi su [homis.space](https://homis.space). Non serve fare altro: niente zip, niente caricamenti a mano.

```
sito/
  index.html            il sito, l'unico file da modificare
  homis-wordmark.png    marchio
  homis-lockup.png      marchio con la riga Record Store Bar
  brand/index.html      brand kit, pubblicato su homis.space/brand
  loc/                  le locandine, una per serata
netlify.toml            dice a Netlify di pubblicare la cartella sito
```

## Aggiornare il calendario

Le istruzioni complete stanno in [`AGGIORNARE-IL-CALENDARIO.md`](AGGIORNARE-IL-CALENDARIO.md). In breve: si modifica la tabella `SERATE` in fondo a `sito/index.html`, si aggiungono le locandine in `sito/loc/`, si allineano gli altri due elenchi dentro lo stesso file, si carica tutto qui.

## Cosa non si tocca

Il testo lungo della sezione "Il posto", la frase grande sopra di esso, i colori, il calendario grande del mese e il brand kit in `sito/brand/index.html`. Se sembrano da cambiare, si chiede prima.

## Se qualcosa esce male

Ogni modifica caricata qui resta nello storico. Si torna alla versione precedente aprendo il progetto su Netlify, sezione Deploys, e ripubblicando il deploy di prima. Il sito torna com'era in pochi secondi.
