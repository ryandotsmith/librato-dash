# librato-dash
A program to create librato dashboards from a metrics manifest file. The motivation for librato-dash comes from having spent lots of time pointing and cliking around the Librato UI to configure dashboards. Also, once you have created a dashboard, there is not a good way to reproduce it. Thus, librato-dash solves these problems while also providing a new way to communicate the KPIs of your system. Keep your `metrics.yml` file in your app's root directory. This way other maintainers of your system can read about your metrics.

## Usage
```bash
$ export LIBRATO_URL=https://u:p@metrics-api.librato.com/v1
$ ./librato-dash FILE
```

## Metrics File Format

```yaml
dashboard-name:
  defaults:
    any_librato_attribute: val
  instrument-name:
    defaults:
      any_attribute: val
    metric-name-0:
      specific_attribute: val
    metric-name-1:
      specific_attribute: val
```
See example.yml for a more complete file format.

## Defaults
You can sepcify a group of default attributes at the dashboard and instrument level. The attributes can be: metrics attributes, instrument attributes, or instrument stream attributes. Librato-dash will make sure that the correct attribute gets associated with its data type. For example, your dashboard defaults section can contain defaults for both instrument attributes and metrics attributes and librato-dash will use information about the Librato API to ensure the the default instrument attributes are not associated with the metric attributes and vise versa.
