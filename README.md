# Singapore Weather & Outdoor Work Dashboard

**Version 2.4.1 | Operational Visibility Enhancement**

A browser-based weather and outdoor-work decision-support dashboard covering five Singapore regions.

The dashboard combines regional PSI and forecast information, nearest-active-station weather readings, lightning observations, operational advisories, risk status, system health, and a saved preferred region.

## Live Dashboard

Add the published GitHub Pages address here:

```text
https://YOUR-GITHUB-USERNAME.github.io/sg-weather-dashboard/
```

Replace `YOUR-GITHUB-USERNAME` with the repository owner's GitHub username.

## Current Release

```text
Version: 2.4.1
Release: Operational Visibility Enhancement
```

v2.4.1 is a display and usability update built on the v2.4.0 weather engine. It does not change API endpoints, risk thresholds, advisory priority, regional station selection, forecast mapping, or refresh logic.

## Main Features

### Region Selection

Users can select:

- West
- East
- North
- South
- Central

The selected region controls:

- 24-hour PSI
- PSI labels and status
- 2-hour forecast area
- Air Temperature station selection
- Relative Humidity station selection
- Rainfall station selection

### Preferred Region

The selected region is stored in the browser using `localStorage`.

- The selected region remains after page refresh.
- The selected region is restored when the dashboard is reopened in the same browser.
- Invalid stored values default to West.
- Browser storage errors do not stop the dashboard.

The preference is specific to the browser, device, and dashboard address.

### Active Region Indicator

The current region is displayed below the Singapore clock and in the footer status summary.

Example:

```text
ACTIVE REGION
NORTH
```

### Regional Weather Station Selection

Air Temperature, Relative Humidity, and Rainfall use the nearest available active station to a representative point for the selected region.

Each card displays:

```text
Station: [station name]
ID: [station ID]
Distance: [distance]
Region: [selected region]
```

Different metrics may use different stations because station availability differs between datasets.

### Regional Forecast Fallbacks

The dashboard checks forecast areas in a defined order.

```javascript
const FORECAST_FALLBACKS = {
    west: [
        "Choa Chu Kang",
        "Tengah",
        "Bukit Batok",
        "Bukit Panjang",
        "Jurong East",
        "Jurong West",
        "Clementi"
    ],
    east: [
        "Changi",
        "Tampines",
        "Pasir Ris",
        "Bedok",
        "Paya Lebar",
        "Marine Parade"
    ],
    north: [
        "Woodlands",
        "Yishun",
        "Sembawang",
        "Mandai",
        "Sungei Kadut",
        "Seletar"
    ],
    south: [
        "Sentosa",
        "Bukit Merah",
        "Queenstown",
        "Southern Islands",
        "Kallang"
    ],
    central: [
        "City",
        "Novena",
        "Toa Payoh",
        "Bishan",
        "Bukit Timah",
        "Tanglin",
        "Central Water Catchment"
    ]
};
```

If no configured area is returned, the dashboard shows a mapping unavailable state instead of an unrelated forecast.

## Dashboard Information

The dashboard displays:

- Wet Bulb Globe Temperature, or WBGT
- Lightning observations
- Regional 24-hour PSI
- Regional Air Temperature station reading
- Regional Relative Humidity station reading
- Regional Rainfall station reading
- Regional 2-hour forecast
- Outdoor Work Advisory
- Risk Matrix
- System Health
- Dashboard Health
- Last and next refresh times

## Operational Visibility Features

### Dashboard Health Badges

The Dashboard Health panel uses these indicators:

```text
🟢 HEALTHY
🟠 DEGRADED
🔄 REFRESHING
🔵 INITIALISING
```

### System Health Detail

Each data feed shows an icon and status label.

Possible states include:

- OK
- Loading
- Rate Limited
- Mapping Unavailable
- Unavailable

Example:

```text
✅ WBGT          OK
✅ Lightning     OK
⚠ Temperature   RATE LIMITED
```

### Forecast Area Label

The forecast card identifies the selected forecast area.

```text
Forecast Area
Woodlands
```

### Footer Status Summary

The footer shows:

- Dashboard Health
- Active Region

### Data Classification Legend

The dashboard explains the scope of each feed:

- WBGT: National feed
- Lightning: Singapore-wide observations
- PSI: Regional
- Forecast: Regional area
- Temperature: Regional station
- Humidity: Regional station
- Rainfall: Regional station

## Risk Matrix

The Risk Matrix evaluates:

- Heat stress
- Lightning
- Air quality
- Weather
- Overall condition

Overall states include:

- Red
- Amber
- Green
- Unknown
- Refreshing

Missing critical data is not treated as safe.

## Advisory Priority

The banner and advisory use this priority:

