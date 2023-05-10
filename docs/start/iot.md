---
description: Get started with Operational Technology and Internet of Things
---

# OT / IoT

## Overview

This page is aimed at getting you up and running with Atsign's technology on your IoT device. For a more general overview of Atsign's technology and IoT, see [here](https://atsign.com/iot-internet-of-things).

## Off-the-shelf solutions

We aim to provide off-the-shelf solutions for the most-frequently-required use cases so you can gain all of the benefits of device security, data security and end-to-end encryption without having to embark on a software development project.

### Available now

#### Ssh! No ports

Our first production ready solution is [SSH! No ports](../solutions/sshnp/), which provides a way to ssh to a remote linux host/device without that device having any open ports (not even 22) on external interfaces. All network connectivity is outbound and there is no need to know the IP address the device has been given. As long as the device has an IP address, DNS and Internet access, you will be able to connect to it.

Downloads are available [here](https://github.com/atsign-foundation/sshnoports/releases).

### Coming soon

Solutions in development.

#### MQTT Bridge

Many IoT devices already use MQTT to move data. at\_mqtt\_bridge is a convenient way to take messages from MQTT topics and transmit them securely from the device to anywhere else on the internet via the atPlatform.

#### IoT Dashboard Bridge

Send your device's data to any or all of:

* Azure IoT Hub
* Google Cloud IoT Core
* AWS IoT Device Management
* ThingsBoard

## Supported Platforms

All of our solutions are available as pre-built binaries and as docker images, for most Linux runtimes including Raspberry Pi 4:

* linux-x64
* linux-arm
* linux-arm64

Our solutions for Linux were developed using our core Dart SDK. We are actively working on SDKs for much more resource-constrained platforms which do not currently have Dart support

* MicroPython SDK
  * e.g. for the Raspberry Pi Pico W
* [C SDK](https://github.com/atsign-foundation/at\_c) for ESP32
  * We do also have an [Arduino-based implementation for ESP32](https://github.com/atsign-foundation/at\_esp32) but we are working on deprecating this in favor of the cross-platform C SDK

### Don't See your platform?

Please contact us! We want to support every platform that we possibly can.

## Custom Solutions

If our off-the-shelf solutions don’t meet your needs, you can create your own solutions using one of our [SDKs](../learn/sdk/).

Currently supported languages include:

* &#x20;Dart - our core SDK, with support for Intel and ARM 32- and 64-bit architectures, as well as support for the RISC-V architecture in Dart 3 (currently in beta)
  * The Flutter framework allows you to build cross-platform apps for iOS, Android and Mac OS X, Linux and Windows desktops
* Java
* \[Coming Soon] MicroPython
* \[Coming Soon] C / C++

To help you get started, in addition to the SDK documentation itself, we also have several open-source examples that you can use as a basis for your solution.

* [SSH! No ports](../solutions/sshnp/)
* [GPS demo](https://github.com/atsign-foundation/at\_gps\_demo) - end to end encrypted GPS using gpsd and thingsboard as the end points
* [at\_nautel\_snmp](https://github.com/cconstab/at\_nautel\_snmp) - Monitor a Nautel Transmitter securely, via the atPlatform
* [catweb](https://github.com/cconstab/catweb) - for ham radio operators to provide near real-time frequency and modulation mode being used to a website, so other operators know where you are listening
* [MWC demo](https://github.com/atsign-foundation/mwc\_demo) - a demo we built for the Mobile World Congress in 2022 which links a Max30101 sensor, a Raspberry Pi and the atPlatform
* [at\_talk](https://github.com/atsign-foundation/at\_talk) a very simple end-to-end-encrypted command line chat client in homage to Unix talk
