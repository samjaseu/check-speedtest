# check-speedtest

This is a fork of sivel's speedtest-cli with Icinga2 support.
Original repo found under: https://github.com/sivel/speedtest-cli


## Installation
```
wget -O check-speedtest https://raw.githubusercontent.com/samjaseu/check-speedtest/master/check-speedtest
```


## Usage
**Only showing Icinga2 support here.**


### command line
```
$ check-speedtest --icinga2
Ping: 5.108 ms
Download: 321.87 Mbit/s
Upload: 644.90 Mbit/s
|ping=5.108ms
|download=321.87
|upload=644.90
```


### Icinga2

#### CheckCommand
```
object CheckCommand "command-check-speedtest" {
    import "plugin-check-command"
    command = [ PluginDir + "/check-speedtest" ]
    arguments += {
        "--icinga2" = {
            order = 0
            required = true
        }
    }
}
```

#### Service template
```
template Service "Check Speedtest Template" {
    check_command = "command-check-speedtest"
    notes_url = "https://github.com/samjaseu/check-speedtest"
}
```

#### Service check output
![Speedtest service check output](speedtest-service-check-output.png)

#### Grafana speedtest graph
![Grafana speedtest graph](grafana-speedtest-graph.png)
