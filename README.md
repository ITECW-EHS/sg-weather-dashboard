# Singapore Weather & Outdoor Work Dashboard

**Version 2.3.0 | Preferred Zone Persistence**

A browser-based dashboard for monitoring weather conditions and supporting outdoor work decisions across Singapore.

The dashboard provides multi-zone PSI and forecast selection, weather readings, lightning observations, operational advisories, risk status, API health monitoring, and saved zone preferences.

## Live Dashboard

Add the published GitHub Pages link here:

```text
https://YOUR-GITHUB-USERNAME.github.io/sg-weather-dashboard/
```

Replace `YOUR-GITHUB-USERNAME` with the repository owner's GitHub username.

## Current Release

```text
Version 2.3.0
Release: Preferred Zone Persistence and Refresh State Fix
```

## Main Features

### Singapore Zone Selection

Users can select one of five Singapore zones:

- West
- East
- North
- South
- Central

The selected zone controls:

- 24-hour PSI display
- PSI labels and risk status
- 2-hour forecast area selection
- Regional refresh state

### Preferred Zone Persistence

The dashboard saves the selected zone in the browser using `localStorage`.

After a user selects a zone:

- The preference is saved automatically.
- The same zone is restored after a page refresh.
- The same zone is restored when the dashboard is reopened in the same browser.
- Invalid saved values default to West.
- Storage access failures do not stop the dashboard.

The saved preference is specific to the browser, device, and dashboard address.

### Regional Forecast Fallbacks

The dashboard uses ordered fallback areas for each zone.

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

The first available area in the configured order is used. If no mapped area is returned, the dashboard displays a mapping unavailable status instead of using an unrelated forecast area.

## Weather and Safety Information

The dashboard displays:

- Wet Bulb Globe Temperature, or WBGT
- Lightning observations
- 24-hour PSI by selected zone
- Air temperature
- Relative humidity
- 5-minute rainfall
- 2-hour forecast by selected zone
- Outdoor work advisory
- Risk Matrix
- System Health
- Dashboard Health Summary

## Risk Matrix

The Risk Matrix evaluates:

- Heat stress
- Lightning
- Air quality
- Weather
- Overall condition

The dashboard uses these overall states:

- `RED`
- `AMBER`
- `GREEN`
- `UNKNOWN`
- `REFRESHING`

Missing critical data is not treated as safe. When critical live data is unavailable, the dashboard displays:

```text
LIVE DATA INCOMPLETE
```

## Advisory Priority

The dashboard applies the following display priority:

1. Lightning detected
2. Hazardous air quality
3. Live data incomplete
4. Red risk condition
5. Amber risk condition
6. Green condition

### Lightning Alert

When lightning observations are returned:

- The lightning icon blinks.
- The lightning value blinks.
- The main banner flashes red.
- The outdoor work advisory changes to lightning controls.

### PSI Status

The PSI card and Risk Matrix use these categories:

- Above 300: Hazardous
- Above 200: Very Unhealthy
- Above 100: Unhealthy
- 100 or below: Good / Moderate

### Outdoor Work Advisory

The advisory card provides controls based on the current dashboard state, including:

- Suspension of roof, open-field, outdoor sport, and event activities during lightning observations
- Review of outdoor work and work-at-height activities during red conditions
- Hydration, rest, shelter, and monitoring controls during amber conditions
- Data verification and approved procedure requirements when live data is incomplete

## System Health

The System Health panel shows the status of these data feeds:

- WBGT
- Lightning
- PSI
- Forecast
- Temperature
- Humidity
- Rainfall

Possible API states include:

- Loading
- OK
- Rate limited
- Mapping unavailable
- Unavailable

The Dashboard Health Summary reports:

- Number of available data sources
- Refresh state
- Last dashboard refresh

## Reliability Controls

Version 2.3.0 includes:

- Controlled five-minute refresh cycle
- Delay between API requests
- Pending refresh queue
- Region refresh state
- Refresh lock protection using `try` and `finally`
- Regional PSI and forecast snapshot during each refresh
- Failed API cleanup
- Stale-state prevention
- Forecast mapping protection
- Unknown risk-state handling
- Saved-zone validation
- Local storage error handling

## Data Sources

The dashboard retrieves live datasets through Data.gov.sg endpoints for:

