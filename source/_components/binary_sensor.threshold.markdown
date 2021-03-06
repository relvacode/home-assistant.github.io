---
layout: page
title: "Threshold Binary Sensor"
description: "Instructions on how to integrate threshold binary sensors into Home Assistant."
date: 2016-11-26 12:10
sidebar: true
comments: false
sharing: true
footer: true
logo: home-assistant.png
ha_category: Binary Sensor
ha_iot_class: "Local Polling"
ha_release: 0.34
---


The `threshold` binary sensor platform observes the state of another sensor. If the value is below (`lower`) or higher (`upper`) than the given threshold then state of the threshold sensor is changed. It support also a range if `lower` and `upper` are given.

If the sensor is configured with no hysteresis and the sensor value is equal to the threshold, the sensor is turned off since it is not `lower` or `upper` with respect to the threshold.

It's an alternative to the template binary sensor's `value_template:` to get the abnormal/too high/too low states.

{% raw %}
```yaml
{{ states.sensor.furnace.state > 2.5 }}
```
{% endraw %}

To enable the threshold sensor, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
binary_sensor:
  - platform: threshold
    entity_id: sensor.random
    lower: 20
```

{% configuration %}
entity_id:
  description: "The entity to monitor. Only [sensors](/components/sensor/) are supported."
  required: true
  type: entity_id
lower:
  description: The lower threshold which the observed value is compared against.
  required: false
  type: float
upper:
  description: The upper threshold which the observed value is compared against.
  required: false
  type: float
hysteresis:
  description: The distance the observed value must be from the threshold before the state is changed.
  required: false
  type: float
  default: 0.0
name:
  description:  Name of the sensor to use in the frontend.
  required: false
  type: string
  default: 
{% endconfiguration %}

