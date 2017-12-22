# bazo_client-android
This repository stores and documents the port of the bazo miner and client to the android platform

## Prerequisites
In order to build the binaries for the android platform one needs to have the arm compiler for the android platform. The following sections give instructions on how to build the compiler for android and how to cross-compile the bazo binaries.

## Build instructions

### Building the toolchain

### Cross-compiling the actual applications

CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 \
CC=/.../my-android-toolchain/bin/clang go build .

## Deploying the binaries

In order to run the compiled binaries on a compatible arm-device running android the following possibilities exist:

* Use `adb push` to copy the files to an android device. Use `adb shell` to open a new shell and then `run-as` to run the binaries in the scope of an existing application.

* Copy the files to a rooted android phone and run them directly

* Place the binaries in the assets folder of an android application. At runtime, let the application copy the files to `/data/<app>` and run them.

