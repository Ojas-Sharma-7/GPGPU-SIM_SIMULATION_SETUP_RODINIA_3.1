## GPGPU-Sim Installation Guide

This repository documents the **installation and setup procedure for
GPGPU-Sim** on a Linux system.\
It is intended as a **reference installation guide**, derived from the
official GPGPU-Sim documentation, with missing but essential steps added
for clarity and reproducibility.

Official GPGPU-Sim source repository :\
 https://github.com/gpgpu-sim/gpgpu-sim_distribution

------------------------------------------------------------------------

## About GPGPU-Sim

GPGPU-Sim is a cycle-level simulator for modern NVIDIA-like GPU
architectures.\
It enables detailed analysis of GPU microarchitecture, memory systems,
caches, and execution pipelines without requiring physical GPU hardware.


------------------------------------------------------------------------

## System Requirements

-   **Linux OS** (Ubuntu 18.04 / 20.04 / 22.04 recommended)
-   NVIDIA CUDA Toolkit (version compatible with GPGPU-Sim)
-   GCC / G++ compiler (may throw some error with gcc 9 , try to use 8 or lower version)
-   GNU Make and standard development tools

>  GPGPU-Sim is not supported on Windows or macOS.

------------------------------------------------------------------------

## Install Required Dependencies (Ubuntu/Debian)

Install all required system packages:

``` bash
sudo apt update
sudo apt install -y build-essential                     bison flex                     xutils-dev                     zlib1g-dev                     libglu1-mesa-dev                     libxml2-dev                     libboost-dev
```

These packages are required for: - Parsing and compilation -
OpenGL-based visualization support - Compression and trace handling

------------------------------------------------------------------------

##  Download GPGPU-Sim

Clone the official distribution repository:

``` bash
git clone https://github.com/gpgpu-sim/gpgpu-sim_distribution.git
cd gpgpu-sim_distribution
```

------------------------------------------------------------------------

## CUDA Toolkit Setup (CRITICAL STEP)

Ensure the CUDA Toolkit is installed on your system.

Typical installation path:

    /usr/local/cuda

You can verify CUDA installation using:

``` bash
nvcc --version
```

------------------------------------------------------------------------

###  Temporary CUDA Environment (Current Terminal Only)

``` bash
export CUDA_INSTALL_PATH=/usr/local/cuda
export PATH=$CUDA_INSTALL_PATH/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_INSTALL_PATH/lib64:$LD_LIBRARY_PATH
```

------------------------------------------------------------------------

### 🔹 Permanent CUDA Setup using `.bashrc` (RECOMMENDED)

Add CUDA paths permanently so they are available in every terminal
session.

Open `.bashrc`:

``` bash
nano ~/.bashrc
```

Append the following lines **at the end of the file**:

``` bash
# CUDA environment variables
export CUDA_INSTALL_PATH=/usr/local/cuda
export PATH=$CUDA_INSTALL_PATH/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_INSTALL_PATH/lib64:$LD_LIBRARY_PATH
```

Save and reload:

``` bash
source ~/.bashrc
```

Re-verify:

``` bash
nvcc --version
```

------------------------------------------------------------------------

##  Build GPGPU-Sim

Before building, source the GPGPU-Sim environment script:

``` bash
source setup_environment release
```

Now compile the simulator:

``` bash
make -j$(nproc)
```

### Build Modes

-   `release` → Faster execution (recommended)
-   `debug` → Debug symbols and assertions

Example for debug build:

``` bash
source setup_environment debug
make -j$(nproc)
```

------------------------------------------------------------------------

##  Installation Verification

A successful build will generate: - `libcuda.so` replacement libraries -
Simulator binaries - Configuration support files

No runtime execution is required at this stage to validate installation.

------------------------------------------------------------------------

##  Important Notes

-   Always **source `setup_environment`** before building or running
    simulations
-   CUDA version mismatch is the **most common installation issue**
-   GPGPU-Sim builds are CPU-intensive and may take several minutes
-   Avoid installing CUDA via Conda or user-space installers

------------------------------------------------------------------------

##  Reference

This installation procedure is based on the official GPGPU-Sim
documentation:

 https://github.com/gpgpu-sim/gpgpu-sim_distribution

------------------------------------------------------------------------

