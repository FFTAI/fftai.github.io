# Verifying and Manual Control of RoCS Services after Installation

---

## Whether the installation is successful or not.
```shell
dpkg -l | grep rocs
```

## Effectiveness
After completing the installation, verify whether the automatic startup of the five services is working properly. If all five are actively running, everything is functioning as expected.

1. rocs-wifi
```shell
sudo systemctl status rocs-wifi.service
```

2. rocs-svr
```shell
sudo systemctl status rocs-svr.service
```

## Manual Start
Manually initiate the RoCS services if needed:

1. Manual Start `rocs-wifi` Service
```shell
sudo systemctl start rocs_enable_wifi.service
```

2. Manual Start `rocs-svr` Service
```shell
sudo systemctl start rocs_svr.service
```

## Manual Stop
Manually stop the RoCS services if necessary:

1. Manual Stop `rocs-wifi` Service
```shell
sudo systemctl stop rocs-wifi.service
```

2. Manual Stop `rocs-svr` Service
```shell
sudo systemctl stop rocs-svr.service
```

## View Logs
1. Monitor the log of `rocs-svr`:
```shell
sudo tail -f /var/log/syslog | grep rocs
```

2. Monitor the log of `rocs-control`:
```shell
sudo tail -f ~/RoCS/server.log
```