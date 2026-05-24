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

# Final Assessment

## Investigation Summary

Analysis of the HTTP log dataset identified multiple indicators of suspicious and potentially malicious web activity originating from internal source IP addresses.

The investigation identified two primary findings:

- Automated web directory enumeration activity associated with the OWASP DirBuster tool (`192.168.203.63`)
- Web reconnaissance and directory traversal probing activity targeting sensitive web application resources (`192.168.202.110`)

Observed activity included:
- High-volume HTTP 404 response generation
- Large-scale URI enumeration
- Requests targeting administrative web application paths
- Directory traversal payloads attempting to access sensitive system files
- Successful HTTP 200 responses associated with traversal-style requests

The overall behavior is consistent with vulnerability scanning, web reconnaissance, and exploitation probing activity targeting exposed web application resources within the environment.

## Severity Assessment

- Finding #1 — Medium Severity
- Finding #2 — High Severity

The second finding was assessed with higher severity due to successful HTTP 200 responses associated with traversal-style payloads targeting sensitive system resources.

## Confidence Assessment

- Finding #1 was assessed with high confidence as  web directory enumeration activity associated with the OWASP DirBuster tool.
- Finding #2 was assessed with high confidence as malicious web reconnaissance and exploitation-oriented traversal probing activity.

The assessment was based on multiple correlated indicators including:
- repeated traversal-style payloads
- requests targeting sensitive system files
- phpMyAdmin and CGI-related targeting
- high-volume HTTP 404 activity
- and repeated HTTP 200 responses associated with traversal-style requests across multiple hosts and applications

No definitive evidence of successful system compromise or post-exploitation activity was identified within the available HTTP logs.

## Potential Impact

If performed against vulnerable production systems, the observed activity could potentially lead to:
- Exposure of sensitive files
- Discovery of vulnerable web application components
- Unauthorized access to system resources
- Additional exploitation attempts against exposed applications

In a production environment, successful traversal-style requests targeting sensitive files such as `/etc/passwd` could expose system configuration details, usernames, application paths, or other information useful for additional exploitation and lateral movement attempts.

## Analyst Assessment

- Finding #1 was assessed as a True Positive associated with directory enumeration activity.
- Finding #2 was assessed as a High-Confidence True Positive associated with web reconnaissance and exploitation-oriented traversal probing activity.

At the current stage of the investigation, no definitive evidence of successful system compromise or post-exploitation activity was identified within the available HTTP logs.

Additional host-level investigation and application review would be recommended to determine whether any targeted systems were successfully exploited.

## Recommendations

Recommended defensive actions include:
- Restrict access to sensitive administrative paths
- Disable unnecessary CGI and legacy web components
- Implement Web Application Firewall (WAF) protections
- Monitor for directory traversal patterns and abnormal HTTP activity
- Review systems targeted by successful traversal-style requests
- Block or alert on automated scanning tools and suspicious user-agents
