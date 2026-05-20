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

## First and Last HTTP Event Time

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| rex field=_raw "^(?<unix_time>\d+)"
| stats min(unix_time) as first_event max(unix_time) as last_event
| convert ctime(first_event) ctime(last_event)
```

### Purpose

Identify the first and last HTTP events in the dataset using extracted Unix timestamps.

### Result

The dataset contains HTTP events between:
- 03/16/2012 12:30:00
- 03/17/2012 20:46:54

### Screenshot

```text
screenshots/first-last-http-event-time.png
```

---
