# Raspberry Pi CEC server add-on

Starting from [HomeAssistant](https://www.home-assistant.io) 2021.7.0, the CEC
libraries included in HomeAssistant do no longer support CEC interfaces that are
not included in the Linux kernel itself. Therefore, it is no longer possible to
control the HDMI-CEC bus through the [hdmi-cec](https://www.home-assistant.io/integrations/hdmi_cec/) integration alone.

However, the hdmi-cec integration supports talking to an HDMI-CEC device over
a TCP socket. This add-on launches a HDMI-CEC server which supports the
Raspberry Pi hardware interface.

## Configuration

First, enable the `https://github.com/samueltardieu/homeassistant-addons` repository in
the "Addons" configuration section of Home Assistant.

After enabling this add-on and configuring it
to automatically start, one can use the following in HomeAssistant `configuration.yaml`:

```yaml
hdmi_cec:
  host: 58c14403-pi-cec
```

and restart HomeAssistant. You should then be able to control your HDMI-CEC devices
with the integration commands.

## Notes

For the curious, `58c14403` is the [SHA-1](https://en.wikipedia.org/wiki/SHA-1) hash
of the string `https://github.com/samueltardieu/homeassistant-addons` and is computed
from the repository name by HomeAssistant.

The icon is part of [iconscount display icon](https://iconscout.com/icon/display-171) collection.

## RPI GPU Memory

The libraries that pycec uses require there be 128M of memory allocated to the GPU.
If you see any strange assertions in the logs, use `raspi-config` to change that value.

## The loop argument is deprecated

If you see messages such as

```
Apr 6 23:06:53 s140n-hass 37dcc20d3026[1330]: /usr/local/lib/python3.8/site-packages/pycec/network.py:431: DeprecationWarning: The loop argument is deprecated since Python 3.8, and scheduled for removal in Python 3.10.
```

know that this is due to [pyCEC](https://github.com/konikvranik/pyCEC/issues/68).
