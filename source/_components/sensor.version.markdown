---
layout: page
title: "Version Sensor"
description: "Instructions on how to integrate a version sensor into Home Assistant."
date: 2017-08-10 10:30
sidebar: true
comments: false
sharing: true
footer: true
ha_category: Utility
ha_iot_class: "Local Pushing"
logo: home-assistant.png
ha_release: 0.52
ha_qa_scale: internal
---

The `version` sensor platform is displaying the current version of Home Assistant in the frontend.

## {% linkable_title Configuration %}

To enable this sensor, add the following lines to your `configuration.yaml` file for a GET request:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: version
```

{% configuration %}
name:
  description: Name to use in the frontend.
  required: false
  type: string
  default: Current Version
{% endconfiguration %}

## {% linkable_title Alternatives %}

This sensor is an alternative to the existing solutions to achieve the same
result through various platforms.
Remember that you can easily get the installed version on the command line.

```bash
$ hass --version
```

Or go to the <img src='/images/screenshots/developer-tool-about-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> **Info** section of the **Developer Tools**.

A [`command_line`](/components/sensor.command_line/) with
[`hass`](/docs/tools/hass/) to display your current version.

```yaml
sensor:
  - platform: command_line
    name: Version
    command: "/home/homeassistant/bin/hass --version"
```

It's also possible to ready a file called `.HA_VERSION` which is located in your
Home Assistant [configuration](/docs/configuration/) folder.

```yaml
sensor:
  - platform: command_line
    name: Version
    command: "cat /home/homeassistant/.homeassistant/.HA_VERSION"
```

You might think that a [`rest` sensor](/components/sensor.rest/) could work,
too,
but it will not as Home Assistant is not ready when the sensor get initialized.

{% raw %}
```yaml
sensor:
  - platform: rest
    resource: http://IP_ADDRESS:8123/api/config
    name: Current Version
    value_template: '{{ value_json.version }}'
```
{% endraw %}
