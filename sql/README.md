# 📊 SQL Sensors

Benvenuto!

Questa cartella contiene i sensori SQL utilizzati da **HA Energy Suite**.

Questi sensori leggono il database di Home Assistant per recuperare i dati storici della Dashboard Energia.

Non preoccuparti se non hai mai usato SQL: ti guideremo passo dopo passo.

---

# ❓ Cos'è un sensore SQL?

Un sensore SQL è un normale sensore di Home Assistant che, invece di leggere un dispositivo fisico, legge i dati già salvati nel database interno di Home Assistant.

HA Energy Suite li usa per recuperare:

- produzione fotovoltaica mensile;
- energia acquistata dalla rete;
- energia immessa in rete;
- consumo della casa;
- report mensili;
- report annuali.

---

# 📋 Requisiti

Prima di iniziare assicurati di avere:

- Home Assistant funzionante;
- Dashboard Energia configurata;
- Visual Studio Code Server installato, oppure accesso al Terminale;
- accesso al file `configuration.yaml`.

---

# 🚀 Installazione

## Passo 1 - Copia il file

Copia il file:

```text
energy-sql.yaml
```

nella cartella:

```text
/config/sql/
```

Se la cartella `sql` non esiste, creala manualmente.

La struttura finale deve essere questa:

```text
/config
│
├── configuration.yaml
│
├── sql
│   └── energy-sql.yaml
```

---

## Passo 2 - Modifica `configuration.yaml`

Apri il file:

```text
/config/configuration.yaml
```

Devi aggiungere questa riga:

```yaml
sql: !include sql/energy-sql.yaml
```

La riga va inserita **allineata a sinistra**, senza spazi prima.

Esempio corretto:

```yaml
homeassistant:

default_config:

frontend:

sql: !include sql/energy-sql.yaml
```

Anche così va bene:

```yaml
default_config:

template: !include templates/core-sensors.yaml
utility_meter: !include utility_meters/utility_meters.yaml
sql: !include sql/energy-sql.yaml
```

Non inserirla dentro un'altra sezione.

Esempio sbagliato:

```yaml
homeassistant:
  sql: !include sql/energy-sql.yaml
```

Esempio sbagliato:

```yaml
sensor:
  sql: !include sql/energy-sql.yaml
```

La voce `sql:` deve stare al livello principale del file, come `template:`, `sensor:`, `utility_meter:` o `automation:`.

Salva il file.

---

## ⚠ Se hai già una sezione `sql:`

Nel file `configuration.yaml` può esistere **una sola voce `sql:`**.

Questo è corretto:

```yaml
sql: !include sql/energy-sql.yaml
```

Questo è sbagliato:

```yaml
sql: !include sql/energy-sql.yaml
sql: !include altri_sensori.yaml
```

Se hai già una riga `sql:` nel tuo `configuration.yaml`, non aggiungerne un'altra.

In quel caso devi copiare il contenuto di `energy-sql.yaml` dentro il file SQL che stai già usando.

---

## Passo 3 - Trova i numeri dei tuoi sensori

Questa è l'unica parte personalizzata.

Apri **Visual Studio Code Server**.

Apri il **Terminale**.

Digita:

```bash
sqlite3 /config/home-assistant_v2.db
```

e premi **Invio**.

Ora incolla questo comando:

```sql
SELECT id, statistic_id
FROM statistics_meta
ORDER BY statistic_id;
```

Premi di nuovo **Invio**.

Comparirà una lista lunga, simile a questa:

```text
265|sensor.inverter_total_production
269|sensor.inverter_total_energy_import
270|sensor.inverter_total_energy_export
274|sensor.inverter_total_load_consumption
...
```

Quei numeri a sinistra sono i `metadata_id`.

Per uscire dal database scrivi:

```text
.quit
```

e premi **Invio**.

---

## Passo 4 - Lascia fare a ChatGPT 😄

Non cercare manualmente i sensori.

Copia tutto l'elenco restituito dal Terminale.

Poi apri ChatGPT e incolla:

- l'elenco dei sensori;
- il contenuto del file `energy-sql.yaml`.

Scrivi questo messaggio:

> Questo è l'elenco dei miei sensori di Home Assistant e questo è il file `energy-sql.yaml` di HA Energy Suite. Sostituisci automaticamente tutti i `metadata_id` con quelli corretti del mio impianto senza modificare nient'altro.

ChatGPT ti restituirà il file già modificato.

Copia il risultato dentro il tuo file:

```text
/config/sql/energy-sql.yaml
```

e salva.

---

## Passo 5 - Controlla la configurazione

Prima di riavviare Home Assistant vai in:

```text
Impostazioni → Sistema → Controlla configurazione
```

Se non vengono segnalati errori puoi procedere.

---

## Passo 6 - Riavvia Home Assistant

Riavvia Home Assistant.

Se tutto è corretto, i sensori SQL verranno creati automaticamente.

---

# ✅ Verifica finale

Vai in:

```text
Impostazioni → Dispositivi e Servizi → Entità
```

e cerca uno dei sensori creati da HA Energy Suite.

Se il sensore mostra un valore, la configurazione è corretta.

---

# ❌ Problemi comuni

## I sensori non vengono creati

Controlla che:

- `energy-sql.yaml` sia in `/config/sql/`;
- `configuration.yaml` contenga questa riga:

```yaml
sql: !include sql/energy-sql.yaml
```

- la riga `sql:` sia allineata a sinistra;
- Home Assistant sia stato riavviato.

---

## Home Assistant non si avvia

Probabilmente la riga `sql:` è stata inserita nel punto sbagliato oppure c'è un errore di spaziatura.

Ricorda:

```yaml
sql: !include sql/energy-sql.yaml
```

deve stare al livello principale del file, senza spazi davanti.

---

## I sensori risultano "Unavailable"

Nella maggior parte dei casi i numeri dei sensori non sono corretti.

Ripeti il Passo 3 e il Passo 4.

---

# 💡 Consiglio

Prima di modificare i file di configurazione, fai sempre un backup di Home Assistant.

---

# ❤️ Hai bisogno di aiuto?

Se incontri difficoltà puoi aprire una **Issue** su GitHub oppure scrivere nel gruppo Facebook dedicato a Home Assistant.

Allega sempre:

- il messaggio di errore;
- la versione di Home Assistant;
- uno screenshot del problema.

Buona configurazione con **HA Energy Suite** ☀️