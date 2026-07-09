# Changelog — PVPerformance fork of HA-Energy-Suite

Fork of [energy-control-center](https://github.com/xbebo83x/HA-Energy-Suite/blob/main/cards/energy-control-center/energy-control.yaml)  
Original author: [@xbebo83x](https://github.com/xbebo83x)

---

## What changed and why

This fork extends the original card in two directions:

1. **Portability** — all entity IDs and economic parameters can now be configured at runtime via a settings UI, without editing the YAML file. The card ships with Solarman inverter defaults but works with any inverter that has equivalent sensors.

2. **Operational context** — the decision panel now surfaces the Smart Energy Manager state (auto/manual, EMS mode, charge current, time-to-full) alongside the convenience score, turning the card into a live SEM dashboard rather than just a score display.

---

## New features

### Settings overlay (⚙️ button)

A full-screen modal overlay with two tabs:

- **Parametri tab** — interactive sliders for all 17 thresholds and score weights. Changes call `input_number.set_value` via the HA WebSocket API immediately. Sliders show the live value and a "default X" badge when the `input_number` entity is missing from HA (graceful degradation).
- **Entità HA tab** — text fields to override every entity ID the card reads. Grouped into three pill sub-tabs: Inverter · Forecast · Statistiche. Each field shows a live green/yellow badge with the current entity state. Values persist across HA restarts via `localStorage('pv_entities_v1')`. A **Reset** button clears all overrides back to defaults.
- **💾 Salva button** in the modal header (cross-tab): saves all entity ID fields to localStorage in one action.
- **Floating tooltips** on each parameter section explaining the scoring logic. Rendered appended to `document.body` to escape `overflow:hidden` clipping.
- **Embedded YAML snippet** (`pvYamlStr`) with the full `input_number` configuration block ready to paste into `configuration.yaml`.

### Configurable thresholds via `input_number`

All scoring thresholds previously hardcoded are now read from HA `input_number` entities with fallback to the original values:

| `input_number` entity | Default | Description |
|---|---|---|
| `fv_surplus_alto_w` | 1800 W | High surplus threshold (+35 conv pts) |
| `fv_surplus_medio_w` | 800 W | Medium surplus (+25 pts) |
| `fv_surplus_basso_w` | 200 W | Low surplus (+15 pts) |
| `fv_soglia_utile_w` | 300 W | Min FV power for useful window calc |
| `fv_soglia_sera_kwh` | 1 kWh | Evening threshold (remaining forecast) |
| `fv_trend_up_ratio` | 1.20 | pot_1h / pv_now ratio → rising trend |
| `fv_trend_down_ratio` | 0.75 | pot_1h / pv_now ratio → falling trend |
| `batt_soglia_alta` | 85 % | Battery high (+15 pts) |
| `batt_soglia_media` | 65 % | Battery medium (+8 pts) |
| `batt_soglia_bassa` | 35 % | Battery low (−15 pts) |
| `batt_sera_buona` | 70 % | Evening label "Buona" |
| `batt_sera_discreta` | 40 % | Evening label "Discreta" |
| `score_peso_forecast` | 0.25 | Score weight: forecast reached % |
| `score_peso_auts_oggi` | 0.25 | Score weight: self-sufficiency today |
| `score_peso_auts_mese` | 0.25 | Score weight: self-sufficiency month |
| `score_peso_batteria` | 0.20 | Score weight: battery SOC |
| `score_bonus_max` | 5 | Bonus points if daily import < 1 kWh |

### Economic parameters via `input_number`

| `input_number` entity | Default | Description |
|---|---|---|
| `costo_kwh_reale` | 0.25 EUR | Cost per kWh purchased |
| `quota_fissa_giornaliera_corrente` | 0 EUR | Daily fixed charge (pro-rated to month) |
| `fv_valore_ssp_kwh` | 0.15 EUR | SSP value per exported kWh |

The fixed monthly cost is now split into:
- **Daily fixed charge × days in month** (from `input_number`, covers standing charge)
- **Canone TV** (configurable numeric field in the Entità HA tab, default 18 EUR — matches original `quotaFissaMese`)

This models real Italian electricity bills more accurately, where the fixed component is billed per day.

### Smart Energy Manager panel

The right-side decision panel has been redesigned to show SEM operational state:

- Dynamic icon: 🤖 green when automation is `on`, ✋ amber when manual
- Status line: SEM state text + contextual info (time-to-full if charging, otherwise EMS mode + max charge current)
- Convenience score bar moved below separator with decision label as text
- Requires 5 additional Solarman-specific entities (see entity mapping section); degrades gracefully with "Sconosciuto" if absent

### Dynamic colors on status mini-cards

Battery, house load, and grid mini-cards now have a dynamic top border and text color:
- Battery: green > `batt_soglia_alta`, yellow > `batt_soglia_bassa`, red otherwise
- House load: amber if FV surplus > 0, red otherwise
- Grid: red on import, violet on export, blue when balanced

### Dynamic year in monthly statistics

Monthly sensor IDs now use `new Date().getFullYear()` instead of the hardcoded `2026`. The card automatically rolls over each January 1st without any file edits.

### Animated progress bars

`transition: width 0.6s ease` added to the production bar, convenience bar, and FV window bar. Values animate smoothly on each re-render instead of jumping.

---

## Modified behaviour

### Entity ID defaults changed (Solarman inverter)

The fork ships with Solarman inverter entity ID defaults instead of the generic `inverter_*` entities of the original. All can be overridden via the Entità HA settings tab.

| Variable | Original default | Fork default |
|---|---|---|
| `pv` | `sensor.inverter_pv_power` | `sensor.solarman_pv_power_w` |
| `casa` | `sensor.inverter_load_l1_power` | `sensor.pow_generale_power` |
| `reteCt` | `sensor.inverter_internal_ct1_power` | `sensor.solarman_power_from_grid` |
| `batt` | `sensor.inverter_battery` | `sensor.solarman_battery_soc` |
| `prodOggi` | `sensor.inverter_today_production` ÷ 1000 | `sensor.solarman_pv_etoday` (already kWh) |
| `importOggiWh` | `sensor.inverter_today_energy_import` (Wh) | `sensor.solarman_etoday_received_from_grid` × 1000 |

### Score badge: dynamic gradient border

The performance score badge in the header now uses a CSS `linear-gradient` border (`135deg, ${colore}, #ffca28, #42a5f5`) instead of a static green border. The gradient reflects the current performance state.

### `tap_action` / `hold_action` set to `none`

Prevents accidental HA navigation events when interacting with sliders and inputs inside the card.

### Container query instead of media query for responsive layout

`@container (max-width: 1200px)` replaces `@media (max-width: 1200px)`. The layout adapts to the card's own container width rather than the viewport, making it more reliable when placed in sidebars or multi-column dashboards.

### `prod-line` font size increased

`40px` → `52px` for the main kWh production figure, for better readability at a glance.

### `.ecc-wrap` fourth row

`grid-template-rows` fourth value changed from `180px` to `1fr` — the bottom row now fills available space instead of having a fixed height.

---

## Prerequisites

To use all features, add the following `input_number` entities to `configuration.yaml`. The card functions without them (all values fall back to hardcoded defaults), but sliders in the Parametri tab will show "default X" badges.

The full YAML block is embedded in the card itself — open the settings overlay, navigate to Parametri, and the `pvYamlStr` variable contains the ready-to-paste configuration.

---

## Breaking changes for existing users of the original card

| Change | Impact |
|---|---|
| Entity ID defaults changed to Solarman | Must override via Entità HA tab if using a different inverter |
| `input_number` entities required for full functionality | Without them the card uses hardcoded defaults — no errors, but sliders are non-functional |
| SEM panel requires 5 Solarman-specific entities | Without them the SEM section shows "Sconosciuto" / empty values |
| `quotaFissaMese` replaced by two-component cost model | If you were relying on the hardcoded 18 EUR, set Canone TV = 18 in the Entità HA tab (it defaults to 18 automatically) |
