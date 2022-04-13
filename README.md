# Custom Update Entities
Custom Update Entities for Home Assistant

This allows you to create custom update entities for Home Assistant 2022.4.0 or later.
Each update entity requires two sensors, one for the installed version and one for the latest version, and an update action.

## Installation

### Via HACS

Add as a custom repository (Integration) to HACS and then install it.

### Manually

Download the **custom_update_entities** folder and copy ir ton the **custom_components** folder in your Home Assistant config folder.

## Configuration

Here is a simple config which uses the shell_command integration to update Home Assistant Core.

```yaml
custom_update_entities:
  updaters:
    - name: Home Assistant Core
      latest_version_entity: sensor.latest_beta_version
      installed_version_entity: sensor.current_version
      logo_url: https://brands.home-assistant.io/_/homeassistant/icon.png
      update_action:
        - service: shell_command.update_hass
          data:
            version: '{{ version }}'
```
