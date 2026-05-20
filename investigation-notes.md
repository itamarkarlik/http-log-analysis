## HTTP Field Extraction

During the initial review of the raw HTTP events, the log structure was manually analyzed in order to understand the position and meaning of important web traffic fields within the dataset.

Field extraction was then performed to normalize key HTTP attributes for investigation and analysis purposes.

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


---
