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

Analysis of HTTP 404 response activity identified multiple source IP addresses generating high volumes of failed web requests across the environment.

One source IP address (`192.168.203.63`) generated a significantly higher volume of HTTP 404 responses compared to all other observed hosts, with over 1.2 million failed requests recorded.

Further analysis revealed that this activity was associated with the `DirBuster-0.12` user-agent, indicating automated web directory enumeration behavior.

The observed pattern is consistent with aggressive reconnaissance activity, including large-scale URI brute-forcing and web content discovery attempts aimed at identifying accessible or hidden web resources within the environment.

---


## Investigation Notes: 192.168.202.110

Initial analysis of HTTP logs identified abnormal traffic originating from 192.168.202.110, with a high number of HTTP 404 responses across multiple endpoints.

Further investigation revealed repeated attempts to access sensitive web application paths, including administrative interfaces and login pages.

Additional inspection identified directory traversal patterns targeting system files such as `/etc/passwd` and Windows configuration files (`win.ini`).


