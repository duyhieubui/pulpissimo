# PULPissimo on the Digilent Arty A7 Board
[\[Documentation\]](https://reference.digilentinc.com/reference/programmable-logic/arty-a7/start)

## Bitstream Generation
In the `fpga` folder, run
```Shell
make arty-a7
```
which will generate `pulpissimo_arty-a7-100t.bit`.

## Bitstream Download
To download this bitstream into the FPGA connect the PROG USB header, turn the board on and run
```Shell
make -C pulpissimo-arty-a7 download
```
## Default Frequencies

By default the clock generating IPs are synthesized to provide the following frequencies to PULPissimo:

| Clock Domain   | Default Frequency on Genesys2 board |
|----------------|-------------------------------------|
| Core Frequency | 20 MHz                              |
| SoC Frequency  | 10 MHz                              |


## Peripherals
If in doubt please review constraint file for current peripheral mapping in `constraints/genesys2.xdc`.

PULPissimo is connected to the following board peripherals:


| PULPissimo Pin | Mapped Board Peripheral                             |
|----------------|-----------------------------------------------------|
| `SPIM0` pins   | QSPI Flash                                          |
| `I2C0` pins    | I2C Bus (connects to Board Current Measurement ICs) |
| `spim_csn1`    | LED0                                                |
| `cam_pclk`     | LED1                                                |
| `cam_hsync`    | LED2                                                |
| `cam_data0`    | LED3                                                |
| `cam_data1`    | Switch 1                                            |
| `cam_data2`    | Switch 2                                            |
| `cam_data3`    | Button C                                            |
| `cam_data4`    | Button D                                            |
| `cam_data5`    | Button L                                            |
| `cam_data6`    | Button R                                            |
| `cam_data7`    | Button U                                            |

### Reset Button
The USER RESET button (RSTN) resets the RISC-V CPU.

### UART
PULPissimo's UART port is mapped to the onboard FTDI FT232R USB-UART bridge and thus accessible through the UART micro-USB connector.

### JTAG
PULPIssimo's JTAG plug is connected to JA Pmod on the board. You will need an extermal
programmer such as Olimex ARM-USB-OCD-H JTAG debugger or an extermal FTDI 2232 programmer.
This is the provided OpenOCD configuration file for Olimex ARM-USB-OCD-H:

```Shell
$OPENOCD/bin/openocd -f pulpissimo/fpga/pulpissimo-arty-a7/openocd-olimex.cfg
```
