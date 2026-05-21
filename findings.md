# Findings

## Automated Web Enumeration Activity Detected

Analysis of HTTP 404 response activity identified a large volume of failed web requests originating from source IP `192.168.203.63`.

Further investigation revealed:

- 1,289,246 HTTP 404 requests
- 1,267,701 unique requested URIs
- The majority of requests used the `DirBuster-0.12` user-agent

The behavior strongly indicates automated web directory enumeration or content discovery activity using the OWASP DirBuster tool.

The activity pattern suggests aggressive scanning of web paths in an attempt to identify accessible resources, hidden directories, or exposed web content.

### Evidence


```text
Dashboards/top-source-ips-404-responses.png
Screenshots/high-unique-uri-count.png
Screenshots/dirbuster-user-agent-detection.png
```
