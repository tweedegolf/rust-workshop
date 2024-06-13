# Unit 8.1 - The Rust embedded ecosystem

<a href="/slides/8_1/" target="_blank">Slides</a>

## Exercise 8.1.1: LIS3DH ID
Use our newly gained knowledge to get our first application running and read out the ID of the LIS3DH accelerometer.

To get started we'll setup the i2c on our development kit and read out the ID register of the LIS3DH accelerometer.
The starting point can be found in the file at `exercises/8-embedded/1-embedded-ecosystem/1-lis3dh-id/src/main.rs` in the [repository](https:://github.com/tweedegolf/rust-training).

Try to run the existing project and then fill in the functionality as instructed by the comments.

To use that project, you can use the following commands from inside that folder using the terminal:
- `cargo build`: Builds the project
- `cargo run`: Builds the project, flashes it to the device and listens for any logs which it will display in the terminal. (This uses the `probe-rs run` tool)

In both cases you can add the `--release` flag to turn on optimizations.

<details>
    <summary><b>Some pointers to help you get started</b></summary>

- You can find the documentation on the HAL here on [docs.rs](https://docs.rs/nrf52840-hal/latest/nrf52840_hal/). This website aggregates documentation on virtually every crate published on <https://crates.io>.
- To find out how to configure I2C for the nRF52840: [nrf-hal TWIM demo example](https://github.com/nrf-rs/nrf-hal/blob/master/examples/twim-demo/src/main.rs). Note that this example is based on a runtime called RTIC, which we are not using here. Therefore, you cannot simply copy the code into your source file. Wherever you see `ctx.device` in the example code, you can replace it with `dp`. It's the same thing.
- You can find the LIS3DH data sheet here: <https://www.st.com/resource/en/datasheet/lis3dh.pdf>. You can find the device ID in the `WHO_AM_I` register, at register address `0x0F`. Depending on which exact LIS3DH breakout board you are using, you will need to use either `0x18` or `0x19` to address the LIS3DH
- Use the [`Twim::write_then_read`](https://docs.rs/nrf52840-hal/latest/nrf52840_hal/twim/struct.Twim.html#method.write_then_read) method to first write the device address, then write the register address, and then read its contents into a buffer. 
</details>