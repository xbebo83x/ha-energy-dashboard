📊 SQL Sensors

Benvenuto!

Se sei arrivato qui probabilmente ti stai chiedendo:

«"Perché HA Energy Suite utilizza dei sensori SQL?"»

La risposta è semplice.

Alcune informazioni mostrate nelle dashboard (come i report mensili e annuali) non sono disponibili come normali sensori di Home Assistant.

Per questo motivo HA Energy Suite legge direttamente il database interno di Home Assistant e crea automaticamente nuovi sensori con tutti i dati necessari.

Non preoccuparti: non serve conoscere SQL.

Ti basterà seguire questa guida passo dopo passo.

---

❓ Cos'è un sensore SQL?

Un sensore SQL è un normale sensore di Home Assistant che invece di leggere un dispositivo (ad esempio un inverter o un termometro) legge direttamente il database di Home Assistant.

In pratica recupera i dati storici già salvati dalla Dashboard Energia.

Una volta configurato funzionerà come qualsiasi altro sensore.

---

✅ Perché è necessario?

HA Energy Suite utilizza questi sensori per calcolare:

- Produzione mensile
- Energia acquistata dalla rete
- Energia immessa in rete
- Consumo della casa
- Report mensili
- Report annuali
- Storico dei consumi
- Storico della produzione

Senza questi sensori alcune dashboard non potrebbero funzionare.

---

📋 Requisiti

Prima di iniziare assicurati di avere:

- Home Assistant installato e funzionante.
- Dashboard Energia configurata.
- Alcuni giorni di dati storici.
- Accesso ai file di configurazione di Home Assistant.

---

🚀 Installazione

Passo 1 - Copia il file

Copia il file:

sql_sensors.yaml

all'interno della cartella:

/config/sql/

Se la cartella "sql" non esiste puoi crearla tranquillamente.

La struttura finale sarà simile a questa:

/config
│
├── configuration.yaml
│
├── sql
│   └── sql_sensors.yaml

---

Passo 2 - Modifica configuration.yaml

Apri il file:

/config/configuration.yaml

e aggiungi questa riga:

sql: !include sql/sql_sensors.yaml

Esempio:

homeassistant:

default_config:

frontend:

sql: !include sql/sql_sensors.yaml

Salva il file.

---

⚠ Se utilizzi già altri sensori SQL

Nel file "configuration.yaml" può esistere una sola sezione "sql:".

Quindi questa configurazione è corretta:

sql: !include sql/sql_sensors.yaml

Questa invece è sbagliata:

sql: !include sql/sql_sensors.yaml
sql: !include altri_sensori.yaml

Se utilizzi già SQL dovrai semplicemente copiare i sensori di HA Energy Suite dentro il tuo file SQL esistente.

---

Passo 3 - Riavvia Home Assistant

Riavvia completamente Home Assistant.

Se il file YAML contiene errori Home Assistant te lo segnalerà all'avvio.

---

🔧 Adesso arriva l'unica parte da personalizzare

Questa operazione va fatta una sola volta.

---

Cos'è un metadata_id?

Ogni sensore della Dashboard Energia possiede un numero identificativo interno.

Questo numero si chiama metadata_id.

HA Energy Suite utilizza questi numeri per sapere quali dati leggere dal database.

Ogni installazione di Home Assistant ha numeri diversi.

Per questo motivo dovrai sostituire quelli presenti nel file SQL con i tuoi.

Non devi inventarli.

Devi semplicemente copiarli.

---

📥 Come trovare i metadata_id

Il modo più semplice è utilizzare il programma gratuito:

DB Browser for SQLite

Apri il database di Home Assistant:

/config/home-assistant_v2.db

Apri la tabella:

statistics_meta

Vedrai una tabella simile a questa:

id| statistic_id
265| sensor.inverter_total_production
269| sensor.inverter_total_energy_import
270| sensor.inverter_total_energy_export
274| sensor.inverter_total_load_consumption

⚠ I numeri mostrati sopra sono soltanto un esempio.

Sul tuo Home Assistant saranno quasi sicuramente diversi.

---

✏ Modifica il file SQL

Apri il file:

sql_sensors.yaml

Troverai righe simili a questa:

WHERE metadata_id = 265

Sostituisci solamente il numero.

Ad esempio:

WHERE metadata_id = 148

Non modificare altro.

Ripeti l'operazione per tutti i sensori presenti nel file.

---

Come faccio a sapere quale sensore cercare?

Nel database cerca il nome dei tuoi sensori energetici.

Ad esempio:

- Produzione totale inverter
- Energia acquistata
- Energia immessa
- Consumo totale della casa

Ogni impianto utilizza nomi differenti.

L'importante è individuare il sensore corretto e copiarne il relativo metadata_id.

---

✅ Come verificare che tutto funzioni

Dopo il riavvio vai in:

Impostazioni → Dispositivi e Servizi → Entità

e cerca uno dei sensori creati da HA Energy Suite.

Se il sensore mostra un valore significa che la configurazione è corretta.

---

❌ Problemi comuni

I sensori sono "Unavailable"

Controlla:

- che il file sia stato copiato nella cartella corretta;
- che "configuration.yaml" contenga la riga "sql: !include sql/sql_sensors.yaml";
- che Home Assistant sia stato riavviato;
- che i metadata_id siano corretti.

---

Tutti i valori sono zero

Quasi sempre significa che il metadata_id non corrisponde al sensore corretto oppure che la Dashboard Energia non dispone ancora di dati storici.

---

Home Assistant non si avvia

Probabilmente c'è un errore di sintassi nel file YAML.

Controlla gli spazi e l'indentazione oppure utilizza il controllo configurazione di Home Assistant prima del riavvio.

---

💡 Consiglio

Prima di modificare qualsiasi file di configurazione fai sempre un backup di Home Assistant.

In questo modo potrai tornare facilmente alla situazione precedente in caso di errore.

---

❤️ Hai bisogno di aiuto?

HA Energy Suite è un progetto open source sviluppato nel tempo libero.

Se incontri difficoltà puoi aprire una Issue su GitHub oppure scrivere nel gruppo Facebook dedicato a Home Assistant allegando:

- uno screenshot della tabella "statistics_meta";
- il messaggio di errore (se presente);
- la versione di Home Assistant utilizzata.

In questo modo sarà molto più semplice aiutarti.

Buon divertimento con HA Energy Suite! ☀️