# Verifying and Manual Control of RoCS Services after Installation

## Verifying Services Effectiveness
After completing the installation, verify whether the automatic startup of the three services is working properly. If all three are actively running, everything is functioning as expected.

### Verifying `rocs_enable_wifi` Service
```shell
sudo systemctl status rocs_enable_wifi.service
```

### Verifying `rocs_svr` Service
```shell
sudo systemctl status rocs_svr.service
```

### Verifying `rocs_model` Service
```shell
sudo systemctl status rocs_model.service
```

## Manual Start
Manually initiate the RoCS services if needed:

### Manual Start `rocs_enable_wifi` Service
```shell
sudo systemctl start rocs_enable_wifi.service
```

### Manual Start `rocs_svr` Service
```shell
sudo systemctl start rocs_svr.service
```

### Manual Start `rocs_model` Service
```shell
sudo systemctl start rocs_model.service
```

## Manual Stop
Manually stop the RoCS services if necessary:

### Manual Stop `rocs_enable_wifi` Service
```shell
sudo systemctl stop rocs_enable_wifi.service
```

### Manual Stop `rocs_svr` Service
```shell
sudo systemctl stop rocs_svr.service
```

### Manual Stop `rocs_model` Service
```shell
sudo systemctl stop rocs_model.service
```

## View Logs
Monitor the system logs for RoCS-related entries:

```shell
sudo tail -f /var/log/syslog | grep rocs
```
