# SPDK NVMe-over-PCIe Loopback Performance Testing  
  
A comprehensive implementation and testing of SPDK (Storage Performance Development Kit) NVMe-over-Fabrics using TCP transport in a loopback configuration.  
  
## Project Overview  
  
This project demonstrates:  
- SPDK userspace storage stack implementation  
- NVMe-over-Fabrics (NVMe-oF) TCP transport configuration  
- Memory-based block device (malloc bdev) setup  
- Performance testing and analysis  
- Problem-solving in virtualized environments  
  
## Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│  SPDK NVMe      │    │   TCP Transport  │    │  SPDK NVMe-oF   │
│  Performance    │◄──►│   (127.0.0.1     │◄──►│  Target         │
│  Tool (Client)  │    │   Port 4420)     │    │  (nvmf_tgt)     │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                        │
                                                        ▼
                                                ┌─────────────────┐
                                                │  Malloc Bdev    │
                                                │  (Memory-based  │
                                                │  Storage)       │
                                                └─────────────────┘
```


## Performance Results  
  
- **IOPS**: 5,075.20  
- **Throughput**: 19.82 MiB/s  
- **Average Latency**: 6,307.18 µs  
- **Min Latency**: 474.38 µs  
- **Max Latency**: 14,010.41 µs  
  
*Note: Results obtained in virtualized environment with --no-huge mode*  
  
## Quick Start  
  
1. **Setup Environment**  
   ```bash  
   ./scripts/setup.sh
   
2. **Run Test**  
   ```bash  
   ./scripts/run_test.sh

3. **Save Results**  
   ```bash  
   ./scripts/save_results.sh

## Technical Highlights

- **Userspace Storage**: Bypasses kernel for reduced latency
- **Polling Mode I/O**: Eliminates interrupt overhead
- **NVMe-oF Protocol**: Network-based NVMe access
- **Problem Resolution**: Solved DPDK initialization, memory allocation, and CPU core locking issues

## Requirements

- Ubuntu/Linux system
- SPDK v25.09-pre or later
- Root privileges
- Minimum 512MB available memory

## Troubleshooting

See [troubleshooting.md](troubleshooting.md) for common issues and solutions.
