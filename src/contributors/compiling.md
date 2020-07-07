# Compiling Veloren

This section covers building Veloren from rust source with `cargo` and running it.

**Note**: _all commands need to be run from the repository._

## Compile and Run Veloren

Run this in a terminal to compile and run Veloren:

```bash
cargo run
```

To compile without running, use `cargo build` instead.

**Note**: _The initial compilation will take from 5min up to 30min therefore grab a tea and some snacks and come back later._

## Compile and Run Veloren Server

```bash
cargo run --bin veloren-server-cli
```

## Logging output

We use [`tracing`](https://crates.io/crates/tracing) to collect logs. They can be filtered by setting the `RUST_LOG` environment variable to the respective level (`error`, `warn`, `info`, `debug`, `trace`).

For all available filtering options visit [the docs](https://docs.rs/tracing-subscriber/0.2.7/tracing_subscriber/filter/struct.EnvFilter.html#examples).

**Tip**: _this works both for the server and client_

## Optimized Release builds

By default debug builds are created which compile faster but run a bit slower than optimized release builds. Unlike many other projects, we've set them up so they're fast enough to be playable. If you want to get optimized builds, add the `--release` flag when calling `cargo`. Keep in mind that compiling release might be very slow!

If you want get familiar with cargo we recommend the [Cargo Book](https://doc.rust-lang.org/cargo/).
