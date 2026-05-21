## HTTP Field Extraction

During the initial review of the raw HTTP events, the log structure was manually analyzed in order to understand the position and meaning of important web traffic fields within the dataset.

To improve searchability, filtering, correlation, and investigation efficiency within Splunk, field extraction was performed to normalize key HTTP attributes from the raw events.

Based on the event structure, the following fields were identified and extracted:

- `src_ip`
- `dest_ip`
- `src_port`
- `dest_port`
- `http_method`
- `unix_time`
- `uri`
- `user_agent`
- `status_code`
- `status_message`
- `http_host`
- `bytes`

The extracted fields were later used throughout the investigation process for traffic analysis, anomaly detection, and HTTP activity monitoring.

---


## High Volume of HTTP 404 Responses

Analysis of HTTP 404 response activity identified several source IP addresses generating failed web requests.

One source IP address (`192.168.203.63`) generated a significantly higher volume of 404 responses compared to all other systems in the dataset, with over 1.2 million failed requests observed.

The activity may indicate automated web requests, aggressive crawling, scanning activity, application misconfiguration, or repeated access attempts to unavailable resources.

Additional investigation was required to determine whether the behavior represented legitimate application activity or potentially suspicious enumeration behavior.
