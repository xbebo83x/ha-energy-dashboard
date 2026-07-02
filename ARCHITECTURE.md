\# Architecture



This document describes the architecture and design principles of \*\*HA Energy Suite\*\*.



The goal is to keep the project modular, scalable and easy to maintain over time.



\---



\# Design Philosophy



HA Energy Suite is designed as a complete energy analysis platform for Home Assistant.



The project is built around one simple idea:



> Raw energy data should become meaningful information.



Dashboards are only the final layer.



The real value of the project comes from data processing and analysis.



\---



\# Project Architecture



HA Energy Suite is divided into independent modules.



```

&#x20;               Home Assistant



&#x20;                      │



&#x20;       ┌──────────────┴──────────────┐



&#x20;       │                             │



&#x20;  Native Sensors               SQL History



&#x20;       │                             │



&#x20;       └──────────────┬──────────────┘



&#x20;                      │



&#x20;               Template Sensors



&#x20;                      │



&#x20;               Utility Meters



&#x20;                      │



&#x20;              Calculated Sensors



&#x20;                      │



&#x20;     ┌────────────────┼────────────────┐



&#x20;     │                │                │



&#x20;Overview         Reports        Statistics



&#x20;                      │



&#x20;                User Dashboard

```



\---



\# Layers



\## Layer 1 — Data Sources



The first layer contains raw data.



Examples:



\- photovoltaic production

\- battery status

\- grid import/export

\- house consumption

\- SQL historical data



No calculations should be performed here.



\---



\## Layer 2 — Data Processing



The second layer transforms raw data into useful information.



Examples:



\- real savings

\- estimated bill

\- self-sufficiency

\- yearly production

\- monthly statistics



This is the core of HA Energy Suite.



\---



\## Layer 3 — User Interface



The third layer displays the processed information.



Examples:



\- Overview dashboard

\- Solar dashboard

\- Monthly report

\- Yearly statistics



Dashboards should never perform calculations whenever possible.



They should only display processed data.



\---



\# Project Structure



```

assets/

dashboards/

docs/

examples/

screenshots/

sql/

templates/

utility\_meters/

```



Each folder has a single responsibility.



\---



\# Modularity



Every module should work independently.



Users should be able to install only the components they need.



Example:



\- only Statistics

\- only Reports

\- only Solar Overview



without installing the entire project.



\---



\# Installation Philosophy



HA Energy Suite is designed to provide a guided installation.



The objective is:



> Install the project in approximately 5–10 minutes.



Users should configure only the required entities.



Everything else should work automatically.



\---



\# Coding Principles



The project follows these principles:



\- Keep it simple.

\- Keep it modular.

\- Prefer readability over complexity.

\- Document everything.

\- Avoid duplicated logic.

\- Separate data from presentation.



\---



\# Future



The architecture has been designed to support future expansions, including:



\- additional dashboards

\- new energy providers

\- multiple inverter brands

\- HACS integration

\- localization

\- community modules



without requiring major architectural changes.

