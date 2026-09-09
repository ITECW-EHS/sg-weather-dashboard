# Changelog

All notable changes to the **Singapore Weather & Outdoor Work Dashboard** are documented in this file.

---

## [2.4.1] - 2026-09-09

### Operational Visibility Enhancement

#### Added

- Added an Active Region indicator below the Singapore clock.
- Added the Active Region to the footer Dashboard Status summary.
- Added coloured Dashboard Health badges:
  - Healthy
  - Degraded
  - Refreshing
  - Initialising
- Added detailed status text for each System Health data feed.
- Added a Forecast Area label above the selected forecast location.
- Added a footer Dashboard Status section.
- Added a Data Classification legend.
- Added a version tooltip describing the release scope.

#### Changed

- Updated the browser title to v2.4.1.
- Updated the visible version label to:

```text
Version 2.4.1 | Operational Visibility Enhancement
```

- Reformatted regional station information to show:
  - Station name
  - Station ID
  - Distance
  - Selected region
- Changed the System Health display from a basic list to a grid with feed name and status.
- Improved mobile presentation for Active Region, System Health, and Data Classification.

#### Retained

No weather-engine or safety-decision logic was intentionally changed in this release.

The following v2.4.0 functions remain in place:

- Preferred-region persistence
- Regional PSI
- Regional forecast-area selection
- Regional Temperature station selection
- Regional Humidity station selection
- Regional Rainfall station selection
- Lightning Priority Banner
- Advisory priority
- Risk Matrix thresholds
- Forecast fallback order
- Refresh queue
- Refresh lock protection
- API failure handling
- Live Data Incomplete protection
- Five-minute refresh cycle

#### Operational impact

- The selected region is clearer in screenshots and management views.
- System Health issues are easier to identify.
- Feed scope is visible without referring to supporting documentation.
- Station source information is easier to review.
- Release risk is limited because operational thresholds and API logic were not changed.

---

## [2.4.0] - 2026-09-09

### Regional Weather Station Selection

#### Added

- Added nearest-active-station selection for Air Temperature.
- Added nearest-active-station selection for Relative Humidity.
- Added nearest-active-station selection for Rainfall.
- Added representative reference points for West, East, North, South, and Central.
- Added station name, station ID, distance, and selected-region information.
- Added regional loading states for Temperature, Humidity, and Rainfall.

#### Changed

- Changed Temperature from the first returned reading to a selected regional station reading.
- Changed Humidity from the first returned reading to a selected regional station reading.
- Changed Rainfall from the first returned reading to a selected regional station reading.
- Expanded selected-region refresh handling to cover five regional feeds:
  - PSI
  - Forecast
  - Temperature
  - Humidity
  - Rainfall

#### Reliability

- Regional selection uses only stations with coordinates and a current numeric reading.
- Each refresh captures the selected region before requesting regional feeds.
- Failed regional station selection produces an unavailable state rather than an unrelated reading.

---

## [2.3.0] - 2026-09-09

### Preferred Region Persistence

#### Added

- Added preferred-region storage using `localStorage`.
- Added region validation.
- Added automatic restoration of the region selector during page load.
- Added safe fallback to West.
- Added browser storage error handling.

#### Fixed

- Removed an invalid `refreshZone` reference from the clock update function.
- Retained the valid region snapshot inside the controlled refresh function.

---

## [2.2.5 Patch 2.1] - 2026-09-09

### Region Refresh State Completion Fix

- Added selected-region refresh state.
- Cleared previous PSI and forecast values during region changes.
- Added regional feed readiness handling.
- Expanded regional forecast fallback areas.

---

## [2.2.4] - 2026-09-09

### Refresh Lock Hardening

- Added `try/finally` protection to the controlled refresh function.
- Ensured the refresh lock is released after unexpected errors.
- Preserved pending refresh handling.

---

## [2.2.3] - 2026-09-09

### API Failure and Stale-State Protection

- Added failed metric cleanup.
- Added summary-value cleanup.
- Added Live Data Incomplete handling.
- Added Unknown Risk state.
- Added grey data-integrity indicators.
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

- Added one pending refresh request when a refresh is already active.
- Reduced missed selected-region updates.

---

## [2.2.0] - 2026-09-09

### Lightning Operations Enhancement

- Added Lightning Priority Banner.
- Added blinking lightning icon and value.
- Added Hazardous Air Quality banner.
- Aligned PSI card, Risk Matrix, and overall risk thresholds.
- Added lightning-specific outdoor work controls.

---

## [2.1.0] - 2026-09-09

### Regional PSI and Forecast Foundation

- Added regional PSI retrieval.
- Added dynamic PSI labels.
- Added regional forecast mapping.
- Added lightning animation.
- Added test-mode framework.

---

## [2.0.0] - 2026-09-09

### Singapore Multi-Zone Foundation

- Created the Singapore Weather & Outdoor Work Dashboard.
- Added West, East, North, South, and Central selection.
- Retained the weather, advisory, Risk Matrix, and refresh foundation from the earlier site dashboard.

---

## Current Known Limitations

- Region reference points are representative points and not official boundaries.
- Nearest-station readings may not represent the entire selected region.
- Temperature, Humidity, and Rainfall can use different stations.
- Lightning observations are Singapore-wide and not selected by region.
- WBGT is a national feed and is not selected by region.
- Forecasts are area-based and not exact-site forecasts.
- Preferred-region storage is local to each browser and device.
- External API downtime or rate limits remain possible.
- No historical trend storage is included.
- No persistent operational event log is included.
- The dashboard is not an official system-of-record.

---

## Release Control Checklist

Before publishing:

1. Confirm the browser title and visible version label.
2. Confirm all test-mode switches are `false`.
3. Run a JavaScript syntax check.
4. Check for duplicate and missing HTML IDs.
5. Test all five regions.
6. Confirm Active Region follows the selector.
7. Confirm preferred region persists after reload.
8. Confirm System Health shows all seven feeds.
9. Confirm Dashboard Health displays the correct state badge.
10. Confirm footer Health and Active Region update.
11. Confirm Forecast Area displays.
12. Confirm no browser console errors appear.

---

## Author

Created by **Kelvin Siow**.
