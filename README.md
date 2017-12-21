# bazo_client-android

## Build instructions

CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 \
CC=/.../my-android-toolchain/bin/clang go build .

