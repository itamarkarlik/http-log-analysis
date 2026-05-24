# Findings

## Finding #1 - Automated Web Enumeration Activity Detected

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

---

## Finding #2 - Web Scanning and Directory Traversal Attempts Detected

Analysis of HTTP 404 response activity and URI patterns identified suspicious web reconnaissance behavior originating from source IP `192.168.202.110`.

Further investigation revealed repeated requests targeting sensitive web application endpoints and system resources.

### Key Observations

- Requests to administrative paths such as `/admin.php` and `/phpmyadmin`
- Directory traversal attempts (`../../../../etc/passwd`, `win.ini`)

Additional analysis identified multiple traversal-style requests that received HTTP 200 responses, including requests attempting to access sensitive resources such as:

- `/etc/passwd`
- `winnt/system32/ipconfig.exe`

The successful responses suggest that some targeted applications processed the traversal-style requests successfully, increasing the likelihood of potential vulnerability exposure or successful resource access attempts.

The behavior strongly indicates automated web scanning and exploitation attempts aimed at discovering vulnerable or exposed web application components.

### Evidence

```text
Screenshots/ip-192-168-202-110-404-uri-analysis.png
Screenshots/ip-192-168-202-110-traversal-analysis.png
Screenshots/ip-192-168-202-110-successful-traversal-responses.png
```
