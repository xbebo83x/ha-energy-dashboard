\# 📊 Annual Report



<p align="center">

&#x20; <img src="screenshot.png" alt="Annual Report">

</p>



\## Overview



\*\*Annual Report\*\* è una card per Home Assistant che mostra il riepilogo annuale dell'impianto fotovoltaico in un'unica tabella.



Utilizzando i dati storici della Dashboard Energia, permette di confrontare rapidamente l'andamento dell'anno mese per mese.



La card fa parte del progetto \*\*HA Energy Suite\*\* e utilizza i sensori SQL condivisi.



\---



\## Features



Per ogni mese vengono visualizzati:



\- ☀️ Produzione fotovoltaica (kWh)

\- 🏠 Consumo dell'abitazione (kWh)

\- 📊 Autosufficienza (%)

\- 💸 Costo stimato senza fotovoltaico (€)

\- 💰 Costo stimato con fotovoltaico (€)

\- 💚 Risparmio stimato (€)

\- 🔵 Ricavo stimato da Scambio sul Posto (€)



La tabella include inoltre:



\- Evidenziazione automatica del mese corrente

\- Totali annuali

\- Autosufficienza media annuale

\- Aggiornamento automatico dei dati



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



\---



\## Installation



1\. Installa il file SQL presente nella cartella `/sql`.

2\. Configura i `metadata\_id` seguendo le istruzioni riportate nel file SQL.

3\. Riavvia Home Assistant.

4\. Copia il contenuto di `annual-report.yaml` nella tua dashboard Lovelace.



L'installazione richiede solo pochi minuti.



\---



\## Notes



\- Il mese corrente viene evidenziato automaticamente.

\- Il risparmio mostrato nella tabella \*\*non include\*\* il ricavo derivante dallo Scambio sul Posto (SSP).

\- Tutti i dati vengono letti dalle Long-Term Statistics della Dashboard Energia di Home Assistant.



\---



\## Support



Hai trovato un bug o hai un suggerimento?



Apri una \*\*GitHub Issue\*\* oppure una \*\*Pull Request\*\*.



Se questa card ti è stata utile, lascia una ⭐ al repository o considera di supportare il progetto tramite \*\*GitHub Sponsors\*\*.



\---



\## License



Distribuito con licenza \*\*MIT\*\*.

