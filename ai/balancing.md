---
status: draft
verified: New master @ c842afdbd
---
# Balancing

**Covers**: prices, costs, capacities, speeds, and intro/retire dates, and how they are chosen to
be economically and historically realistic.

## Notes

- Balancing is a stated long-term priority, and the ex-15 engine work is critical for balancing
  to work ([../../AGENTS.md](../../AGENTS.md)). Read this doc before tuning any value, and read
  [high-level-design-goals](high-level-design-goals.md) first.
- The main source of pricing information is the forum thread "A snippet of relative pricing
  information": https://forum.simutrans.com/index.php/topic,6521.0.html
   `[FORUM:https://forum.simutrans.com/index.php/topic,6521.0.html]`. It collects historical British
   transport costs and prices, including vehicle purchase prices and related data.

## Cost balancing project

- Forum thread "Cost balancing - the great project" on the Pak128.Britain-Ex board, started
  January 2022: https://forum.simutrans.com/index.php/topic,21310.0.html
  `[FORUM:https://forum.simutrans.com/index.php/topic,21310.0.html]`. It records the calibration
  method and the interim findings.
- Calibration: all figures are normalised to the year 1900. General inflation uses the Bank of
  England inflation calculator; labour costs use measuringworth, which separates average
  earnings. The SimuCent to GBP conversion comes from passenger revenue: the `.dat` figure of
  0.50 cents per kilometre (second fare stage) represents 1d per mile, the third-class maximum
  prescribed by the Regulation of the Railways Act 1844. Per-kilometre costs use the short
  timescale and capital or annual costs use the long timescale; the day counts as 16 active
  hours. `[FORUM:https://forum.simutrans.com/index.php/topic,21310.0.html]`
- Interim findings: infrastructure capital and maintenance costs are broadly realistic except
  that bridges are far too cheap and the rail forge cost is too high; operating costs are too
  low relative to revenue; passenger revenue is possibly overstated, with roughly halved fares
  proposed for the 1900 calibration. `[FORUM:https://forum.simutrans.com/index.php/topic,21310.0.html]`
- Interim stance: where simulating features do not yet exist (inflation, vehicle wear and
  overhauls), balance errs on the side of being generous to the player, with more detail added
  as the feature set permits. `[FORUM:https://forum.simutrans.com/index.php/topic,21310.0.html]`
- Much of the full balancing work described in the thread is still in the future for the ex-15
  engine version. `[RECOLLECTION:2026-09-19]`
- The vehicle cost balancing in the project takes effect only after ex-15 with its inflation
  feature; without year-indexed price adjustment, the calibrated vehicle figures cannot apply.
  `[RECOLLECTION:2026-09-19]`

## Inflation recording (ex-15)

- Engine mechanism: `karte_t::get_inflation_adjusted_price` multiplies a base `.dat` price by a
  year-indexed factor: adjusted price equals base price times index divided by 100, so an index
  of 100 leaves prices unchanged. Between listed years the index is linearly interpolated; past
  the last year the last index applies, before the first year the first index applies. Where a
  price type has no table, the `general` table is used. With the timeline off, base prices are
  returned unadjusted. `[CODE simutrans-extended ex-15 @ d4893f3]`
- Pakset record: `config/prices.tab` in the pakset directory. It holds one line per price type
  with year and index pairs in increasing year order. The engine loads it in `prices_init` and
  reports ill-formed lines, falling back to defaults for that type.
  `[CODE simutrans-extended ex-15 @ d4893f3]`
- Price type keys, 12 in total: `general`, `passenger fare`, `mail rate`, `goods rate`,
  `vehicle purchase`, `vehicle maintenance`, `buildings`, `infrastructure`, `city land`,
  `country land`, `corporation tax`, `base rate`.
  `[CODE simutrans-extended ex-15 @ d4893f3]`
- Coverage: vehicle purchase, running, fixed and upgrade costs; passenger, mail and goods fares;
  way, bridge, tunnel, signal, roadsign and way-object construction and maintenance; buildings,
  depots and stations; the `cst_*` settings; corporation tax; land values; and overdraft
  interest via `base rate`. `[CODE simutrans-extended ex-15 @ d4893f3]`
