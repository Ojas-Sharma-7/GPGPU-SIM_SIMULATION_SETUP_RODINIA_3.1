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
nvcc --cudart shared -o hello hello.cu
```
------------------------------------------------------------------------

## 🔍 3. Verify CUDA Runtime Linking

Check that the executable links against libcudart.so:
```bash
ldd hello
```
📸 Expected Output (Reference Image)
[v2-0082a419b7b3d2ddc3fc6bb021e7eab6-b.png](https://postimg.cc/c6x0drsx)

if you are unable to see this then , you have to follow the below mentioned steps to make it happen as it is neccesary to have these files for exceution of the program 
