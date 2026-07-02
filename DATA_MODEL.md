\# Data Model



This document defines the official data model used by \*\*HA Energy Suite\*\*.



Every dashboard, template, utility meter and future integration must use this model.



The purpose is to guarantee consistency across the entire project.



\---



\# Principles



Every data point should have:



\- One purpose

\- One unit

\- One calculation method

\- One official name



The same information should never exist twice under different names.



\---



\# Categories



The project is organized into the following data groups.



\- Production

\- Consumption

\- Grid

\- Battery

\- Self Sufficiency

\- Costs

\- Savings

\- Statistics

\- Forecasts



\---



\# Production



| Data | Unit |

|------|------|

| Current PV Power | W |

| Today Production | kWh |

| Month Production | kWh |

| Year Production | kWh |

| Lifetime Production | kWh |



\---



\# Consumption



| Data | Unit |

|------|------|

| Current House Consumption | W |

| Today Consumption | kWh |

| Month Consumption | kWh |

| Year Consumption | kWh |



\---



\# Grid



| Data | Unit |

|------|------|

| Current Grid Power | W |

| Today Import | kWh |

| Today Export | kWh |

| Month Import | kWh |

| Month Export | kWh |

| Year Import | kWh |

| Year Export | kWh |



\---



\# Battery



| Data | Unit |

|------|------|

| State of Charge | % |

| Current Battery Power | W |

| Battery Status | Charging / Discharging / Idle |

| Estimated Remaining Time | hh:mm |



\---



\# Self Sufficiency



| Data | Unit |

|------|------|

| Today | % |

| Month | % |

| Year | % |



\---



\# Costs



| Data | Unit |

|------|------|

| Estimated Daily Cost | € |

| Estimated Monthly Cost | € |

| Estimated Yearly Cost | € |



\---



\# Savings



| Data | Unit |

|------|------|

| Daily Savings | € |

| Monthly Savings | € |

| Yearly Savings | € |

| Savings Without PV Comparison | € |



\---



\# Statistics



| Data | Unit |

|------|------|

| Monthly History | Various |

| Yearly History | Various |

| Lifetime Statistics | Various |



\---



\# Forecasts



| Data | Unit |

|------|------|

| Expected Production Today | kWh |

| Expected Production Tomorrow | kWh |

| Monthly Forecast | kWh |



\---



\# Future Extensions



Additional categories may be introduced without breaking the existing model.



Examples:



\- EV Charging

\- Heat Pump

\- Dynamic Tariffs

\- Water Heating

\- Home Automation



\---



\# Design Rule



Dashboards must display these values.



Templates must calculate these values.



SQL must reconstruct these values.



Every component of HA Energy Suite speaks the same language.

