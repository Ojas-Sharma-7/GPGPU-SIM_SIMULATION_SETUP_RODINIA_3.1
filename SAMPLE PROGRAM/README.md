# ▶️ Running and Compiling a CUDA Program on GPGPU-Sim

This document explains how to **compile and run a CUDA program on GPGPU-Sim** after the simulator has been successfully installed and built.

---

## 📁 1. Program Location

Place your CUDA program (for example `hello.cu`) in a separate directory:

```bash
mkdir ~/gpgpu_sim_runs
cp hello.cu ~/gpgpu_sim_runs/
cd ~/gpgpu_sim_runs/
```
------------------------------------------------------------------------
## 🛠️ 2. Compile the CUDA Program

The program must be compiled with shared CUDA runtime so that GPGPU-Sim can intercept CUDA calls.
```bash
nvcc --cudart shared -o your_program your_program.cu
```
------------------------------------------------------------------------

## 🔍 3. Verify CUDA Runtime Linking

Check that the executable links against libcudart.so:
```bash
ldd your_program
```
📸 Expected Output (Reference Image)
[v2-0082a419b7b3d2ddc3fc6bb021e7eab6-b.png](https://postimg.cc/c6x0drsx)

if you are unable to see this then , you have to follow the below mentioned steps to make it happen as it is neccesary to have these files for exceution of the program 

```bash 
sudo ln -s /home/project/gpgpu-sim_distribution/lib/gcc-8.4.0/cuda-10010/release/libcuda.so lib/libcuda.so
sudo ln -s /home/project/gpgpu-sim_distribution/lib/gcc-8.4.0/cuda-10010/release/libcuda.so libcuda.so
sudo ln -s /home/project/gpgpu-sim_distribution/lib/gcc-8.4.0/cuda-10010/release/libcudart.so.10.1 lib/libcudart.so.10.1
nvcc --cudart shared -o your_program your_program.cu
ldd your_program
```
this will link the required libcudart.so files to your GPGPU-SIM , make sure to change the CUDA Version and the gcc version that you are using in the syntax while compiling your program 
------------------------------------------------------------------------

## 🧾 4. Copy GPGPU-Sim Configuration Files

GPGPU-Sim requires architecture configuration files.

Example (GTX480):
```bash
cp -r /path/to/gpgpu-sim_distribution/configs/GTX480/* .
```
------------------------------------------------------------------------

## 🌱 5. Source the GPGPU-Sim Environment

Before running the program, source the simulator environment:


``` bash
source /path/to/gpgpu-sim_distribution/setup_environment release
```
or could the same in the GPGPU-SIM distribution directory 

```bash
source setup_environment
```
------------------------------------------------------------------------

## ▶️ 6. Run the Program

Execute the compiled binary:

```bash
./your_program
```
------------------------------------------------------------------------
