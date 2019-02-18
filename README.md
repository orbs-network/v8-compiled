# V8 Compiled
> The aim of this repo is to store the compiled verion of V8 library (not executable) in releases for the use in other projects.

V8 is Google's open source project. As a result of it, V8's toolchain contains some parts of overall Google toolchain. It's not that straigtforvard, Without prior knowledge, to compile V8 as a library. 

Below is a small step-by-step description for common actions.

## How to clone
1. Clone the repo `git clone https://github.com/bolshchikov/v8-compiled.git`
1. Add depot_tools to the path `PATH=$PATH:$PWD/depot_tools`
1. Clone v8 `fetch v8`

## How to update
1. Add depot_tools to the path `PATH=$PATH:$PWD/depot_tools`
1. Enter v8 directory `cd v8`
1. Pull changes `gil pull`
1. Update dependencies `gclient sync`

## How to compile
1. Add depot_tools to the path `PATH=$PATH:$PWD/depot_tools`
1. Enter v8 directory `cd v8`
1. Checkout the desired version, e.g. `git checkout 7.4.166`
1. Generate build configuration `gn args out/<version.number>` and paste [build flags](./v8build-flags)
1. Run the build `ninja -C out/<version.number> v8_monolith`

## Release
1. Copy `include` folder to the build folder `cp -rf ./v8/include/ ./v8/out/<version.number>/include`
1. Create archive out of build folder `tar -zcvf ./binary/<version.number>.tar.gz ./v8/out/<version.number>/`
1. Create checksum on archive file `echo ./binary/<version.number>.tar.gz | openssl dgst -sha256 >> ./binary/checksum.txt`
1. Create a new release in github with the `<version.number>` and upload `binary` folder content to it.