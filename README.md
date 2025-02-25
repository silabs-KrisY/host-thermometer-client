# host-thermometer-client

This is a Linux/Posix BGAPI host application version of the soc-thermometer-client example in the Silicon Labs Blue Gecko Bluetooth SDK for EFR32 devices. It communicates with a serial Blue Gecko NCP device via BGAPI, connects using BLE to devices implementing (and advertising) the GATT server role of the Health Thermometer Profile, and prints the RSSI and temperature readings from each server device when they arrive.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

1. Blue Gecko SDK (installed via Simplicity Studio).
2. Linux/Posix build environment (OSX, Cygwin, Raspberry Pi, etc.).
3. Blue Gecko / Mighty Gecko device running a serial UART NCP (Network Co-Processor) firmware image. See the "To Run" section below for more details.
4. One or more devices implementing (and advertising) the GATT server role of the Health Thermometer Profile. See the "To Run" secton below for more details.

### Installing

This project can be built as supplied within the Blue Gecko SDK frameworks.

#### For Cygwin/OSX/Linux with SDK installed

Clone or copy the contents of this repository into the Blue Gecko SDK, into a subfolder of app/bluetooth/examples_ncp_host. Commands shown here are from OSX using Gecko SDK Suite v2.6, but will be similar in Linux/Cygwin.

```
$ cd /Applications/SimplicityStudiov4.app/Contents/Eclipse/developer/sdks/gecko_sdk_suite/v2.6/app/bluetooth/examples_ncp_host/
$ git clone https://github.com/kryoung-silabs/host-thermometer-client.git
$ cd host-thermometer-client
$ make
```

#### For Raspberry Pi

1. On the host with SDK installed, create a compressed file archive containing the required SDK source files (command line example here on OS X using Gecko SDK Suite v2.6).

```
$ cd /Applications/SimplicityStudiov4.app/Contents/Eclipse/developer/sdks/gecko_sdk_suite/v2.6
$ tar -cvf ble_2_12_2.tgz "protocol/bluetooth/ble_stack/inc" "protocol/bluetooth/ble_stack/src" "app/bluetooth/examples_ncp_host/common"
```

You can also create a zip archive including the same files/paths using your favorite Windows Zip tool (7zip, etc.). Make sure you preserve paths relative to the Gecko SDK root when creating the archive!

2. Transfer archive to Raspberry Pi, extract, cd to the new directory, and make.

```
$ mkdir blue_gecko_sdk_v2p12p2
$ tar -xvf ble_2_12_2.tgz -C blue_gecko_sdk_v2p12p2
$ cd blue_gecko_sdk_v2p12p2/app/bluetooth/examples_ncp_host/
$ git clone https://github.com/kryoung-silabs/host-thermometer-client.git
$ cd host-thermometer-client
$ make
```

If using a zip archive with preserved paths relative to the Gecko SDK root, the extraction process is as follows:
```
$ mkdir blue_gecko_sdk_v2p12p2
$ unzip ble_2_12_2.tgz -d blue_gecko_sdk_v2p12p2
```

#### To Run

1. Program your NCP image "ncp-empty-target" into your target. Instructions on how to implement this, both on custom hardware and on Silicon Labs wireless starter kit (WSTK) radio boards are provided in [AN1092: Using the Silicon Labs Bluetooth(R) Stack in Network Co-Processor Mode](https://www.silabs.com/documents/login/application-notes/an1042-bt-ncp-mode.pdf).
2. Prepare one or more devices running the soc-thermometer firmware or equivalent device implementing Health Thermometer service. Silicon Labs provides pre-built and customizable versions of this firmware as the "SOC - Thermometer" example project that will run on Silicon Labs wireless starter kit (WSTK) radio boards. Instructions on how to build and run SiLabs Bluetooth example projects (including "SOC - Thermometer" is described in [QSG139: Getting Started with Bluetooth Software Development](https://www.silabs.com/documents/public/quick-start-guides/qsg139-getting-started-with-bluetooth.pdf).
3. Connect your Blue Gecko serial NCP device ("ncp-empty-target") to the host (via USB, uart, etc.).
4. Run the application, pointing to the correct serial port. The command line is:
```
Usage: thermometer-client <serial port> <baud rate> [flow control: 1(on, default) or 0(off)]
```

Here's an example using Raspberry Pi with the target NCP running on a WSTK radio board and connected to the Raspberry Pi via USB virtual COM port:

```
$ ./exe/thermometer-client /dev/ttyACM0 115200 1
Starting up...
Resetting NCP target...

BLE Central started
```

Here's a similar example using Cygwin:

```
$ ./exe/thermometer-client.exe COM43 115200 1
Starting up...
Resetting NCP target...

BLE Central started
```

If you have one or more soc-thermometer servers advertising, you will see a table with the RSSI and temperature reading from each.

```
ADDR  TEMP   RSSI |ADDR  TEMP   RSSI |ADDR  TEMP   RSSI |ADDR  TEMP   RSSI |
2a9b 29.90C -28dBm|0000  0.00C   0dBm|0000  0.00C   0dBm|0000  0.00C   0dBm|
```

## Deployment

For a commercially deployed system (i.e. embedded gateway, etc.), use the supplied makefile and source files from the Blue Gecko SDK to cross-compile for the desired platform.

## Support

I am a Field Applications Engineer for Silicon Labs, not a full time software developer, so I've created this application in my "spare time" to provide an example for Silicon Labs customers to use to bring up their hardware, do some testing, and perhaps form as the basis to extend with additional functionality. If needed, I can provide limited support for this specific software via email <<kris.young@silabs.com>>. For support on building NCP firmware images, bringing up NCP firmware, and building target firmware images using examples under Simplicity Studio, please obtain support through the [official Silicon Labs support portal](http://silabs.com/support).

## Versioning

I plan to use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/host-thermometer-client/tags). All notable changes to this project will be documented in [CHANGELOG.md](CHANGELOG.md).

## Authors

* **Kris Young** - *Initial work* - [Kris Young](https://github.com/kryoung-silabs) <<kris.young@silabs.com>>

## License

This AS-IS example project is licensed under the standard Silicon Labs software license. See the [LICENSE.md](LICENSE.md) file for details
