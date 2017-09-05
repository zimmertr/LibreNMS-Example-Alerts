# LibreNMS Example Alerts

Collection of my custom alerts. Defined here since examples are scarce on the internet and I did not want to recreate them.

## Alert Example 

| # | Name | Rule | Severity | Extra |
| - | ---- | ---- | -------- | ----- |
| 1 | Host has been down for 5 minutes. | %macros.device_down = "1" | critical | Max: 1 Delay: 300 Interval: 1800 |
| 2 | CPU usage > 90% for 5 minutes. | %processors.processor_usage >= "90" | warning | Max: 1 Delay: 300 Interval: 900 |

## Included alerts 

![Alt text](https://raw.githubusercontent.com/zimmertr/Librenms-Example-Alerts/master/alerts.png "Alerts in LibreNMS")

## Alert Template

![Alt text](https://raw.githubusercontent.com/zimmertr/Librenms-Example-Alerts/master/alert_template.png "Alert template in LibeNMS")
