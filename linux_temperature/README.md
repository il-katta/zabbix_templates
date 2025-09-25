# Zabbix Linux Temperature Template

## Prerequisites

- Zabbix Agent must be installed and configured

## Installation

1. Install and configure `lm-sensors` package on the target system
2. Add the following line to your Zabbix Agent configuration file:
   ```
   UserParameter=sensors,/usr/bin/sensors -j
   ```
3. Restart the Zabbix Agent service
4. Import the [template file](Linux%20CPU%20Temperature%20by%20Zabbix%20agent.yml) into your Zabbix server

## Configuration

### Macros

Configure the following macros for the template:

- **`{$SENSORS_JSON_PATH}`**: JSONPath expression to extract the desired temperature value from the sensors output (according to the output of `sensors -j` command on the target host)
- **`{$CPU_TEMP_WARN}`**: Warning threshold for temperature triggers (default value recommended)
- **`{$CPU_TEMP_CRITICAL}`**: Critical threshold for temperature triggers (default value recommended)

### Usage

The template monitors system temperatures by parsing the JSON output from `lm-sensors`. Configure the `{$SENSORS_JSON_PATH}` macro to match the specific temperature sensor you want to monitor from your system's sensors output.