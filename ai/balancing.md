---
status: stub
verified: none
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

## Planned sections

- The calibration method: what data sources are used and how values are derived.
- The relationship between pakset values and the engine's economic simulation.
- Vehicle operating costs, capacities, and weights.
- Infrastructure costs and maintenance.
- Historical price and wage data sources.

## Open questions

- What is the current, documented calibration method, and where does it live?
- Which engine fields must a balancing change touch together to stay coherent?
