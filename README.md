# Singapore Weather & Outdoor Work Dashboard

**Version 2.5.0 | Cause-Based Advisory Enhancement**

A browser-based weather and outdoor-work decision-support dashboard covering five Singapore regions.

The dashboard combines regional PSI and forecast information, nearest-active-station weather readings, Singapore-wide lightning observations, operational advisories, risk status, system health, refresh readiness, and saved region preference.

## Current Release

```text
Version: 2.5.0
Release: Cause-Based Advisory Enhancement
```

v2.5.0 adds a structured decision-support layer to the v2.4.2 dashboard. The advisory now identifies the main hazard, supporting conditions, affected activities, operational actions, control priority, and decision basis.

The release retains:

- Five-minute automatic refresh
- Refresh Now control
- Seven-feed refresh progress
- Last successful refresh tracking
- Data freshness
- Preferred region persistence
- Regional station selection
- Regional PSI and forecast mapping
- Refresh lock and pending-refresh queue
- System Health and Dashboard Health

## Region Selection

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
- Decision Basis region display

### Preferred Region

The selected region is stored in the browser using `localStorage`.

- The selected region remains after page refresh.
- The selected region is restored when the dashboard is reopened in the same browser.
- Invalid stored values default to West.
- Browser storage errors do not stop the dashboard.

The preference is specific to the browser, device, and dashboard address.

## Cause-Based Outdoor Work Advisory

The advisory explains what is driving the current dashboard state and what users should do.

### Primary Hazard

The highest-priority active condition is displayed first.

Possible primary hazards include:

- Singapore Lightning Observations
- Hazardous Air Quality
- Very Unhealthy Air Quality
- High Heat Stress
- Moderate Heat Stress
- Unhealthy Air Quality
- Rain Detected
- Rain, Shower, or Thunder Forecast
- Live Data Incomplete
- No Active Hazard

### Measurement, Trigger, and Control

Each primary hazard states:

- Measurement used
- Trigger threshold
- Control category

Example:

```text
Primary Hazard
High Heat Stress

Measurement
WBGT: 32.4°C

Trigger
WBGT ≥ 32.0°C or source class High

Control
High heat-stress controls
```

### Supporting Conditions

The dashboard displays up to three other active conditions below the primary hazard.

Example:

```text
Primary Hazard
High Heat Stress

Supporting Conditions
Rain Detected
Showers Forecast
Unhealthy Air Quality
```

### Affected Activities

The advisory identifies activities that may require review.

Examples include:

- Work at height
- Open-field work
- Outdoor sports and events
- Prolonged outdoor work
- Strenuous work
- Direct-sun work
- External access routes
- Rain-sensitive work
- Event setup

### Operational Actions

Actions change according to the primary hazard.

For lightning observations:

- Suspend exposed outdoor activities.
- Suspend work at height and open-field activities.
- Move personnel to shelter.
- Check official site lightning alerts and procedures.

For high heat stress:

- Review strenuous and prolonged outdoor work.
- Increase hydration and rest frequency.
- Reduce physical workload where practicable.
- Monitor personnel for heat-related symptoms.

For rain:

- Review slip, trip, and water-accumulation hazards.
- Check external access routes.
- Protect rain-sensitive equipment and materials.
- Continue monitoring rainfall and lightning.

### Control Priority

The advisory assigns one of these levels:

```text
IMMEDIATE ACTION REQUIRED
HIGH ATTENTION REQUIRED
CONTROLS REQUIRED
ROUTINE MONITORING
DATA VERIFICATION REQUIRED
```

### Decision Basis

The advisory shows the readings used for the decision:

- Selected region
- Lightning observation count
- WBGT
- PSI
- Forecast
- Forecast area

## Lightning Treatment

The lightning feed remains Singapore-wide in v2.5.0.

The dashboard displays the observation count returned by the Singapore API. It does not claim that lightning is within a specific distance of the selected region.

When one or more observations are returned:

- The lightning value changes to Red.
- The lightning icon blinks.
- The main banner changes to a lightning warning.
- Lightning becomes the Primary Hazard.
- The Control Priority becomes Immediate Action Required.

