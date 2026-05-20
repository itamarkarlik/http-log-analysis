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

## HTTP Status Code Distribution

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| stats count by status_code
| sort - count
```

### Purpose

Analyze the distribution of HTTP response status codes within the dataset.

### Result

The analysis identified the most common HTTP response codes and provided visibility into different kind of requests.

### Screenshot

```text
Dashboards/http-status-code-distribution.png
```

---

## HTTP Methods Distribution

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| stats count by http_method
| sort - count
| head 10
```

### Purpose

Analyze the distribution of HTTP request methods within the dataset.

### Result

The analysis identified the most frequently used HTTP methods observed in the web traffic logs.

### Screenshot

```text
Dashboards/http-methods-distribution.png
```

---

## Top Requested URIs

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| where uri!="-" AND uri!= "/"
| top limit=10 uri
```

### Purpose

Identify the most frequently requested HTTP URIs within the dataset.

### Result

The analysis identified the most commonly accessed web resources.

### Screenshot

```text
Dashboards/top-requested-uris.png
```

---
