# SPL Queries

## Total HTTP Event Count

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| stats count as total_http_events
```

### Purpose

Count the total number of HTTP events in the dataset and confirm successful ingestion.

### Result

2,048,440 HTTP events were identified.

### Screenshot

```text
screenshots/total-http-event-count.png
```

---

## HTTP Activity Over Time

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| rex field=_raw "^(?<unix_time>\d+\.\d+)"
| eval _time=unix_time
| timechart span=1m count as http_events
```

### Purpose

Analyze HTTP event volume over time to identify traffic patterns and potential spikes in web activity.

### Result

The analysis revealed multiple spikes in HTTP traffic volume during the observed timeframe.
The query also validated that event timestamps were successfully extracted and usable for time-based analysis within Splunk.


### Screenshot

```text
Dashboards/http-event-volume-over-time.png
```

---
