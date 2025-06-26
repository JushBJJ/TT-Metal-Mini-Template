# tt-metal Project Template

This is a minimal CMake template to kickstart your tt-metal projects.

It as simple and clean as it can get. If it doesnt work on the latest tt-metal commit, you might have to tinker a bit.


## Other Useful Templates
- [Marty's ttnn hello-world C++ template](https://github.com/marty1885/ttnn-helloworld-cpp)
- [Tenstorrent's ttnn C++ project template](https://github.com/tenstorrent/cpp-ttnn-project-template)

## Setup
Before building, make sure you’ve [built and installed tt-metal](https://github.com/tenstorrent/tt-metal/blob/main/INSTALLING.md) and set the `TT_METAL_HOME` and `CXX` env variables:

```sh
export TT_METAL_HOME=/path/to/tt-metal
export CXX=/usr/bin/clang++-17 # or g++
```

## Build and Compile
```sh
cmake -S . -B build
make -C build
```

## Running your Project
```sh
./build/my_foo
```

If kernels aren’t found, check they’re in the right path (e.g., `./kernels/`).
