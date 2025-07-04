# DNS Dashboard Panels SPL Queries

## Top DNS Sources
```spl
index=* sourcetype=dnslogs | top fqdn, src_ip
```
## Top DNS Source IPs
```spl
index=* sourcetype=dnslogs | top src_ip limit=10
```
## Unusual DNS Record Types
```spl
index=* sourcetype=dnslogs record=TXT OR record=NULL | stats count by src_ip fqdn record
```
## DNS Queries by Record Type
```spl
index=* sourcetype=dnslogs | stats count by record

```
## DNS Activity
```spl
index=_* OR index=* sourcetype=dnslogs  | stats count by fqdn
```
## Top DNS Destination IPs
```spl
index=* sourcetype=dnslogs | top dst_ip limit=10
```
## High-Frequency Queried Domains (Potential Anomalies)
```spl
index=* sourcetype=dnslogs | stats count by fqdn | where count > 1000 | sort - count
```
## DNS Records Over Time
```spl
index=* sourcetype=dnslogs | timechart span=10m count by record
```
## DNS Queries by Source and Destination IP Pair
```spl
index=* sourcetype=dnslogs | stats count by src_ip, dst_ip | sort - count
