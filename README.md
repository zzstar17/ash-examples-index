# Collection of Ash Examples

This is a collection of [Vulkan®](https://www.khronos.org/vulkan/) examples created with [Ash](https://github.com/ash-rs/ash) as its wrapper API. It is aimed to be similar to the official [Vulkan Samples](https://github.com/KhronosGroup/Vulkan-Samples).

Each example has its own `README.md` that explains explains some of the Vulkan functionality and how it is applied in the context of the example's code. Most of it is meant to be introductory but may be incomplete from a beginner's perspective, so I try to link other sources that may explain the technical parts better.

Each example exists in a separate git submodule. You can clone all examples with `git clone --recurse-submodules https://github.com/zzstar17/ash-examples-index` or clone and initialize submodules individually with `git submodule init <path>`.

Feel free to suggest new examples or improvements for old ones.

## Table of Contents

- [Instance creation](https://github.com/zzstar17/ash-examples/tree/3e81f321962bbb18e3fcc2655edc7c58df253d39) (/instance): Covers Instance creation and enabling validation layers.
- [Device creation](https://github.com/zzstar17/ash-examples/tree/5dd2f7663dae068a5c1b777508aeacc1fc34d494) (/device): Covers physical device selection, logical device creation and queue retrieval.
- [Compute image clear](https://github.com/zzstar17/ash-examples/tree/7abcb45458f02abf948ca3cc8795aee2514a1433) (/clear_image): Clears an image, copies it from device memory to host accessible (CPU) memory and saves it to a file. This example covers command buffer creation, buffer and image allocations, image layout transitions with image barriers, queue family ownership transfer and queue submission.
- [Storage image compute shader](https://github.com/zzstar17/ash-examples/tree/306e3cc3b4b4294f496810c148f5a0ca5ade249a) (/mandelbrot): Generates the Mandelbrot Set offline by using a compute shader on a storage image and saves it to a file. This example covers compute pipeline creation, pipeline caches, descriptor sets and compute shaders. It also demonstrates the use of specialization constants in order to assign constant values in the shader during pipeline creation.
- [Triangle image](https://github.com/zzstar17/ash-examples/tree/3ff9d6d75d336319c652a6336da638826144a245) (/triangle_image): Draws a triangle and saves it to a file. Covers executing a simple graphics pipeline with a render pass, vertex and index buffers.
- [Bouncing texture](https://github.com/zzstar17/ash-examples/tree/d8614d324cfa2738d9a7cb0ce4507a17464cbd7e) (/bouncy_ferris): Drag Ferris the crab around and make it bounce around the screen. Applies a texture to an image and draws first to a separate image, then to the swapchain each frame. Introduces rendering to windows with a swapchain as well as sampling images.
- [Compute instanced draw](https://github.com/zzstar17/ash-examples/tree/9a279eae9e4f1136d8dc8bd2bdde1cd374540062) (/instance_draw): A separate compute thread updates positions for a set of particles, after which it passes those positions to be rendered in the main thread. This example is not yet fully complete.

## Building and running

Running the examples requires the nightly Rust Toolchain (`rustup default nightly`) as well as the [Vulkan SDK](https://www.lunarg.com/vulkan-sdk/).

Each example uses a set of cargo features that can be enabled or disabled to toggle specific functionality, which you can customize by using the `--features` flag.

To run an example with all validations enabled, navigate to the respective folder and run:

```bash
RUST_LOG=debug cargo run
```

To run an example with validation layers disabled and with optimizations, navigate to the respective folder and run:

```bash
cargo run --release --no-default-features --features link
```

The `link` / `load` features specify if the Vulkan Loader shall be linked at runtime or compile time (see https://docs.vulkan.org/guide/latest/loader.html). `vl` enables the use of validation layers. More information, as well as the list of default cargo features can be found in the respective example's README.

## Checking the logs

Every example uses the [log](https://github.com/rust-lang/log) crate with [env_logger](https://docs.rs/env_logger/latest/env_logger/) as its facade implementation. This means that, for example, the validation layers (if enabled) will only show errors by default.

Different levels of visibility can be changed with the environment variable `RUST_LOG`, so if
for example you want to see all error, warning, info and debug messages, just run the executable preceding
it with `RUST_LOG=debug`. You can find more information at [https://docs.rs/env_logger/0latest/env_logger/](https://docs.rs/env_logger/latest/env_logger/).
