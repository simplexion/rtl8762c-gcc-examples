# RTL8762C GCC Examples
Firmware examples for the RTL8762C BLE SoC

[![hackaday.io](https://img.shields.io/badge/hackaday-io-gold.svg)](https://hackaday.io/project/182205-py-ft10)

## Download
To obtain this code, clone this repository recursively.
```shell
git clone --recurse-submodules https://github.com/cyber-murmel/rtl8762c-gcc-examples.git
```

## Toolchain
To build the firmware you need
- [GNU Make](https://ftp.gnu.org/gnu/make/) 4.3
- [arm-none-eabi-gcc](https://developer.arm.com/downloads/-/gnu-rm) (GNU Arm Embedded Toolchain 10.3-2021.10) 10.3.1 20210824 (release)

You additionally need to install some Python libraries and download the vendor SDK and MPTool files.

### Nix
Users of Nix or NixOS can simply run `nix-shell` to enter an environment with all necessary binaries and Python libraries. You then only need to download the vendor
files.

### Python modules
The tools used depend on the python modules listed in the `pyproject.toml`.
Run the following in the root of this repository to create a development environment
and install the dependencies.
```shell
poetry shell
poetry install
```

To enter the environment again, just run `poetry shell` in the root of this repository.

### Vendor Files
You need to register an account at [RealMCU](https://www.realmcu.com).
This requires an email address.

#### SDK
Download the *RTL8762C SDK GCC(ZIP)* from the 
[product page](https://www.realmcu.com/en/Home/Product/93cc0582-3a3f-4ea8-82ea-76c6504e478a).

Extract the zip archive and move the `sdk` directory into the root of this repository.

```shell
unzip RTL8762C-sdk-gcc-v0.0.5.zip
mv bee2-sdk-gcc-v0.0.5/sdk ./sdk
rm -r bee2-sdk-gcc-v0.0.5
```

#### MP Tool Kits
Download the RTL8762x MP Tool Kits(ZIP) from the vendor page and place it in the tools/rtltool/rtl8762c/ directory.

## Building
To build an example, set `TARGET` to one of the directories in [src/targets](src/targets) and run make.

```shell
make TARGET=00-blink
```

The default `TARGET` is `00-blink`

Currently available targets are
- `00-blink`
- `01-uart_echo`
- `02-uart_printf`

### Cleanup
It's advised to clean up build results before switching to a different target.

```shell
make clean
```

## Flashing
To flash the firmware onto the board via UART, run

```shell
make TARGET=00-blink flash
```

### Port
The UART port can be be set via the `PORT` variable.

```shell
make TARGET=00-blink PORT=/dev/ttyUSB0 flash
```

The default `PORT` is `/dev/ttyUSB1`

## Terminal
To open a miniterm session, run

```shell
make term
```

The port can be changed in the same way as for [flashing](#port).
