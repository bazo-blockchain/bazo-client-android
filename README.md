# bazo_client-android


## Prerequisites
In order to build the binaries for the android platform one needs to have the arm compiler for the android platform as well as the golang runtime. 

## Build instructions

### Building the toolchain

Please follow the <a href="https://developer.android.com/ndk/guides/standalone_toolchain.html">official documentation</a> on how to obtain a toolchain for ndk development.

### Cross-compiling the actual applications

Now, setup your go environment so that the newly created compiler is used. The following command shows how the compilation is configured and started. Navigate to the projects source code and run:

```
CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 \
CC=<path to your ndk toolchain>/bin/clang go build .
```

## Deploying the binaries

In order to run the compiled binaries on a compatible arm-device running android the following possibilities exist:

* Use `adb push` to copy the files to an android device. Use `adb shell` to open a new shell and then `run-as` to run the binaries in the scope of an existing application.

* Copy the files to a rooted android phone and run them directly

* Place the binaries in the assets folder of an android application. At runtime, let the application copy the files to `/data/<app>` and run them.

## Running the binaries

Run the binaries as usual. The following commands show how the binaries can be run with the supplied sample setup. This setup consists of two non-root users and a root account. All accounts have >100 Bazo coins of Funds at the beginning.

```
./bin/bazo_miner-android-armv5 ./sample-setup/database :8000 > miner.log &
```
```
./bin/bazo_client-android-armv5 &
```
If the binaries are required for running the Bazo Wallet or other applications that depend on a secure context, a secure tunnel is necessary. <a href="https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm.zip">ngrok</a> can be used to create a secure connection and provides an ARMv5 binary suitable for most android devices:

`./ngrok http 8001`

