# `mcp23S17`

> no_std driver for [MCP23S17](http://ww1.microchip.com/downloads/en/DeviceDoc/20001952C.pdf) (16-Bit SPI I/O Expander with Serial Interface module)

Note: This is a fork of the orginal MCP23017 repository and is **WORK IN PROGRESS**. Goal is to have a crate for the MCP23S17 which is functionaly the same as the MCP23017, but with an SPI interface.

<!--[![Build Status](https://github.com/lucazulian/mcp23017/workflows/mcp23017-ci/badge.svg)](https://github.com/lucazulian/mcp23017/actions?query=workflow%3Amcp23017-ci)
-->
<!--[![crates.io](http://meritbadge.herokuapp.com/mcp23017?style=flat-square)](https://crates.io/crates/mcp23017)
-->
[![Docs](https://docs.rs/mcp23017/badge.svg)](https://docs.rs/mcp23017)

## Basic usage

Include this [library](https://crates.io/crates/mcp23S17) as a dependency in your `Cargo.toml`:

```rust
[dependencies.mcp23S17]
version = "<version>"
```

Writing to all expansion pins:

```rust
    let chip_select_pi = todo!();
    let spi = todo!();

    let delay = todo!();
   
    let mut chip = MCP23S17::new(spi, chip_select_pin).unwrap();
    chip.all_pin_mode(mcp23s17::PinMode::OUTPUT).unwrap();

    chip.write_gpioab(0x0000_u16).unwrap(); // All pins low
    
    // Toggles the expansion pins
    loop {
        delay.delay_ms(200u16);
        chip.write_gpioab(0xFFFF_u16).unwrap(); // All pins high
        delay.delay_ms(300u16);
        chip.write_gpioab(0x0000_u16).unwrap(); // All pins low
    }
```

Reading from a single expansion pin:

```rust
    let chip_select_pi = todo!();
    let spi = todo!();
   
    let mut chip = mcp23s17::MCP23S17::new(spi, pin_cs).unwrap();

    let input_pin: u8 = 8;   // Expansion pin to read from
    chip.pin_mode(input_pin, mcp23s17::PinMode::INPUT).unwrap();
    chip.pull_up(input_pin, true).unwrap();

    let let r = chip.digital_read(input_pin).unwrap();
```

Read from all pins:
```rust
    let chip_select_pi = todo!();
    let spi = todo!();
   
    let mut chip = mcp23s17::MCP23S17::new(spi, pin_cs)
                   .unwrap();
        
    let reg: u16 = chip.read_gpioab().unwrap();     
```


## Hardware address pins
**TODO**


## Documentation

Not yet available.

<!--API Docs available on [docs.rs](https://docs.rs/mcp23017/0.1.0/mcp23017/)-->


## License

[MIT license](http://opensource.org/licenses/MIT)
