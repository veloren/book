# Generating Docs

Once you have the main Veloren repository cloned locally and Rust installed, it is possible to generate and view the project documentation by running the following command from the `voxygen/` directory:

```
cargo doc --open --features gl
```

This command will automatically open the documentation in your web browser when it has finished generating. The documentation is organised by crate and gives an overview as to what each trait/function/type is for, how it may be used, and in what scenario it is appropriate to be used for.

Generally speaking, we only require publicly-visible interfaces to be documented fully, but it is encouraged to add documentation comments to non-public interfaces too.