Users must check official site lightning alerts and procedures before acting.

## Regional Weather Station Selection

Air Temperature, Relative Humidity, and Rainfall use the nearest available active station to a representative point for the selected region.

Each card displays:

```text
Station: [station name]
ID: [station ID]
Distance: [distance]
Region: [selected region]
```

Different metrics may use different stations because station availability can differ between datasets.

## Regional Forecast Fallbacks

The dashboard checks forecast areas in a defined order.

```javascript
const AREAS = {
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

If no configured area is returned, the dashboard shows a Mapping Unavailable state instead of using an unrelated forecast area.

## Dashboard Information

The dashboard displays:

- Wet Bulb Globe Temperature, or WBGT
- Singapore-wide lightning observations
- Regional 24-hour PSI
- Regional Air Temperature station reading
- Regional Relative Humidity station reading
- Regional Rainfall station reading
- Regional 2-hour forecast
- Cause-Based Outdoor Work Advisory
- Risk Matrix
- System Health
- Dashboard Health
- Refresh progress
- Last completed refresh
- Last successful refresh
- Data freshness
- Next scheduled refresh

## Risk Matrix

The Risk Matrix evaluates:

- Heat stress
- Lightning
- Air quality
- Weather
- Overall condition

Possible Overall states include:

- Red
- Amber
- Green
- Unknown
- Refreshing

Missing critical data is not treated as safe.

## Advisory and Banner Priority

The dashboard applies this general order:

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

A confirmed Red hazard remains visible if another feed fails. The failed source can appear as a supporting condition.

## PSI Categories

- Above 300: Hazardous
- Above 200: Very Unhealthy
- Above 100: Unhealthy
- 100 or below: Good / Moderate

## Refresh Readiness

### Refresh Now

The **Refresh Now** button uses the same protected refresh function as the automatic schedule.

- The button is disabled during an active refresh.
- Parallel refresh sequences are prevented.
- One pending refresh can be recorded.
- The five-minute automatic refresh remains active.

### Refresh Progress

The dashboard shows:

```text
Refreshing 1/7: WBGT
Refreshing 2/7: Lightning
Refreshing 3/7: PSI
Refreshing 4/7: Temperature
Refreshing 5/7: Humidity
Refreshing 6/7: Rainfall
Refreshing 7/7: Forecast
```

After completion:

```text
Completed: 7/7 feeds OK
```

or:

```text
Completed with unavailable feeds
```

### Last Successful Refresh

The successful timestamp updates only when all seven feed states are `OK`.

A degraded refresh updates the completion time but does not overwrite the last successful timestamp.

### Data Freshness

Freshness is calculated from the last successful refresh:

```text
Fresh: less than 10 minutes
Aging: 10 to less than 20 minutes
Stale: 20 minutes or more
No Successful Refresh: no valid timestamp
```

The timestamp is stored in the same browser using `localStorage`.

## System Health

Each feed can show:

- OK
- Loading
- Rate Limited
- Mapping Unavailable
- Unavailable

Dashboard Health can show:

```text
🟢 HEALTHY
🟠 DEGRADED
🔄 REFRESHING
🔵 INITIALISING
```

## Reliability Controls

The dashboard includes:

- Five-minute automatic refresh
- Manual Refresh Now control
- Seven-stage refresh progress
- Delay between API requests
- Refresh lock protection using `try` and `finally`
- One pending refresh queue
- Consistent selected-region snapshot during a refresh
- Regional refresh loading state
- Forecast fallback protection
- Failed API state cleanup
- Live Data Incomplete protection
- Preferred-region validation
- Last-successful-refresh browser storage
- Browser storage error handling
- Freshness calculation based on the last fully successful refresh
- Dynamic text escaping in the Cause-Based Advisory

## Data Classification

- WBGT: National feed
- Lightning: Singapore-wide observations
- PSI: Regional
- Forecast: Regional area
- Temperature: Regional station
- Humidity: Regional station
- Rainfall: Regional station

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
├── CHANGELOG.md
└── Singapore_Weather_Dashboard_User_Manual_v2.4.2.docx
```

The dashboard uses one HTML file containing its HTML, CSS, and JavaScript.

