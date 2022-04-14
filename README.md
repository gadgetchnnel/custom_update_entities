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

### Sample config

Here is a simple config which uses the shell_command integration to update Home Assistant Core.

```yaml
custom_update_entities:
  updaters:
    - name: Home Assistant Core
      latest_version_entity: sensor.latest_beta_version
      installed_version_entity: sensor.current_version
      logo_url: https://brands.home-assistant.io/_/homeassistant/icon.png
      release_notes_url: https://www.home-assistant.io/latest-release-notes/
      update_action:
        - service: shell_command.update_hass
          data:
            version: '{{ version }}'
```

### Options

* **updaters** `list` Required  
List of updaters
    * **name** `string` Required  
      Name of the software, etc. which this updater will update.  
      (this will be used as the **title** attribute in the update entity, and will be suffixed with ": Update" in the entity name)
    * **latest_version_entity** `string` Required  
      A sensor entity, the state of which contains the latest version of this software
    * **installed_version_entity** `string` Required  
      A sensor entity, the state of which contains the currently installed version of this software
    * **logo_url** `string` Optional  
      The URL of an image to use as the logo
    * **release_notes_url** `string` Optional  
      A URL for the release notes / announcement for this version
    * **update_action** [action](https://www.home-assistant.io/docs/scripts/) Required  
      The action to run to update the software - the **version** template variable will be populated with the version to be installed and this can be used as `{{ version }}` in the script.