- WBGT
- Lightning
- PSI
- 2-hour forecast
- Air temperature
- Relative humidity
- Rainfall

The dashboard is a decision-support display. Users must apply approved site procedures, lightning alerts, risk assessments, and supervisor instructions before starting or continuing outdoor work.

## Repository Structure

```text
sg-weather-dashboard/
├── index.html
└── README.md
```

The current release uses a single-file dashboard. HTML, CSS, and JavaScript are contained in `index.html`.

## GitHub Pages Deployment

1. Upload `index.html` and `README.md` to the repository root.
2. Open the repository **Settings**.
3. Open **Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select the `main` branch.
6. Select the `/ (root)` folder.
7. Save the settings.
8. Open the published GitHub Pages address after deployment completes.

## Updating the Dashboard

For each release:

1. Keep a backup of the previous `index.html`.
2. Replace the repository root `index.html` with the tested version.
3. Update the browser title, dashboard version label, release header, and README.
4. Confirm all test switches are set to `false`.
5. Commit the changes with the release version.
6. Test the live GitHub Pages site.

Suggested v2.3.0 commit message:

```text
v2.3.0 Preferred Zone Persistence

- Added saved zone preference
- Added zone validation
- Restored saved zone during page load
- Fixed region refresh state reference
- Retained regional PSI and forecast safeguards
```

## Production Check

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

1. Select a zone other than West.
2. Allow the regional refresh to complete.
3. Refresh the browser.
4. Confirm the selected zone remains active.
5. Confirm the PSI label matches the zone.
6. Confirm the forecast area belongs to the selected zone's fallback list.
7. Confirm the System Health panel updates.
8. Confirm there are no browser console errors.

## Monitoring Checklist

Monitor the dashboard for:

- Zone preference restoration
- Region switching response
- PSI and forecast consistency
- Forecast mapping unavailable messages
- API Busy or Unavailable states
- Lightning banner activation and clearing
- Live Data Incomplete handling
- Five-minute refresh continuity
- Browser console errors

## Browser Storage Note

The preferred zone is stored locally in the user's browser. The preference does not automatically transfer between:

- Different browsers
- Different devices
- Private or incognito sessions
- Different dashboard URLs

Clearing browser site data may remove the saved zone preference.

## Version History

### v2.3.0

**Preferred Zone Persistence**

Added:

- Saved zone preference using browser local storage
- Zone validation and West fallback
- Saved selector restoration during page load
- Local storage error handling

Fixed:

- Removed an invalid `refreshZone` reference from the clock update function
- Retained the valid refresh-zone snapshot inside the controlled refresh function

### v2.2.5 Patch 2.1

**Region Refresh State Completion Fix**

- Added selected-region refresh state
- Cleared previous regional PSI and forecast values during a zone change
- Added regional feed readiness handling
- Added expanded forecast fallback areas

### v2.2.4

**Reliability Hardening**

- Added refresh lock protection using `try` and `finally`
- Preserved pending refresh handling

### v2.2.3

**API Failure and Stale-State Protection**

- Cleared failed metric values
- Cleared stale internal values
- Added Live Data Incomplete handling
- Added grey risk indicators for unknown data

### v2.2.2

**Forecast Mapping Protection**

- Added ordered regional forecast fallbacks
- Prevented silent fallback to an unrelated forecast area

### v2.2.1

**Refresh Queue Enhancement**

- Added pending refresh handling during an active refresh

### v2.2.0

**Lightning Operations Enhancement**

- Added lightning priority banner
- Added blinking lightning icon and value
- Added hazardous PSI banner
- Aligned PSI Risk Matrix logic

### v2.1.0

- Added regional PSI
- Added regional forecast mapping
- Added test mode framework
- Added lightning alert animation

### v2.0

- Created Singapore multi-zone dashboard foundation
- Added West, East, North, South, and Central selection

## Limitations

- PSI and the 2-hour forecast are selected by zone.
- Temperature, humidity, and rainfall currently use the first available reading returned by their respective data feeds.
- Lightning observations are treated as observations returned by the Singapore data feed and are not filtered by the selected zone.
- The dashboard does not replace official alerts, site procedures, risk assessments, or supervisory decisions.

## Author

Created by **Kelvin Siow**.

## Disclaimer

This dashboard is for decision support only. Verify conditions using official information and apply approved workplace safety, emergency, and operational procedures before work starts or continues.
