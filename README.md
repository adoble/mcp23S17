# `mcp23S17`

> no_std driver for [MCP23S17](http://ww1.microchip.com/downloads/en/DeviceDoc/20001952C.pdf) (16-Bit SPI I/O Expander with Serial Interface module)

**Note: This is an early fork of the orginal MCP23017 repository and is WORK IN PROGRESS. Goal is to have a crate for the MCP23S17 which is functionaly the same as the MCP23017, but with an SPI interface.**

<!--[![Build Status](https://github.com/lucazulian/mcp23017/workflows/mcp23017-ci/badge.svg)](https://github.com/lucazulian/mcp23017/actions?query=workflow%3Amcp23017-ci)
-->
<!--[![crates.io](http://meritbadge.herokuapp.com/mcp23017?style=flat-square)](https://crates.io/crates/mcp23017)
-->
[![Docs](https://docs.rs/mcp23017/badge.svg)](https://docs.rs/mcp23017)

## Basic usage

**Note: This is a sketch of the API. It tries to preserve the API of the MCP23017 crate as much as possible**

Include this [library](https://crates.io/crates/mcp23S17) as a dependency in your `Cargo.toml`:

```rust
[dependencies.mcp23S17]
version = "<version>"
```
Use [embedded-hal](https://github.com/rust-embedded/embedded-hal) implementation to get SPI handle and then create mcp23S17 handle:

```rust
extern crate mcp23S17;

match mcp23S17::MCP23S17::default(spi) {
    Ok(mut u) => {
        u.init_hardware();
        u.pin_mode(1, mcp23S17::PinMode::OUTPUT);   // for the first pin
        u.all_pin_mode(mcp23S17::PinMode::OUTPUT);  // or for all pins

        let status = u.read_gpioab().unwrap();
        println!("all {:#?}", status).unwrap();

        let read_a = u.read_gpio(mcp23S17::Port::GPIOA).unwrap();
        println!("port a {:#?}", read_a).unwrap();

        match u.write_gpioab(65503){
            Ok(_) => {
                println!("ok").unwrap();
            }
            _ => {
                println!("something wrong").unwrap();
            }
        }
    }
    Err(mcp23S17::MCP23S17::Error::BusError(error)) => {
        println!("{:#?}", error).unwrap();;
        panic!();
    }
    _ => {
        panic!();
    }
};
```

### Hardware address pins
![](docs/address-pins.jpg)

## Documentation

Not yet available.

<!--API Docs available on [docs.rs](https://docs.rs/mcp23017/0.1.0/mcp23017/)-->

## License

[MIT license](http://opensource.org/licenses/MIT)
