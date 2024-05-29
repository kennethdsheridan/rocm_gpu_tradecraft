# Radeon Open Compute Tradecraft
This is a collection of Radeon Open Compute (ROCm) commnds, best practices and what not that will make you more confident with the AMD ROCm toolkit. And assist in transitioning from CUDA, over to a community driven parallel programming ecoystem you have control over. 

Welcome to the future folks...lets get started.

## Table of Contents

- [Radeon Open Compute Tradecraft](#radeon-open-compute-tradecraft)
  - [ROCm Tradecraft for GPU Performance Tuning](#rocm-tradecraft-for-gpu-performance-tuning)
    - [System Setup and Installation](#system-setup-and-installation)
      - [Installing ROCm](#installing-rocm)
      - [Adding ROCm Repository](#adding-rocm-repository)
      - [Installing ROCm Components](#installing-rocm-components)
  - [ROCm Component Packages](#rocm-component-packages)
    - [rocm-dev](#rocm-dev)
    - [rocm-utils](#rocm-utils)
    - [rocm-libs](#rocm-libs)
    - [miopen-hip](#miopen-hip)
  - [Monitoring and Managing GPU Usage](#monitoring-and-managing-gpu-usage)
    - [Listing Available GPUs](#listing-available-gpus)
    - [Monitoring GPU Utilization](#monitoring-gpu-utilization)
    - [Checking GPU Temperature](#checking-gpu-temperature)
    - [Checking GPU Power Consumption](#checking-gpu-power-consumption)
    - [Checking GPU Fan Speed](#checking-gpu-fan-speed)
    - [Checking GPU Clock Frequencies](#checking-gpu-clock-frequencies)
  - [GPU Performance Tuning](#gpu-performance-tuning)
    - [Setting GPU Power Profile](#setting-gpu-power-profile)
    - [Setting GPU Fan Speed](#setting-gpu-fan-speed)
    - [Setting GPU Memory Clock](#setting-gpu-memory-clock)
    - [Setting GPU Performance Level](#setting-gpu-performance-level)
  - [Diagnostics and Debugging](#diagnostics-and-debugging)
    - [Checking GPU Health](#checking-gpu-health)
    - [Resetting GPU](#resetting-gpu)
    - [Saving GPU Logs](#saving-gpu-logs)
    - [Clearing GPU Logs](#clearing-gpu-logs)
  - [GPU Memory Management](#gpu-memory-management)
    - [Checking GPU Memory Usage](#checking-gpu-memory-usage)
    - [Clearing GPU Memory](#clearing-gpu-memory)
  - [Advanced GPU Configuration](#advanced-gpu-configuration)
    - [Overclocking GPU](#overclocking-gpu)
    - [Underclocking GPU](#underclocking-gpu)
    - [Setting Power Cap](#setting-power-cap)
  - [ROCm-SMI Commands Summary](#rocm-smi-commands-summary)
    - [General Information](#general-information)
    - [Temperature and Fan](#temperature-and-fan)
    - [Power and Performance](#power-and-performance)
    - [Clock Speeds](#clock-speeds)
    - [Memory](#memory)
    - [Logs and Health](#logs-and-health)
    - [Reset](#reset)
  - [Development Tools](#development-tools)
    - [Installing HIP](#installing-hip)
    - [Compiling HIP Programs](#compiling-hip-programs)
    - [Running HIP Programs](#running-hip-programs)
    - [Using ROCm Libraries](#using-rocm-libraries)
  - [Performance Tuning and Benchmarking](#performance-tuning-and-benchmarking)
    - [Installing ROCm Bandwidth Test](#installing-rocm-bandwidth-test)
    - [Running Bandwidth Test](#running-bandwidth-test)
    - [Using rocprof for Profiling](#using-rocprof-for-profiling)
    - [Using rocminfo for System Information](#using-rocminfo-for-system-information)
  - [RoCE and GPU Network Fabrics](#roce-and-gpu-network-fabrics)
    - [Installing RDMA Tools](#installing-rdma-tools)
    - [Configuring RoCE](#configuring-roce)
    - [Checking RDMA Devices](#checking-rdma-devices)
    - [Displaying RDMA Configuration](#displaying-rdma-configuration)
    - [Setting Up RDMA Over TCP/IP](#setting-up-rdma-over-tcpip)
    - [Listing RDMA Interfaces](#listing-rdma-interfaces)
    - [Running RDMA Bandwidth Test](#running-rdma-bandwidth-test)
    - [RDMA Latency Test](#rdma-latency-test)
    - [Connecting RDMA Devices](#connecting-rdma-devices)
    - [Using rping for RDMA Connectivity Testing](#using-rping-for-rdma-connectivity-testing)
      - [Server-side](#server-side)
      - [Client-side](#client-side)
    - [Configuring QoS for RDMA Traffic](#configuring-qos-for-rdma-traffic)
    - [Setting up RDMA Multicast](#setting-up-rdma-multicast)
    - [Monitoring RDMA Traffic](#monitoring-rdma-traffic)
  - [Performance and Benchmarking Cookbook Using ROCm, RDMA, and RoCE](#performance-and-benchmarking-cookbook-using-rocm-rdma-and-roce)
    - [Installing Required Tools](#installing-required-tools)
    - [Basic Performance Testing](#basic-performance-testing)
    - [Profiling Applications with rocprof](#profiling-applications-with-rocprof)
    - [Using rocminfo for System Information](#using-rocminfo-for-system-information)
    - [RDMA and RoCE Performance Testing](#rdma-and-roce-performance-testing)
    - [Advanced Performance Benchmarking](#advanced-performance-benchmarking)
      - [Using rocblas-bench for BLAS Performance](#using-rocblas-bench-for-blas-performance)
      - [Using rocFFT for FFT Performance](#using-rocfft-for-fft-performance)
      - [Using RVS (ROCm Validation Suite)](#using-rvs-rocm-validation-suite)
        - [Example Configuration for RVS Stress Test](#example-configuration-for-rvs-stress-test)
        - [Running the Stress Test](#running-the-stress-test)
    - [Custom Performance Scripts](#custom-performance-scripts)
      - [Writing a Custom Benchmark Script](#writing-a-custom-benchmark-script)
      - [Running the Custom Script](#running-the-custom-script)
    - [Performance Optimization Tips](#performance-optimization-tips)
      - [Optimizing Kernel Execution](#optimizing-kernel-execution)
      - [Optimizing Data Transfers](#optimizing-data-transfers)
      - [Analyzing Bottlenecks](#analyzing-bottlenecks)
    - [Summary of Commands](#summary-of-commands)


## ROCm Tradecraft for GPU Performance Tuning

### System Setup and Installation

**Installing ROCm:**

```bash 
sudo apt update
sudo apt install -y rocm-dkms
```

**Adding ROCm Repository:**

```bash
echo 'deb [arch=amd64] http://repo.radeon.com/rocm/apt/debian/ xenial main' | sudo tee /etc/apt/sources.list.d/rocm.list
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key 609B6B9E
sudo apt update
```

**Installing ROCm Components:**

```bash
sudo apt install -y rocm-dev rocm-utils rocm-libs miopen-hip
```

## ROCm Component Packages

### rocm-dev
- **Description**: Development package for ROCm, including compiler and libraries needed for developing applications.
- **Components**: Includes the ROCm compiler, ROCm runtime, and various ROCm libraries for development.

### rocm-utils
- **Description**: Utility package for ROCm, providing tools for monitoring and managing ROCm-enabled devices.
- **Components**: Contains utilities like `rocm-smi` for system management and monitoring of ROCm devices.

### rocm-libs
- **Description**: Library package for ROCm, providing essential libraries for ROCm applications.
- **Components**: Includes libraries like ROCm Math Libraries (rocBLAS, rocFFT, rocSPARSE), ROCm Communication Libraries, and others necessary for running ROCm applications.

### miopen-hip
- **Description**: Machine Intelligence library for deep learning frameworks on ROCm, optimized for AMD GPUs.
- **Components**: Includes MIOpen, a GPU-accelerated library providing highly optimized implementations of standard deep learning operations.

## Monitoring and Managing GPU Usage

### Listing Available GPUs

To list all available GPUs:

```bash
/opt/rocm/bin/rocm-smi
```

### Monitoring GPU Utilization

To monitor GPU utilization in real-time:

```bash
watch -n 1 /opt/rocm/bin/rocm-smi --showhw
```

### Checking GPU Temperature

To check the current temperature of the GPUs:

```bash
/opt/rocm/bin/rocm-smi --showtemp
```

### Checking GPU Power Consumption

To check the power consumption of the GPUs:

```bash
/opt/rocm/bin/rocm-smi --showpower
```

### Checking GPU Fan Speed

To check the fan speed of the GPUs:

```bash
/opt/rocm/bin/rocm-smi --showfan
```

### Checking GPU Clock Frequencies

To check the clock frequencies of the GPUs:

```bash
/opt/rocm/bin/rocm-smi --showclk
```

## GPU Performance Tuning

### Setting GPU Power Profile

To set the power profile of a GPU:

```bash
sudo /opt/rocm/bin/rocm-smi --setsclk 4 --device 0
```

- **Description**: Sets the GPU power profile to a specific state.
- **Example**: `--setsclk 4` sets the GPU's power state to level 4.
- **Device**: `--device 0` specifies the target GPU (device 0).
- **Real-World Reasons**:
  - **Energy Efficiency**: Reduce power consumption and heat output in low-demand scenarios.
  - **Performance Tuning**: Increase power limits for high-performance tasks like deep learning model training.

### Setting GPU Fan Speed

To set the fan speed of a GPU:

```bash
sudo /opt/rocm/bin/rocm-smi --setfan 100 --device 0
```

- **Description**: Sets the GPU fan speed to a specific percentage.
- **Example**: `--setfan 100` sets the fan speed to 100% (full speed).
- **Device**: `--device 0` specifies the target GPU (device 0).
- **Real-World Reasons**:
  - **Overheating Prevention**: Increase fan speed during intensive tasks to prevent overheating.
  - **Noise Management**: Lower fan speed in less demanding scenarios to reduce noise in quiet environments.

### Setting GPU Memory Clock

To set the memory clock speed of a GPU:

```bash
sudo /opt/rocm/bin/rocm-smi --setmclk 2 --device 0
```

- **Description**: Sets the memory clock speed of the GPU to a specific level.
- **Example**: `--setmclk 2` sets the memory clock to level 2.
- **Device**: `--device 0` specifies the target GPU (device 0).
- **Real-World Reasons**:
  - **Performance Optimization**: Increase memory clock speed to boost performance in memory-intensive applications.
  - **Power Saving**: Reduce memory clock speed when high performance is not required to save energy.

### Setting GPU Performance Level

To set the performance level of a GPU:

```bash
sudo /opt/rocm/bin/rocm-smi --setperflevel high --device 0
```

- **Description**: Sets the GPU performance level.
- **Example**: `--setperflevel high` sets the performance level to high.
- **Device**: `--device 0` specifies the target GPU (device 0).
- **Real-World Reasons**:
  - **High Performance**: Set to high performance for demanding tasks like real-time rendering or complex simulations.
  - **Balanced Mode**: Use balanced performance levels to maintain a balance between performance and power consumption for typical workloads.

### Diagnostics and Debugging

**Checking GPU Health:**

```bash
/opt/rocm/bin/rocm-smi --showhealth
```

**Resetting GPU:**

```bash
sudo /opt/rocm/bin/rocm-smi --reset
```

**Saving GPU Logs:**

```bash
/opt/rocm/bin/rocm-smi --save log.txt
```

**Clearing GPU Logs:**

```bash
sudo /opt/rocm/bin/rocm-smi --clearlog
```

### GPU Memory Management

**Checking GPU Memory Usage:**

```bash
/opt/rocm/bin/rocm-smi --showmemuse
```

**Clearing GPU Memory:**

```bash
sudo /opt/rocm/bin/rocm-smi --clearmem
```

### Advanced GPU Configuration

**Overclocking GPU:**

```bash
sudo /opt/rocm/bin/rocm-smi --setsclkoc 1700 --device 0
```

**Underclocking GPU:**

```bash
sudo /opt/rocm/bin/rocm-smi --setsclkoc 1400 --device 0
```

**Setting Power Cap:**

```bash
sudo /opt/rocm/bin/rocm-smi --setpoweroverdrive 200 --device 0
```

### ROCm-SMI Commands Summary

**General Information:**

```bash
/opt/rocm/bin/rocm-smi --showhw
/opt/rocm/bin/rocm-smi --showallinfo
```

**Temperature and Fan:**

```bash
/opt/rocm/bin/rocm-smi --showtemp
/opt/rocm/bin/rocm-smi --showfan
/opt/rocm/bin/rocm-smi --setfan <percentage> --device <device_id>
```

**Power and Performance:**

```bash
/opt/rocm/bin/rocm-smi --showpower
/opt/rocm/bin/rocm-smi --setperflevel <level> --device <device_id>
/opt/rocm/bin/rocm-smi --setpoweroverdrive <value> --device <device_id>
```

**Clock Speeds:**

```bash
/opt/rocm/bin/rocm-smi --showclk
/opt/rocm/bin/rocm-smi --setsclk <value> --device <device_id>
/opt/rocm/bin/rocm-smi --setmclk <value> --device <device_id>
/opt/rocm/bin/rocm-smi --setsclkoc <value> --device <device_id>
```

**Memory:**

```bash
/opt/rocm/bin/rocm-smi --showmemuse
/opt/rocm/bin/rocm-smi --clearmem
```

**Logs and Health:**

```bash
/opt/rocm/bin/rocm-smi --showhealth
/opt/rocm/bin/rocm-smi --save <filename>
/opt/rocm/bin/rocm-smi --clearlog
```

**Reset:**

```bash
sudo /opt/rocm/bin/rocm-smi --reset
```

### Development Tools

**Installing HIP (Heterogeneous-Compute Interface for Portability):**

```bash
sudo apt install -y hip-base
```

**Compiling HIP Programs:**

```bash
hipcc my_program.cpp -o my_program
```

**Running HIP Programs:**

```bash
./my_program
```

**Using ROCm Libraries (e.g., rocBLAS, rocFFT):**

```bash
sudo apt install -y rocblas rocfft
```

### Performance Tuning and Benchmarking

**Installing ROCm Bandwidth Test:**

```bash
sudo apt install -y rocm-bandwidth-test
```

**Running Bandwidth Test:**

```bash
/opt/rocm/bin/rocm-bandwidth-test
```

**Using rocprof for Profiling:**

```bash
sudo apt install -y rocprof
rocprof --hip-trace ./my_program
```

**Using rocminfo for System Information:**

```bash
/opt/rocm/bin/rocminfo
```

### RoCE (RDMA over Converged Ethernet) and GPU Network Fabrics

**Installing RDMA Tools:**

```bash
sudo apt install -y rdma-core
```

**Configuring RoCE:**

```bash
sudo modprobe mlx4_ib
sudo modprobe rdma_ucm
sudo modprobe ib_ipoib
```

**Checking RDMA Devices:**

```bash
ibv_devices
```

**Displaying RDMA Configuration:**

```bash
ibv_devinfo
```

**Setting Up RDMA Over TCP/IP:**

```bash
sudo rdma link add rxe0 type rxe netdev eth0
```

**Listing RDMA Interfaces:**

```bash
rdma link show
```

**Running RDMA Bandwidth Test:**

```bash
ib_send_bw -d mlx5_0 -i 1
```

**RDMA Latency Test:**
```bash
ib_send_lat -d mlx5_0 -i 1
```

**Connecting RDMA Devices:**
```bash
rdma resource show qp
rdma resource show pd
Using rping for RDMA Connectivity Testing:
```

**Server-side:**
```bash

Copy code
sudo rping -s -a <server_ip> -v -C 10
```

**Client-side:**
```bash
Copy code
sudo rping -c -a <server_ip> -v -C 10
```

**Configuring QoS for RDMA Traffic:**
```bash
sudo tc qdisc add dev eth0 root handle 1: htb default 10
sudo tc class add dev eth0 parent 1:1 classid 1:10 htb rate 10Gbit
sudo tc filter add dev eth0 protocol ip parent 1:0 prio 1 u32 match ip dport 4791 0xffff flowid 1:10
```

**Setting up RDMA Multicast:**
```bash
sudo ib_mcjoin -v <multicast_group>
```

**Monitoring RDMA Traffic:**
```bash
sudo perfquery -a
```

## Performance and Benchmarking Cookbook Using ROCm, RDMA, and RoCE

### Installing Required Tools

**Installing ROCm and Performance Tools:**

```bash
sudo apt update
sudo apt install -y rocm-dkms rocm-utils rocm-libs rocm-bandwidth-test rocprof rdma-core
```

### Basic Performance Testing

**Running ROCm Bandwidth Test:**

```bash
/opt/rocm/bin/rocm-bandwidth-test
```

**Interpreting Bandwidth Test Results:**

- The output will display various bandwidth metrics for device-to-device, host-to-device, and device-to-host transfers.
- Look for metrics like `Peak Bandwidth` to understand the data transfer capabilities of your system.

### Profiling Applications with rocprof

**Profiling a HIP Program:**

```bash
rocprof --hip-trace ./my_program
```

**Generating a Profile Report:**

```bash
rocprof --hsa-trace ./my_program
```

**Analyzing Profile Data:**

- Use `rocprof` output to analyze kernel execution times, memory transfer times, and other performance metrics.
- Look for bottlenecks in kernel execution or data transfers.

### Using rocminfo for System Information

**Checking System Information:**

```bash
/opt/rocm/bin/rocminfo
```

- This provides detailed information about the GPUs in your system, including device IDs, memory sizes, and supported features.

### RDMA and RoCE Performance Testing

**Configuring RoCE:**

```bash
sudo modprobe mlx4_ib
sudo modprobe rdma_ucm
sudo modprobe ib_ipoib
```

**Setting Up RDMA Over TCP/IP:**

```bash
sudo rdma link add rxe0 type rxe netdev eth0
sudo ip link set rxe0 up
```

**Checking RDMA Devices:**

```bash
ibv_devices
```

**Displaying RDMA Configuration:**

```bash
ibv_devinfo
```

**Running RDMA Bandwidth Test:**

```bash
ib_send_bw -d mlx5_0 -I 1
```

**RDMA Latency Test:**

```bash
ib_send_lat -d mlx5_0 -I 1
```

**Using `rping` for RDMA Connectivity Testing:**

**Server-side:**

```bash
sudo rping -s -a <server_ip> -v -C 10
```

**Client-side:**

```bash
sudo rping -c -a <server_ip> -v -C 10
```

**Configuring QoS for RDMA Traffic:**

```bash
sudo tc qdisc add dev eth0 root handle 1: htb default 10
sudo tc class add dev eth0 parent 1:1 classid 1:10 htb rate 10Gbit
sudo tc filter add dev eth0 protocol ip parent 1:0 prio 1 u32 match ip dport 4791 0xffff flowid 1:10
```

**Setting up RDMA Multicast:**

```bash
sudo ib_mcjoin -v <multicast_group>
```

**Monitoring RDMA Traffic:**

```bash
sudo perfquery -a
```

### Advanced Performance Benchmarking

**Using rocblas-bench for BLAS Performance:**

**Installing rocBLAS:**

```bash
sudo apt install -y rocblas
```

**Running rocblas-bench:**

```bash
rocblas-bench -f gemm -r f32_r -m 4096 -n 4096 -k 4096 --a_type f32_r --b_type f32_r --c_type f32_r --d_type f32_r --alpha 1 --beta 0
```

- This command benchmarks the General Matrix Multiply (GEMM) operation for single-precision floating-point numbers.

### Using rocFFT for FFT Performance

**Installing rocFFT:**

```bash
sudo apt install -y rocfft
```

**Running rocFFT Benchmarks:**

```bash
/opt/rocm/bin/rocfft-bench -n 1000 -b 2048 -p single -t complex_forward
```

- This command benchmarks the FFT operation for single-precision complex numbers.

### Using RVS (ROCm Validation Suite)

**Installing RVS:**

```bash
sudo apt install -y rocm-validation-suite
```

**Example Configuration for RVS Stress Test:**

**Creating `stress.json`:**

```json
{
  "stress": {
    "device": ["all"],
    "count": 1,
    "duration": 5000,
    "metrics": ["gpu_busy", "mem_busy"]
  }
}
```

**Running the Stress Test:**

```bash
sudo rvs -c stress.json
```

- This command runs a stress test on all available GPUs for 5000 milliseconds and measures GPU and memory busy metrics.

### Custom Performance Scripts

**Writing a Custom Benchmark Script:**

**Example:**

```bash
#!/bin/bash

# Set environment variables for ROCm
export ROCM_PATH=/opt/rocm
export PATH=$ROCM_PATH/bin:$PATH
export LD_LIBRARY_PATH=$ROCM_PATH/lib:$LD_LIBRARY_PATH

# Run rocminfo
echo "Running rocminfo..."
/opt/rocm/bin/rocminfo

# Run rocprof on a HIP program
echo "Profiling HIP program..."
rocprof --hip-trace ./my_program

# Run rocBLAS benchmark
echo "Running rocBLAS GEMM benchmark..."
rocblas-bench -f gemm -r f32_r -m 4096 -n 4096 -k 4096 --a_type f32_r --b_type f32_r --c_type f32_r --d_type f32_r --alpha 1 --beta 0

# Run rocFFT benchmark
echo "Running rocFFT benchmark..."
/opt/rocm/bin/rocfft-bench -n 1000 -b 2048 -p single -t complex_forward

# Configure RDMA
echo "Configuring RDMA..."
sudo modprobe mlx4_ib
sudo modprobe rdma_ucm
sudo modprobe ib_ipoib
sudo rdma link add rxe0 type rxe netdev eth0
sudo ip link set rxe0 up

# Run RDMA bandwidth test
echo "Running RDMA bandwidth test..."
ib_send_bw -d mlx5_0 -I 1

# Run RDMA latency test
echo "Running RDMA latency test..."
ib_send_lat -d mlx5_0 -I 1

# Run RVS stress test
echo "Running RVS stress test..."
sudo rvs -c stress.json
```

**Running the Custom Script:**

```bash
chmod +x custom_benchmark.sh
./custom_benchmark.sh
```

### Performance Optimization Tips

**Optimizing Kernel Execution:**

- Use the `__global__` and `__device__` qualifiers correctly to ensure that kernel functions are executed on the GPU.
- Optimize memory access patterns to maximize memory bandwidth utilization.
- Use shared memory and registers effectively to reduce global memory access latency.

**Optimizing Data Transfers:**

- Minimize data transfers between host and device to reduce overhead.
- Use pinned (page-locked) memory for faster data transfers between host and device.

**Analyzing Bottlenecks:**

- Use profiling tools like `rocprof` to identify bottlenecks in kernel execution and data transfers.
- Experiment with different kernel configurations and memory layouts to improve performance.

### Summary of Commands

**System Information:**

```bash
/opt/rocm/bin/rocminfo
```

**Bandwidth Test:**

```bash
/opt/rocm/bin/rocm-bandwidth-test
```

**Profiling:**

```bash
rocprof --hip-trace ./my_program
```

**rocBLAS Benchmark:**

```bash
rocblas-bench -f gemm -r f32_r -m 4096 -n 4096 -k 4096 --a_type f32_r --b_type f32_r --c_type f32_r --d_type f32_r --alpha 1 --beta 0
```

**rocFFT Benchmark:**

```bash
/opt/rocm/bin/rocfft-bench -n 1000 -b 2048 -p single -t complex_forward
```

**RVS Stress Test:**

```bash
sudo rvs -c stress.json
```

**RDMA Configuration:**

```bash
sudo modprobe mlx4_ib
sudo modprobe rdma_ucm
sudo modprobe ib_ipoib
sudo rdma link add rxe0 type rxe netdev eth0
sudo ip link set rxe0 up
```

**RDMA Bandwidth Test:**

```bash
ib_send_bw -d mlx5_0 -I 1
```

**RDMA Latency Test:**

```bash
ib_send_lat -d mlx5_0 -I 1
```

**RDMA Connectivity Testing with `rping`:**

**Server-side:**

```bash
sudo rping -s -a <server_ip> -v -C 10
```

**Client-side:**

```bash
sudo rping -c -a <server_ip> -v -C 10
```