1. Lightning detected
2. Hazardous air quality
3. Live data incomplete
4. Red risk condition
5. Amber risk condition
6. Green condition

### PSI Categories

- Above 300: Hazardous
- Above 200: Very Unhealthy
- Above 100: Unhealthy
- 100 or below: Good / Moderate

### Lightning Alert

When lightning observations are returned:

- The lightning icon blinks.
- The lightning value blinks.
- The banner flashes red.
- The advisory instructs users to suspend exposed activities and move to shelter.

## Reliability Controls

The dashboard includes:

- Five-minute refresh cycle
- Delay between API requests
- Refresh lock protection using `try` and `finally`
- One pending refresh queue
- Consistent selected-region snapshot during a refresh
- Regional refresh loading state
- Forecast fallback protection
- Failed API state cleanup
- Stale-value prevention
- Live Data Incomplete protection
- Preferred-region validation
- Browser storage error handling

## Data Sources

The dashboard retrieves live information through Data.gov.sg endpoints for:

- WBGT
- Lightning
- PSI
- 2-hour forecast
- Air Temperature
- Relative Humidity
- Rainfall

## Repository Structure

```text
sg-weather-dashboard/
├── index.html
├── README.md
└── CHANGELOG.md
```

The dashboard uses one HTML file containing its HTML, CSS, and JavaScript.

## GitHub Pages Deployment

1. Keep a backup of the current production `index.html`.
2. Rename `index_v2.4.1.html` to `index.html`.
3. Upload `index.html`, `README.md`, and `CHANGELOG.md` to the repository root.
4. Commit the files to the `main` branch.
5. Confirm GitHub Pages deploys from `main` and `/ (root)`.
6. Open the published dashboard.
7. Perform the production checks below.

## Production Checks

Before deployment, confirm:

```javascript
const TEST_MODE = {
    LIGHTNING: false,
    PSI: false,
    WBGT: false,
    RAINFALL: false
};
```

After deployment:

1. Confirm the browser title shows v2.4.1.
2. Confirm the version label shows Operational Visibility Enhancement.
3. Confirm the Active Region matches the selector.
4. Test West, East, North, South, and Central.
5. Confirm PSI and forecast match the selected region.
6. Confirm Temperature, Humidity, and Rainfall show station details.
7. Confirm System Health shows status text for all seven feeds.
8. Confirm Dashboard Health shows the correct colour badge.
9. Confirm the footer Health and Active Region update.
10. Refresh the browser and confirm the preferred region remains selected.
11. Confirm there are no browser console errors.

## Known Limitations

- Region reference points are internal representative points, not official administrative or meteorological boundaries.
- The nearest active station may not represent all conditions across a region.
- Temperature, Humidity, and Rainfall may use different stations.
- Station selection can change when a nearer station is unavailable.
- Lightning observations are Singapore-wide and are not filtered by selected region.
- WBGT is presented as a national feed and is not selected by region.
- Forecast information is area-based rather than site-specific.
- Preferred-region storage does not transfer between browsers or devices.
- Clearing browser site data can remove the saved preference.
- External API rate limiting or downtime can produce API Busy or Unavailable states.
- The dashboard does not store historical trends or operational event logs.
- The dashboard is not an official system-of-record.
- The dashboard does not replace official alerts, risk assessments, site procedures, or supervisor decisions.

## Version History

### v2.4.1

Operational Visibility Enhancement:

- Added Active Region indicator.
- Added coloured Dashboard Health badges.
- Added detailed System Health statuses.
- Improved station source formatting.
- Added Forecast Area label.
- Added footer Dashboard Status.
- Added Data Classification legend.
- Added version tooltip.
- Retained v2.4.0 weather and safety logic.

### v2.4.0

Regional Weather Station Selection:

- Added regional Air Temperature station selection.
- Added regional Relative Humidity station selection.
- Added regional Rainfall station selection.
- Added station name, ID, distance, and region display.
- Expanded the regional refresh state.

### v2.3.0

- Added preferred-region persistence.
- Added saved-region validation.
- Restored the saved region on page load.

### v2.2.x

- Added Lightning Priority Banner.
- Added forecast mapping protection.
- Added refresh queue and refresh-lock protection.
- Added API failure and stale-state protection.
- Added Live Data Incomplete handling.
- Aligned PSI and Risk Matrix thresholds.

### v2.1.0

- Added regional PSI.
- Added regional forecast mapping.
- Added lightning alert animation and test-mode framework.

### v2.0.0

- Created the Singapore multi-zone dashboard.

## Author

Created by **Kelvin Siow**.

## Disclaimer

This dashboard is for decision support only. Verify conditions using official information and apply approved workplace safety, emergency, and operational procedures before work starts or continues.
