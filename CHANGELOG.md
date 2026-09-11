# Changelog

All notable changes to the **Singapore Weather & Outdoor Work Dashboard** are documented in this file.

---

## [2.5.0] - 2026-09-11

### Cause-Based Advisory Enhancement

#### Added

- Added a Cause-Based Outdoor Work Advisory.
- Added Primary Hazard identification.
- Added Measurement, Trigger, and Control information for the primary hazard.
- Added up to three Supporting Conditions.
- Added Affected Activities linked to the primary hazard.
- Added hazard-specific Operational Actions.
- Added Control Priority levels:
  - Immediate Action Required
  - High Attention Required
  - Controls Required
  - Routine Monitoring
  - Data Verification Required
- Added a Decision Basis section showing:
  - Selected region
  - Lightning observation count
  - WBGT
  - PSI
  - Forecast
  - Forecast area
- Added rule-based advisory content for:
  - Singapore lightning observations
  - Hazardous air quality
  - Very unhealthy air quality
  - Unhealthy air quality
  - High heat stress
  - Moderate heat stress
  - Rain detected
  - Rain, shower, or thunder forecast
  - Live data incomplete
  - No active hazard
- Added dynamic text escaping for forecast and area values inserted into the advisory.

#### Changed

- Updated the browser title to v2.5.0.
- Updated the visible version label to:

```text
Version 2.5.0 | Cause-Based Advisory Enhancement
```

- Changed the Outdoor Work Advisory card to a structured Cause-Based Outdoor Work Advisory.
- Changed the advisory from a generic action list to a prioritised explanation of hazard, trigger, affected work, actions, and decision basis.
- Changed the main lightning wording to reflect Singapore-wide observations rather than a region-specific distance.
- Retained the existing Red, Amber, Green, Unknown, Initialising, and Refreshing status framework.

#### Advisory priority

The advisory applies this general order:

1. Confirmed lightning observations
2. Hazardous air quality
3. Very unhealthy air quality
4. High heat stress
5. Live data incomplete
6. Moderate heat stress
7. Unhealthy air quality
8. Rain detected
9. Rain, shower, or thunder forecast
10. No active hazard

A confirmed Red hazard remains the primary condition when another data source is unavailable. The unavailable source may appear as a supporting condition.

#### Lightning scope

- Lightning remains based on the Singapore-wide observation count returned by the source feed.
- v2.5.0 does not claim that a lightning observation is within a defined distance of the selected region.
- The advisory directs users to check official site lightning alerts and procedures.

#### Retained from v2.4.2

- West, East, North, South, and Central selection
- Preferred-region browser storage
- Active Region display
- Regional PSI
- Regional forecast fallback lists
- Regional Temperature station selection
- Regional Humidity station selection
- Regional Rainfall station selection
- Station name, ID, distance, and region display
- Refresh Now control
- Seven-feed refresh progress
- Last dashboard refresh completed
- Last Successful Refresh
- Data Freshness
- Five-minute automatic refresh
- API request spacing
- Refresh lock protection
- Pending-refresh queue
- System Health
- Dashboard Health
- Live Data Incomplete handling
- Data Classification legend

#### Operational impact

- Users can identify the main active hazard.
- Users can see other conditions contributing to the operating state.
- Users can identify activities requiring review.
- Users receive actions matched to the primary hazard.
- Users can see the control priority.
- Users can review the readings used for the decision.
- The dashboard provides supporting information without replacing official alerts, risk assessments, or site procedures.

#### Validation completed

- JavaScript syntax check passed.
- v2.5.0 title and version check passed.
- Primary Hazard check passed.
- Supporting Conditions check passed.
- Affected Activities check passed.
- Operational Actions check passed.
- Control Priority check passed.
- Decision Basis check passed.
- Preferred-region persistence check passed.
- Regional station selection check passed.
- Seven-stage refresh check passed.
- Last-successful-refresh check passed.
- Refresh lock and pending queue check passed.
- Production test switches confirmed as `false`.
- No missing HTML IDs found.
- No duplicate HTML IDs found.
- Dynamic forecast and area escaping check passed.

---

## [2.4.2] - 2026-09-10

### Operational Readiness Enhancement

#### Added

- Added a Refresh Now button.
- Added seven-feed refresh-progress reporting.
- Added a Last Successful Refresh field.
- Added a separate Last Dashboard Refresh Completed field.
- Added Data Freshness states:
  - Fresh
  - Aging
  - Stale
  - No Successful Refresh
- Added browser storage for the last successful refresh timestamp.
- Added refresh completion messages for fully successful and degraded refreshes.

#### Refresh behaviour

- The Refresh Now button uses the same protected refresh path as the automatic refresh.
- Parallel refresh sequences are prevented.
- One pending refresh can be recorded.
- A degraded refresh updates the completion time but does not overwrite the last successful timestamp.

---

## [2.4.1] - 2026-09-09

### Operational Visibility Enhancement

