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

Each package lists its parameters and the hardware it expects in a comment at the top of the file.
