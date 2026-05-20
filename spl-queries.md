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
| timechart span=15m count as http_events
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

## Top Source IPs by HTTP Request Volume

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| stats count as request_count by src_ip
| sort - request_count
| head 10
```

### Purpose

Identify the source IP addresses generating the highest volume of HTTP requests within the dataset.

### Result

Several internal source IP addresses were responsible for the majority of HTTP traffic observed in the environment.

### Screenshot

```text
Dashboards/top-source-ips-http-volume.png
```

---

