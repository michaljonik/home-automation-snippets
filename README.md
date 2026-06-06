# home-automation-snippets

Reusable pieces from my house: ESPHome packages and Home Assistant blueprints. Each one runs on
real hardware at home and is written so you can include it as it is, without copying and editing.

## Layout

| Directory | What is in it | How to use it |
|---|---|---|
| [`esphome/`](esphome/) | ESPHome packages | `packages:` with a `github://` source, see [esphome/README.md](esphome/README.md) |
| [`blueprints/automation/`](blueprints/automation/) | Home Assistant automation blueprints | import by URL in Home Assistant |

## Blueprints

| Blueprint | What it does | Import |
|---|---|---|
| [Conditional notification](blueprints/automation/persistent_notification.yaml) | Shows a persistent notification on the phone while an entity is in a given state and clears it when the state changes | [![Open your Home Assistant instance and show the blueprint import dialog with this blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmichaljonik%2Fhome-automation-snippets%2Fblob%2Fmain%2Fblueprints%2Fautomation%2Fpersistent_notification.yaml) |

## Safety

Some packages here switch mains-powered heaters or drive motors. The code adds software limits; it
does not replace the protection built into the appliance, the drive controller or the electrical
installation. Wiring on 230/400 V belongs to a qualified electrician. You use everything here at
your own risk.

## License

[Apache 2.0](LICENSE)
