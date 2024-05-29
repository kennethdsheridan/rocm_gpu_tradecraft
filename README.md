# ROCm Tradecraft
This is a collection of Radeon Open Compute (ROCm) commnds, best practices and what not that will make you more confident with the AMD ROCm toolkit. And assist in transitioning from CUDA, over to a community driven parallel programming ecoystem you have control over. 

Welcome to the future folks...lets get started.

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

### Monitoring and Managing GPU Usage

**Listing Available GPUs:**

```bash
/opt/rocm/bin/rocm-smi
```

**Monitoring GPU Utilization:**

```bash
watch -n 1 /opt/rocm/bin/rocm-smi --showhw
```

**Checking GPU Temperature:**

```bash
/opt/rocm/bin/rocm-smi --showtemp
```

**Checking GPU Power Consumption:**

```bash
/opt/rocm/bin/rocm-smi --showpower
```

**Checking GPU Fan Speed:**

```bash
/opt/rocm/bin/rocm-smi --showfan
```

**Checking GPU Clock Frequencies:**

```bash
/opt/rocm/bin/rocm-smi --showclk
```

### Performance Tuning

**Setting GPU Power Profile:**

```bash
sudo /opt/rocm/bin/rocm-smi --setsclk 4 --device 0
```

**Setting GPU Fan Speed:**

```bash
sudo /opt/rocm/bin/rocm-smi --setfan 100 --device 0
```

**Setting GPU Memory Clock:**

```bash
sudo /opt/rocm/bin/rocm-smi --setmclk 2 --device 0
```

**Setting GPU Performance Level:**

```bash
sudo /opt/rocm/bin/rocm-smi --setperflevel high --device 0
```

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

