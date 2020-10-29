# Performance Analysis

You want to improve velorens performance?
But you don't know how to best measure velorens performance ?
This page is a collection of tools that are already integrated in veloren and can be used to help you collecting data.

## Compiling With Release & Debug Symbols

Most tools work better with debug symbols AND in release mode:
You can build the project with debug symbols included by running this command:

```bash
cargo build -Z unstable-options --profile releasedebuginfo
```

# Integrated tooling

## Prometheus

Prometheus allows you to gather internals of veloren during runtime. The data points are aggregated (e.g. all entities, state tick time spend in physics system).
It allows to get a quick, rough look into velorens performance, but is not very detailed.

Prometheus statics are exported by default whenever you run `veloren-server-cli`
Open your webbrowser http://localhost:14005 to see the raw values.

You can import this data into prometheus via this tutorial: https://prometheus.io/docs/prometheus/latest/getting_started/
Add `localhost:14005/metrics` to your `/etc/prometheus/prometheus.yml`.
Connect to http://localhost:9090 and enter `tick_time`, execute and switch over to `Graph` mode.

You can connect your prometheus service to a Grafana instance: https://prometheus.io/docs/visualization/grafana/
You'll find example dashboards in the veloren infrastructure repo (not yet available): https://gitlab.com/veloren/infrastructure/-/blob/master/veloren-infra/templates/grafana-dashboads-gameserver.yaml

## Tracy

Tracy https://bitbucket.org/wolfpld/tracy/src/master/ enables you to track the time spend in certain spans based on trace spans.
It allows to get a detailed level into certain blocks of code, when they execute and how long they take.

Enable tracy support with the feature `tracy`:
```bash
cargo -Zunstable-options -Zpackage-features run --bin veloren-voxygen --no-default-features --features tracy,gl --profile releasedebuginfo
```

Connect to the running process via you tracy tool https://aur.archlinux.org/packages/tracy/

## 'cargo build -Z timings'

When you want to analyse compile time, you can use cargos feature `-Z timings`. It will output a .html file with individual compile times, and dependencies and a total graph showing inactive, active and indling projects.

# External tooling

## rust: flamegraph

follow the installation tutorial here: https://github.com/flamegraph-rs/flamegraph
execute it via either `cargo flamegraph` or simply `flamegraph` and provide the location to the executable.
Once you close veloren a `flamegraph.svg` file will be created you can open with your browser

## Visual Studio 2019 Comminity Edition (Windows only)

visual studio has a build in profiler, follow this tutorial and attach it to the running veloren program:
https://docs.microsoft.com/de-de/visualstudio/profiling/cpu-usage?view=vs-2019

## valgrind/cachegrind

you can use valgrind/cachegrind profiler to generate a output file and later analyse it via valgrind.
Tutorial: https://www.valgrind.org/docs/manual/cg-manual.html