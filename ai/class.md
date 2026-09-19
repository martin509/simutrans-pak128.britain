---
status: draft
verified: New master @ eff439751
---
# Classes

**Covers**: passenger and mail classes, vehicle accommodation classes, and how comfort,
catering and travelling post offices modify revenue.

## Passenger classes

- Passengers generate with a wealth class, 5 levels: `p_class[0]` Very low, `p_class[1]` Low,
  `p_class[2]` Medium, `p_class[3]` High, `p_class[4]` Very high, named in `New/text/en.tab`.
  `[CODE New master @ eff439751]`
- Different buildings generate and demand different proportions of each class. Lower-class
  passengers cannot afford high prices; each class travels on the lowest-journey-time route
  available at prices it can pay. `[FORUM:https://forum.simutrans.com/index.php/topic,1959.0.html]`
- Per-class fares use the `p_fare[i]` keys in `New/text/en.tab`.
  `[CODE New master @ eff439751]`

## Mail classes

- Mail has 2 classes: `m_class[0]` Normal and `m_class[1]` Priority, with matching
  `m_accommodation[i]` and `m_fare[i]` keys in `New/text/en.tab`.
  `[CODE New master @ eff439751]`

## Accommodation

- Vehicles declare capacity and comfort per class index: `payload[i]` and `comfort[i]`, for
  example `New/trains/4wheel-1850s-first.dat` carries `payload[3]=18` with `comfort[3]=69`,
  and later stock such as `New/trains/br-251.dat` uses index 4.
  `[CODE New master @ eff439751]`
- A comfort rating is the maximum comfortable journey time for that accommodation. Revenue
  falls when comfort is below the passengers' tolerance; above tolerance a luxury bonus
  applies. Passengers in overcrowded vehicles count comfort as 10 for revenue purposes, or
  lower where the base rating is 10 or below.
  `[FORUM:https://forum.simutrans.com/index.php/topic,1959.0.html]`
- Upgrade willingness: passengers who can afford higher-class accommodation on the same convoy
  pay for it only where the extra comfort is worthwhile, randomised per passenger between the
  lower accommodation's maximum comfortable journey time and
  `max_comfort_preference_percentage = 650` percent of it.
  `[CODE New master @ eff439751]`

## Comfort and revenue

- Tolerable comfort ratings by journey time in `New/config/simuconf.tab`: 10 for up to 5
  minutes, 50 for up to 60, 125 for up to 150, 165 for up to 360, 250 for 1440 and above,
  with scaled proportions between. Revenue impact is strongest at long journey times.
  `[CODE New master @ eff439751]`
- The discomfort penalty is calibrated higher than the luxury bonus:
  `max_discomfort_penalty_differential = 220` with `max_discomfort_penalty_percent = 25`.
  `[CODE New master @ eff439751]`

## Catering and travelling post offices

- Catering levels on longer journeys earn extra revenue per passenger: no revenue below
  `catering_min_minutes = 45`; level maxima of 160 from 60 minutes, 390 from 90, 830 from
  120, 1600 from 180, and 4400 from 210, with scaled proportions between levels. Catering
  vehicles also add a small comfort increase. `[CODE New master @ eff439751]`
- Vehicles declare catering with `catering_level`, for example `catering_level=1` on early
  carriages and `catering_level=3` on `New/trains/br-123.dat`. `[CODE New master @ eff439751]`
- Travelling post offices earn `tpo_revenue = 300` per mail bag carried on trips above
  `tpo_min_minutes = 90`. `[CODE New master @ eff439751]`

## Open questions

- Which fare-stage figures currently apply per class, and where are they recorded?
