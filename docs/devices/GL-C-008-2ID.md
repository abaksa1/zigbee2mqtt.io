---
title: "Gledopto GL-C-008-2ID control via MQTT"
description: "Integrate your Gledopto GL-C-008-2ID via Zigbee2mqtt with whatever smart home
 infrastructure you are using without the vendors bridge or gateway."
---

*To contribute to this page, edit the following
[file](https://github.com/Koenkk/zigbee2mqtt.io/blob/master/docs/devices/GL-C-008-2ID.md)*

# Gledopto GL-C-008-2ID

| Model | GL-C-008-2ID  |
| Vendor  | Gledopto  |
| Description | Zigbee LED controller RGB + CCT (2 ID) |
| Supports | on/off, brightness, color temperature, color |
| Picture | ![Gledopto GL-C-008-2ID](../images/devices/GL-C-008-2ID.jpg) |

## Notes


### Pairing
1. Switch on your device.
2. Now switch off and on within 2 seconds.
3. Repeat off/on four times.
4. Reset is done when the device is switched on in the fifth time and the light stays on after blinking 4 times


### 2ID handling
This device exposes the two specific endpoints `rgb` and `cct`. The command topics are `zigbee2mqtt/<FRIENDLY_NAME>/rgb/set`, and `zigbee2mqtt/<FRIENDLY_NAME>/cct/set`. Both [specific endpoints can be added to a group](../information/groups.md#adding-a-specific-endpoint). These endpoints are `<FRIENDLY_NAME>/rgb`, and `<FRIENDLY_NAME>/cct`.


### Device type specific configuration
*[How to use device type specific configuration](../information/configuration.md)*


* `transition`: Controls the transition time (in seconds) of on/off, brightness,
color temperature (if applicable) and color (if applicable) changes. Defaults to `0` (no transition).
Note that this value is overridden if a `transition` value is present in the MQTT command payload.


## Manual Home Assistant configuration
Although Home Assistant integration through [MQTT discovery](../integration/home_assistant) is preferred,
manual integration is possible with the following configuration:


{% raw %}
```yaml
light:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    brightness: true
    xy: true
    schema: "json"
    command_topic: "zigbee2mqtt/<FRIENDLY_NAME>/rgb/set"
    brightness_scale: 254
    state_topic_postfix: "rgb"

light:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    brightness: true
    color_temp: true
    schema: "json"
    command_topic: "zigbee2mqtt/<FRIENDLY_NAME>/cct/set"
    brightness_scale: 254
    state_topic_postfix: "cct"

sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    icon: "mdi:signal"
    unit_of_measurement: "lqi"
    value_template: "{{ value_json.linkquality }}"
```
{% endraw %}