- Savegames: the price tables are stored in saves on extended version 15 and above, and the
  pakset-directory file is re-read on load. `[CODE simutrans-extended ex-15 @ d4893f3]`
- Fuel and staff sit outside this file: absolute yearly prices per fuel and engine type live in
  `fuel.tab`, and yearly wages per staff type in `staff.tab`.
  `[CODE simutrans-extended ex-15 @ d4893f3]`
- No in-game display currently reads these tables; the planned display of price factors over
  time is outstanding.
  `[FORUM:https://forum.simutrans.com/index.php/topic,22054.msg202141.html]`
- Pakset status: `New/config/` contains no `prices.tab`, `fuel.tab`, or `staff.tab`; authoring
  them is outstanding pakset work for ex-15. `[CODE New master @ c842afdbd]`

## Calibration working papers

- `New/` contains calibration spreadsheets used as working papers for balancing decisions. They
  are inputs, not canonical values; the canonical values live in the `.dat` files.
  `[CODE New master @ c842afdbd]`
- Vehicle purchase prices and operating physics: `Vehicle cost table.ods`,
  `Horses cost table.ods`, `steam-physics-calcs.ods`, `road-vehicle-physics-calibration.ods`,
  `Rolling resistance calcs.ods`, `Multiple unit TE extrapolation.ods`, `Track weights.ods`.
  `[CODE New master @ c842afdbd]`
- Interim vehicle balance: `Pak128 Britain - mod.xlsx` is reported to be the interim balancing
  spreadsheet for vehicles, attributed to neroden. `[RECOLLECTION:2026-09-19]`
- Passenger capacity and comfort: `Comfort calibration overview.ods` (sheets `Overview` and
  `All vehicles`), `Exp-Cater-Comfort-Capacity.ods`, `Passenger density calculations.ods`,
  `payload-tonnage-calcs.ods`, `stagecoach-passenger-calcs.ods`.
  `[CODE New master @ c842afdbd]`
- Infrastructure costs: `Infrastructure balancing calibration.ods`,
  `Infrastructure balancing calibration-2.ods` (calculation spreadsheet behind the thread tables;
  sheets include currency conversion, historical and Simutrans infrastructure costs, historical
  and Simutrans vehicles, wages, passenger fares, revenue ratios, and fuel price normalisation;
  one sheet links to the `Extrapolation` sheet of `steam-physics-calcs.ods`),
  `bridges-new.xls`,
  `road-bridges.xls`, `Tunnel cost research (PJMack).ods`, `ways-rail-balance-v1.ods`,
  `Wear calculations.ods`, `road-vehicle-wear-calcs.ods`. `[CODE New master @ c842afdbd]`
- Steam locomotive physics: `steam-physics-calcs.ods` (sheets `Hill (AEO)`, `Hill (Hood)`,
  `Extrapolation`, `Theoretical figures`). `[CODE New master @ c842afdbd]`
- Demand and wider economy: `Agricultural output calibration.ods`,
  `Population growth extrapolation.ods`, `Congestion index.ods`, `balancing.xls`,
  `new-balancing.xls`, `Simutrans Ship Balance.xlsx`. `[CODE New master @ c842afdbd]`
- The relationship between these working papers and the engine's economic simulation is not
  yet documented; see the open questions below.

## Planned sections

- The calibration method: what data sources are used and how values are derived.
- The relationship between pakset values and the engine's economic simulation.
- Vehicle operating costs, capacities, and weights.
- Infrastructure costs and maintenance.
- Historical price and wage data sources.

## Open questions

- What is the current, documented calibration method, and where does it live?
- Which engine fields must a balancing change touch together to stay coherent?
- Who authored `Pak128 Britain - mod.xlsx` and which vehicle classes does its interim balance
  cover?
- What yearly factors should `New/config/prices.tab` record per price type, and from which
  historical sources?
