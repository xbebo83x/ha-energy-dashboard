\# Installazione



\## Requisiti



\- Home Assistant

\- Dashboard Energia configurata

\- custom:button-card

\- SQL Integration



\## Installazione



1\. Copia il file:



sql/monthly-report-sql.yaml



nella cartella



/config/sql/



2\. Nel tuo configuration.yaml aggiungi:



sql: !include sql/monthly-report-sql.yaml



3\. Riavvia Home Assistant.



4\. Individua i metadata\_id eseguendo:



SELECT id, statistic\_id

FROM statistics\_meta

ORDER BY statistic\_id;



5\. Sostituisci i quattro metadata\_id nel file SQL.



6\. Copia il contenuto di



cards/monthly-report.yaml



nella tua dashboard Lovelace.



Fine.