#### Added

- Added an Active Region indicator.
- Added Dashboard Health badges.
- Added detailed System Health status text.
- Added a Forecast Area label.
- Added a footer Dashboard Status section.
- Added a Data Classification legend.
- Added a version tooltip.

#### Changed

- Reformatted regional station information.
- Changed the System Health display to a feed-and-status grid.
- Improved mobile presentation.

---

## [2.4.0] - 2026-09-09

### Regional Weather Station Selection

#### Added

- Added nearest-active-station selection for Air Temperature.
- Added nearest-active-station selection for Relative Humidity.
- Added nearest-active-station selection for Rainfall.
- Added representative points for West, East, North, South, and Central.
- Added station name, station ID, distance, and selected-region information.

#### Reliability

- Regional selection uses stations with coordinates and a current numeric reading.
- Each refresh captures the selected region before requesting regional feeds.
- Failed station selection produces an unavailable state rather than an unrelated reading.

---

## [2.3.0] - 2026-09-09

### Preferred Region Persistence

- Added preferred-region storage using `localStorage`.
- Added region validation.
- Added automatic restoration of the selector during page load.
- Added safe fallback to West.
- Added browser storage error handling.

---

## [2.2.5 Patch 2.1] - 2026-09-09

### Region Refresh State Completion Fix

- Added selected-region refresh state.
- Cleared previous regional PSI and forecast values during region changes.
- Added regional feed readiness handling.
- Expanded regional forecast fallback areas.

---

## [2.2.4] - 2026-09-09

### Refresh Lock Hardening

- Added `try/finally` protection to the refresh function.
- Ensured the refresh lock is released after unexpected errors.
- Preserved pending-refresh handling.

---

## [2.2.3] - 2026-09-09

### API Failure and Stale-State Protection

- Added failed metric cleanup.
- Added summary-value cleanup.
- Added Live Data Incomplete handling.
- Added Unknown Risk state.
- Prevented missing critical data from being treated as safe.

---

## [2.2.2] - 2026-09-09

### Forecast Mapping Protection

- Added ordered forecast-area fallbacks.
- Removed silent fallback to an unrelated forecast area.
- Added Mapping Unavailable handling.

---

## [2.2.1] - 2026-09-09

### Refresh Queue Enhancement

- Added one pending refresh request when a refresh is active.
- Reduced missed selected-region updates.

---

## [2.2.0] - 2026-09-09

### Lightning Operations Enhancement

- Added a lightning priority banner.
- Added blinking lightning icon and value.
- Added a Hazardous Air Quality banner.
- Aligned PSI card, Risk Matrix, and Overall thresholds.

---

## [2.1.0] - 2026-09-09

### Regional PSI and Forecast Foundation

- Added regional PSI retrieval.
- Added dynamic PSI labels.
- Added regional forecast mapping.
- Added lightning animation.
- Added the test-mode framework.

---

## [2.0.0] - 2026-09-09

### Singapore Multi-Zone Foundation

- Created the Singapore Weather & Outdoor Work Dashboard.
- Added West, East, North, South, and Central selection.

---

## Current Known Limitations

- Region reference points are representative points and not official boundaries.
- Nearest-station readings may not represent the entire selected region.
- Temperature, Humidity, and Rainfall can use different stations.
- Lightning observations are Singapore-wide and not selected by region.
- v2.5.0 does not calculate lightning distance from the selected region.
- WBGT is a national feed and is not selected by region.
- Forecasts are area-based and not exact-site forecasts.
- Preferred-region and successful-refresh storage are local to each browser and device.
- Clearing browser site data removes stored values.
- External API downtime or rate limits remain possible.
- Freshness is based on the last seven-feed browser success, not official source publication time.
- The Cause-Based Advisory is rule-based and does not replace a site risk assessment.
- No historical trend storage is included.
- No persistent operational event log is included.
- The dashboard is not an official warning system or system of record.

---

## Release Control Checklist

Before publishing:

1. Confirm the browser title and visible version label show v2.5.0.
2. Confirm all test switches are `false`.
3. Run a JavaScript syntax check.
4. Check for duplicate and missing HTML IDs.
5. Test all five regions.
6. Confirm Active Region follows the selector.
7. Confirm preferred region persists after reload.
8. Confirm Refresh Now is disabled during an active refresh.
9. Confirm progress moves through all seven feeds.
10. Confirm the Cause-Based Advisory displays a Primary Hazard.
11. Confirm Supporting Conditions appear when multiple conditions exist.
12. Confirm Affected Activities match the Primary Hazard.
13. Confirm Operational Actions match the Primary Hazard.
14. Confirm Control Priority is displayed.
15. Confirm Decision Basis displays the selected region and readings.
16. Confirm Last Successful Refresh and Freshness update correctly.
17. Confirm System Health shows all seven feeds.
18. Confirm no browser console errors appear.

---

## Author

Created by **Kelvin Siow**.
