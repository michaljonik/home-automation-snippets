# ESPHome packages

Every file in this directory is an ESPHome [package](https://esphome.io/components/packages/).
You include it in your device configuration and set its parameters with `vars`, so updates reach
your device without editing a copy:

```yaml
packages:
  example:
    url: https://github.com/michaljonik/home-automation-snippets
    ref: main          # pin a commit or tag if you want updates only on your terms
    files:
      - path: esphome/<package>.yaml
        vars:
          some_parameter: value
```

Secrets (API encryption key, OTA password, Wi-Fi) stay in your own `secrets.yaml`. No package here
reads or ships a secret.

Each package describes its features and wiring at the top of the file; parameters and their
defaults are in its `defaults:` block.

## Packages

### Water meter

[`water-meter.yaml`](water-meter.yaml) counts water with a QMC5883L magnetometer fixed to the meter
body, without touching the installation. The counter is kept in flash, survives reboots and
updates, and can be set to the meter reading from Home Assistant with the action
`set_water_meter_litres`. It exposes a `total_increasing` water sensor for the Energy dashboard and
the raw field for calibration. Example: [examples/water-meter.yaml](examples/water-meter.yaml)
(ESP32-CAM).

### Gate controller

[`gate-controller.yaml`](gate-controller.yaml) turns a gate with a single step button into a cover
with open, close and stop. Two limit switches and the photocell feed a state machine, and each
command becomes the right number of presses. If no limit switch confirms a movement within
`motion_timeout`, the state becomes unknown and commands are refused.

- Auto close after passing: the "auto close" switch opens the gate and closes it once the
  photocell clears, after a car has driven through.
- Knock to close: tap-tap, pause, tap-tap on the photocell closes the gate. Off by default and not
  authenticated.

It only presses the controller's button; the controller's own safety devices stay in charge.
Example: [examples/gate.yaml](examples/gate.yaml).

### Sauna controller

[`sauna-controller.yaml`](sauna-controller.yaml) is a thermostat for an electric sauna stove that
keeps its safety limits on the ESP, so they work when Home Assistant or Wi-Fi is down:

- over-temperature cut-off, latched across reboots and cleared only by a button below the limit;
- sensor timeout, for a sensor that goes silent, not only one that reads an invalid value;
- maximum run time;
- OFF after every boot, and a relay interlock that switches the relay off whenever the thermostat
  is OFF or the latch is set.

A local button switches it on (hold 3 s) and off. It complements the stove's own thermal cut-out
and does not replace it. Example: [examples/sauna.yaml](examples/sauna.yaml).