## GitHub Pages Deployment

1. Keep a backup of the current production `index.html`.
2. Rename `index_v2.5.0.html` to `index.html`.
3. Upload `index.html`, `README.md`, and `CHANGELOG.md` to the repository root.
4. Commit the files to the `main` branch.
5. Confirm GitHub Pages deploys from `main` and `/ (root)`.
6. Open the published dashboard.
7. Run the production checks below.

## Production Checks

Before deployment, confirm:

```javascript
const TEST = {
    LIGHTNING: false,
    PSI: false,
    WBGT: false,
    RAINFALL: false
};
```

After deployment:

1. Confirm the browser title and dashboard label show v2.5.0.
2. Confirm the Active Region matches the selector.
3. Test West, East, North, South, and Central.
4. Confirm the preferred region remains after page reload.
5. Select **Refresh Now**.
6. Confirm progress moves from feed 1 to feed 7.
7. Confirm the Cause-Based Advisory displays a Primary Hazard.
8. Confirm Supporting Conditions appear when more than one condition is active.
9. Confirm Affected Activities match the Primary Hazard.
10. Confirm Operational Actions match the Primary Hazard.
11. Confirm Control Priority is displayed.
12. Confirm Decision Basis shows the selected region and current readings.
13. Confirm a rain or shower condition produces wet-weather controls.
14. Confirm Last Successful Refresh and Data Freshness update correctly.
15. Confirm System Health shows all seven feeds.
16. Confirm there are no browser console errors.

## Known Limitations

- Region reference points are representative points and not official boundaries.
- The nearest active station may not represent all conditions across a region.
- Temperature, Humidity, and Rainfall may use different stations.
- Station selection can change when a nearer station is unavailable.
- Lightning observations are Singapore-wide and are not filtered by selected region.
- The dashboard does not calculate lightning distance from the selected region in v2.5.0.
- WBGT is a national feed and is not selected by region.
- Forecast information is area-based rather than site-specific.
- Preferred-region and successful-refresh storage do not transfer between browsers or devices.
- Clearing browser site data removes stored values.
- External API rate limiting or downtime can produce API Busy or Unavailable states.
- Data Freshness reflects the last complete seven-feed browser success, not official source publication time.
- The Cause-Based Advisory is rule-based and does not replace a site risk assessment.
- The dashboard does not store historical trends or persistent operational event logs.
- The dashboard is not an official warning system or system of record.
- Official alerts, approved procedures, risk assessments, and supervisor instructions take precedence.

## Version History

### v2.5.0

Cause-Based Advisory Enhancement:

- Added Primary Hazard identification.
- Added Measurement, Trigger, and Control details.
- Added up to three Supporting Conditions.
- Added Affected Activities.
- Added hazard-specific Operational Actions.
- Added Control Priority levels.
- Added Decision Basis.
- Added rule-based handling for heat, air quality, rain, forecast, lightning observations, and missing data.
- Retained v2.4.2 regional and refresh-readiness functions.

### v2.4.2

Operational Readiness Enhancement:

- Added protected Refresh Now control.
- Added seven-feed refresh progress.
- Added last successful refresh tracking.
- Added Data Freshness.

### v2.4.1

Operational Visibility Enhancement:

- Added Active Region indicator.
- Added Dashboard Health badges.
- Added detailed System Health statuses.
- Improved station source formatting.
- Added Forecast Area label and Data Classification legend.

### v2.4.0

Regional Weather Station Selection:

- Added regional Temperature, Humidity, and Rainfall station selection.
- Added station name, ID, distance, and region display.

### v2.3.0

- Added preferred-region persistence and validation.

### v2.2.x

- Added Lightning Priority Banner.
- Added forecast mapping protection.
- Added refresh queue and refresh-lock protection.
- Added API failure and Live Data Incomplete handling.

### v2.1.0

- Added regional PSI and forecast mapping.

### v2.0.0

- Created the Singapore multi-zone dashboard.

## Author

Created by **Kelvin Siow**.

## Disclaimer

This dashboard is for decision support only. Verify conditions using official information and apply approved workplace safety, emergency, and operational procedures before work starts or continues.
