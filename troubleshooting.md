# Troubleshooting Guide

## Common Issues and Solutions

### 1. CPU Core Lock Conflict
**Error**: `Cannot create lock on core 0, probably process XXX has claimed it`

**Solution**: 
```bash
sudo pkill -f spdk
# or
sudo build/bin/spdk_tgt --disable-cpumask-locks &
```

### 2. Memory Allocation Failure
**Error**: `malloc_buf spdk_zmalloc() failed`

**Solution**: Use smaller memory allocation or --no-huge mode
```bash
sudo scripts/rpc.py bdev_malloc_create -b Malloc0 8 512  # 8MB instead of larger sizes
```

### 3. DPDK Initialization Failure
**Error**: `Cannot use IOVA as 'PA' since physical addresses are not available`

**Solution**: Use --no-huge mode with memory specification
```bash
build/bin/spdk_nvme_perf --no-huge -s 512 [other parameters]
```