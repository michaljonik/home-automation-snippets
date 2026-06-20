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
