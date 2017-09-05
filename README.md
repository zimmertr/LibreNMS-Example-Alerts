# LibreNMS Example Alerts

Collection of my custom alerts. Defined here since examples are scarce on the internet and I did not want to recreate them.


## Included alerts 

| # | Name | Rule | Severity | Extra |
| - | ---- | ---- | -------- | ----- |
| 1 | Host has been down for 5 minutes. | %macros.device_down = "1" | critical | Max: 1 Delay: 300 Interval: 1800 |
| 2 | CPU usage > 90% for 5 minutes. | %processors.processor_usage >= "90" | warning | Max: 1 Delay: 300 Interval: 900 |
| 3 | Memory usage > 90% for 5 minutes. | %mempools.mempool_perc >= "90" | warning | Max: 1 Delay: 300 Interval: 900 |
| 4 | Root filesystem has less than 5% free space available. | %storage.storage_descr = "/" && %storage.storage_perc >= "95" | critical | Max: 1 Delay: 60 Interval: 900 |
| 5 | Disk usage is abnormally high. | %storage.storage_perc > %storage.storage_perc_warn && %devices.type = "server" && %storage.storage_descr !~ "/boot" = "" | critical | Max: 1 Delay: 60 Interval: 900
| 6 | AUTHENTICATION FAILURE!!!!!!! | %syslog.msg ~ "@authentication failure@" = %syslog.timestamp >= %macros.past_5m | critical | Max: -1 Delay: 300 Interval: 300 |
| 7 | Network usage > 80% for 5 minutes. | %macros.port_usage_perc >= "80" && %port.port_descr_type != "client" && %ports.ifType != "softwareLoopback" | ok | Max: -1 Delay: 300 Interval: 300 |
| 8 | CPU Latency > 500ms for 1 minute. | %device_perf.avg >= "1000" | critical | Max: 1 Delay: 60 Interval: 900 |
| 9 | Network usage > 2MBps for 5 minutes. | %ports.ifHighSpeed >= "2" | ok | Max: 1 Delay: 300 Interval: 900 |
| 10 | Device discovered within the last 60 minutes | %eventlog.type = "discovery" && %eventlog.message ~ "@autodiscovered@" && %eventlog.datetime >= %macros.past_60m | ok | Max: 1 Delay: 0 Interval: 300 |
| 11 | Host has been rebooted. | %devices.uptime < "300" && %macros.device = "1" | warning | Max: 1 Delay: 300 Interval: 300 |
| 12 | Poller is taking longer than expected. | %pollers.time_taken >= "250" | critical | Max: -1 Delay: 300 Interval: 300 |
| 13 | A network port has gone down. | %ports.ifOperStatus = "down" && %ports.ifOperStatus_prev = "up" && %macros.device_up = "1" | warning | Max: -1 Delay: 300 Interval: 300 | 
| 14 | Interface errors rate is abnormally high. | %ports.ifOutErrors_rate >= "100" || %ports.ifInErrors_rate >= "100" | critical | Max: -1 Delay: 300 Interval: 300 | 
| 15 | Host has entered a Warning state. | %services.service_status = "1" | warning | Max: -1 Delay: 300 Interval: 300 | 
| 16 | Host has entered a Critical state. | %services.service_status = "2" | critical | Max: -1 Delay: 300 Interval: 300 | 
| 17 | FQDN does not include the domain name. | %devices.sysName !~ "@sol.milkyway" | warning | Max: -1 Delay: 300 Interval: 300 |
| 18 | Hostname includes the domain name. | %devices.hostname ~ "@.sol.milkyway" | warning | Max: -1 Delay: 300 Interval: 300 | 
| 19 | IP Address is within the DHCP scope. | %devices.ip ~ "192.168.1.2@" | warning | Max: -1 Delay: 300 Interval: 300 | 
| 20 | Host has not been polled within the last day. | %devices.last_polled >= "86400" | critical | Max: -1 Delay: 300 Interval: 300 | Max: 1 Delay: 1 Interval: 300 | 
| 21 | Host is using a slow network adapter. | %ports.port_descr_speed > "1000" | ok | Max: -1 Delay: 300 Interval: 300 |
| 22 | CPU ready time > 10% for 5 minutes. | %processes.cputime >= "10" | critical | Max: -1 Delay: 300 Interval: 900 |
| 23 | Host has less than 1GB of allocated memory. | %vminfo.vmwVmMemSize <= "1024" | warning | Max: -1 Delay: 300 Interval: 300 |
| 24 | Host has more than 3 VCPUs. | %vminfo.vmwVmCpus >= "3" | warning | Max: -1 Delay: 300 Interval: 300 |


## Alert Template

**Alert Title:** LibreNMS (%hostname) - NEW ALERT  
**Recovery Title:** LibreNMS (%hostname) - CANCELLATION  
**Alert Body**:  
```
{if %state == 0}Duration: %elapsed{else}Severity: %severity{/if}

Rule: {if %name}%name{else}%rule{/if}
---------------------------
Timestamp: %timestamp
Uptime: %uptime_long
```

## Alert Example 

![Alt text](https://raw.githubusercontent.com/zimmertr/Librenms-Example-Alerts/master/alert_example.png "Alerts in LibeNMS")
