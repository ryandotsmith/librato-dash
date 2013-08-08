# librato-dash
A program to create librato dashboards from a metrics manifest file. The motivation for librato-dash comes from having spent lots of time pointing and clicking around the Librato UI to configure dashboards. Also, once you have created a dashboard, there is not a good way to reproduce it. Thus, librato-dash solves these problems while also providing a new way to communicate the KPIs of your system. Keep your `metrics.yml` file in your app's root directory. This way other maintainers of your system can read about your metrics.

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
You can specify a group of default attributes at the dashboard and instrument level. The attributes can be: metrics attributes, instrument attributes, or instrument stream attributes. Librato-dash will make sure that the correct attribute gets associated with its data type. For example, your dashboard defaults section can contain defaults for both instrument attributes and metrics attributes and librato-dash will use information about the Librato API to ensure the default instrument attributes are not associated with the metric attributes and vise versa.

## Idempotency
Librato-dash will not delete any of your metrics, instruments, or dashboards. It will remove instruments not defined in your metrics manifest from your dashboard. So as long as you are keeping your dashboard in sync with your manifest, you will be fine. Also, as you add metrics to your manifest, you can continue to run librato-dash on the manifest with no negative side-effects. If you do experience a negative side-effect, please report it as a bug.
