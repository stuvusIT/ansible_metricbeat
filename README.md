# metricbeat

Setup a metricbeat instance.


## Requirements

An apt based linux system

## Role Variables


| Variable           | Default / Mandatory                                                                                                                                  | Description                                                                                                                                                                                                                                              |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricbeat_config`  | `{ output.elasticsearch: { hosts: ["localhost:9200"] }, metricbeat.config.modules: { reload.enabled: false } }` | Since the metricbeat settings file is a yaml file we write the whole object to the settings file. For more Information please see the [metricbeat settings file documentation](https://www.elastic.co/guide/en/metricbeat/current/metricbeat-settings-file.html) |
| `metricbeat_modules` | `[]`                                                                                                                                                 | List of config files to write to modules.d/. More information below.                                                                                                                                                                                     |

### `metricbeat_modules`
Each entry in the `metricbeat_modules` consists out of the following entries.
| Variable | Default / Mandatory | Description                                                                              |
|----------|---------------------|------------------------------------------------------------------------------------------|
| `name`   | :heavy_check_mark:  | Name of the module config file. This value has to be the same as the name of the module. |
| `config` | :heavy_check_mark:  | Yaml config for the module name .                                                        |

## Example Playbook

```yml
- hosts: all
  become: true
  vars:
    metricbeat_config:
      metricbeat.config.modules:
        reload.enabled: false
      output.logstash:
        hosts: ["localhost:9200"]
	metricbeat_modules:
      - name: graphite
	    config: 
		  - module: graphite
		    metricsets: ["server"]
			enabled: true

```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
