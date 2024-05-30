# Popur Litter Box Integration with Home Assistant using ESPHome

Welcome to the Popur Litter Box integration project! This project aims to integrate the Popur Litter Box into Home Assistant using ESPHome. Given the challenges associated with this task, including expired certificates and a lack of security on Popur's side, this README will guide you through the setup process and provide solutions to these issues.

## Introduction
The Popur Litter Box is a smart litter box that can be monitored and controlled via MQTT. However, integrating it with Home Assistant presents challenges due to the use of MQTTS over an MQTT port and an expired certificate. This project provides a workaround for these issues using ESPHome.

## Prerequisites
Before you begin, ensure you have the following:

A Popur Litter Box
An ESP32 microcontroller
Home Assistant setup and running
ESPHome running locally

## ESPHome Configuration
1. Edit the ESPHome MQTT backend for ESP32:
* Navigate to the file `esphome\components\mqtt\mqtt_backend_esp32.cpp`.
* Remove lines 14-99.
* Add the following line: 
```
mqtt_cfg_.uri = MQTT_POPUR_URL;
```
2. Edit the ESPHome config:
* Navigate to the file `esphome\components\esp32\__init__.py`.
* Add lines to line 507
```
add_idf_sdkconfig_option("CONFIG_ESP_TLS_INSECURE", True)
add_idf_sdkconfig_option("CONFIG_ESP_TLS_SKIP_SERVER_CERT_VERIFY", True)
```
3. Add the config.yaml and create the secrets.yaml file.
4. Compile and upload the configuration

## Known Issues
Expired Certificate: Popur's MQTT service uses an expired certificate, requiring disabled certificate verification in ESPHome, which is insecure.
No Security: Popur's MQTT implementation lacks proper security. This issue has been raised with the Popur team.

## Contributing
Contributions are welcome! If you have suggestions or improvements, please submit a pull request or open an issue on GitHub.