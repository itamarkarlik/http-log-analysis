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

## Top Source IPs Generating HTTP 404 Responses

```spl
index="soc-splunk-lab" sourcetype="http_logs"
| where status_code="404"
| stats count by src_ip
| sort - count
| head 10
```

### Purpose

Identify the source IP addresses responsible for generating the highest number of HTTP 404 responses.

### Result

Several internal source IP addresses generated a high volume of HTTP 404 responses, potentially indicating resource enumeration, broken links, or scanning activity.

### Screenshot

```text
Dashboards/top-source-ips-404-responses.png
```

---


## URI Analysis for 192.168.202.110

```spl
index="soc-splunk-lab" sourcetype="http_logs" src_ip="192.168.202.110"
| stats count by uri
| sort - count
| head 20
```

### Purpose

Identify the most frequently requested HTTP URIs that resulted in 404 responses for the suspicious source IP 192.168.202.110.

### Result

The analysis revealed repeated access attempts to sensitive web application paths including administrative interfaces, login pages, and multiple directory traversal payloads. Several requests included attempts to access system files such as `/etc/passwd` and Windows configuration files (`win.ini`), indicating potential reconnaissance and exploitation attempts.

### Screenshot

```text
Screenshots/ip-192-168-202-110-uri-analysis.png
```

---

## Raw Request Analysis for 192.168.202.110 (Traversal Focus)

```spl
index="soc-splunk-lab" sourcetype="http_logs" src_ip="192.168.202.110"
| search uri="*../*"
| table _time uri status_code http_method user_agent
```

### Purpose

Detect directory traversal attempts.

### Result

Multiple directory traversal patterns were observed, including attempts to access `/etc/passwd` and Windows system files.

### Screenshot

```text
Screenshots/ip-192-168-202-110-traversal-analysis.png
```
