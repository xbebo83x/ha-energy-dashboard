\# 📈 Monthly Report



<p align="center">

&#x20; <img src="screenshot.png" alt="Monthly Report">

</p>



\## Overview



\*\*Monthly Report\*\* è una dashboard per Home Assistant che offre una panoramica dettagliata dell'andamento energetico del mese corrente.



La card raccoglie in un'unica schermata i principali indicatori dell'impianto fotovoltaico, combinando dati energetici ed economici con grafici di avanzamento e suggerimenti automatici.



Fa parte del progetto \*\*HA Energy Suite\*\* e utilizza i sensori SQL condivisi.



\---



\## Features



La card mostra in tempo reale:



\- ☀️ Produzione fotovoltaica del mese

\- 🏠 Consumo dell'abitazione

\- ⚡ Energia prelevata dalla rete

\- 🔌 Energia immessa in rete

\- 📊 Autosufficienza con indicatore grafico

\- 💰 Costo stimato della bolletta con fotovoltaico

\- 💸 Costo stimato senza fotovoltaico

\- 💚 Beneficio economico complessivo

\- 🔄 Avanzamento del mese

\- 📈 Stima del beneficio a fine mese

\- 💡 Suggerimenti automatici basati sull'andamento dell'impianto



\---



\## Requirements



Prima dell'installazione assicurati di avere:



\- Home Assistant

\- Dashboard Energia configurata

\- SQL Integration

\- `custom:button-card`



È inoltre necessario installare i sensori SQL condivisi presenti nella cartella:



```text

/sql/

```



La card utilizza anche alcuni helper di Home Assistant per il calcolo dei costi:



\- `input\_number.fv\_rata\_mensile`

\- `input\_number.costo\_kwh\_reale`

\- `input\_number.quota\_fissa\_giornaliera\_corrente`

\- `input\_number.fv\_valore\_ssp\_kwh`

\- `sensor.canone\_tv\_mensile`



\---



\## Installation



1\. Installa il file SQL presente nella cartella `/sql`.

2\. Configura i `metadata\_id` seguendo le istruzioni del file SQL.

3\. Riavvia Home Assistant.

4\. Configura gli helper richiesti.

5\. Copia `monthly-report.yaml` nella tua dashboard Lovelace.



L'installazione richiede solo pochi minuti.



\---



\## Notes



\- I dati vengono aggiornati automaticamente utilizzando le Long-Term Statistics della Dashboard Energia.

\- Il beneficio economico mostrato è calcolato come \*\*risparmio + valore stimato dello Scambio sul Posto (SSP)\*\*.

\- Le valutazioni sull'autosufficienza e i suggerimenti vengono generati automaticamente in base ai dati del mese corrente.



\---



\## Support



Hai trovato un bug o hai un suggerimento?



Apri una \*\*GitHub Issue\*\* oppure una \*\*Pull Request\*\*.



Se questa card ti è stata utile, lascia una ⭐ al repository o considera di supportare il progetto tramite \*\*GitHub Sponsors\*\*.



\---



\## License



Distribuito con licenza \*\*MIT\*\*.

