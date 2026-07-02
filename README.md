# ☀️ HA Energy Suite

A collection of professional Home Assistant cards dedicated to photovoltaic systems.

The goal of this project is simple:

- Beautiful cards
- Easy installation
- No complex integrations
- No mandatory templates
- No packages
- Minimal configuration

Every card is independent and can be installed in just a few minutes.

---

# 📦 Requirements

Depending on the selected card, you may need:

- Home Assistant
- Energy Dashboard configured
- custom:button-card
- SQL Integration

Each card clearly indicates its requirements.

---

# 🚀 Installation

1. Download the desired card from the **cards/** folder.

2. If required, copy the corresponding SQL file from the **sql/** folder into:

```text
/config/sql/
```

3. Add the SQL include to your `configuration.yaml`:

```yaml
sql: !include sql/monthly-report-sql.yaml
```

4. Restart Home Assistant.

5. Configure the required sensors or metadata IDs following the instructions inside the SQL file.

6. Copy the YAML card into your Lovelace dashboard.

Done.

---

# 📋 Available Cards

| Card | Description |
|------|-------------|
| Monthly Report | Monthly photovoltaic history with production, consumption, self-sufficiency, estimated costs and savings. |

More cards will be added in future releases.

---

# 📷 Screenshots

Screenshots are available inside the **screenshots/** folder.

---

# 📁 Repository Structure

```text
HA-Energy-Suite
│
├── cards/
├── sql/
├── docs/
├── screenshots/
├── README.md
├── CHANGELOG.md
├── ROADMAP.md
├── CONTRIBUTING.md
├── BRAND.md
└── LICENSE
```

---

# 🤝 Contributing

Suggestions, improvements and pull requests are always welcome.

---

# 📄 License

This project is released under the MIT License.