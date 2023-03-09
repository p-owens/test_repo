# CoreAXI4 DMA Performance Benchmarks

- [CoreAXI4 DMA Performance Benchmarks](#coreaxi4-dma-performance-benchmarks)
  - [Block Transfers](#block-transfers)
    - [Executing from L2-LIM](#executing-from-l2-lim)
    - [Executing from Scratchpad Memory](#executing-from-scratchpad-memory)
    - [Executing from DDR](#executing-from-ddr)
  - [Stream Transfers](#stream-transfers)
    - [Executing from L2-LIM](#executing-from-l2-lim-1)
    - [Executing from Scratchpad Memory](#executing-from-scratchpad-memory-1)
    - [Executing from DDR](#executing-from-ddr-1)

## Block Transfers

These results show the performance of the CoreAXI4 DMA (Fabric-DMA/F-DMA) block transferring data.

### Executing from L2-LIM

![l2-lim_block_transfer](images/CoreAXI4_DMA_Controller/L2_LIM.png)

| Source:        | Destination    | Transfer Size (MB) | Peak Rate (MB/s) | % of Theoretical Rate |
| :------------- | :------------- | :----------------- | :--------------- | :-------------------- |
| Cached DDR     | Cached DDR     | 0.10               | 899              | 45%                   |
| Cached DDR     | Non-Cached DDR | 0.12               | 907              | 45%                   |
| Non-Cached DDR | Cached DDR     | 0.52               | 868              | 43%                   |
| Non-Cached DDR | Non-Cached DDR | 1.00               | 871              | 43%                   |

### Executing from Scratchpad Memory

![scratchpad_block_transfer](images/CoreAXI4_DMA_Controller/SCRATHCPAD.png)

| Source:        | Destination    | Transfer Size (MB) | Peak Rate (MB/s) | % of Theoretical Rate |
| :------------- | :------------- | :----------------- | :--------------- | :-------------------- |
| Cached DDR     | Cached DDR     | 0.52               | 784              | 39%                   |
| Cached DDR     | Non-Cached DDR | 1.00               | 926              | 46%                   |
| Non-Cached DDR | Cached DDR     | 1.00               | 871              | 44%                   |
| Non-Cached DDR | Non-Cached DDR | 1.00               | 871              | 44%                   |

### Executing from DDR

![ddr_block_transfer](images/CoreAXI4_DMA_Controller/CACHED_DDR.png)

| Source:        | Destination    | Transfer Size (MB) | Peak Rate (MB/s) | % of Theoretical Rate |
| :------------- | :------------- | :----------------- | :--------------- | :-------------------- |
| Cached DDR     | Cached DDR     | 0.06               | 886              | 44%                   |
| Cached DDR     | Non-Cached DDR | 0.01               | 904              | 45%                   |
| Non-Cached DDR | Cached DDR     | 0.43               | 868              | 44%                   |
| Non-Cached DDR | Non-Cached DDR | 1.00               | 871              | 44%                   |

## Stream Transfers

These results show the performance of the CoreAXI4 DMA (Fabric-DMA/F-DMA) stream transferring data.

### Executing from: L2-LIM

![l2-lim_stream_transfer](images/CoreAXI4_DMA_Controller/L2_LIM-STREAMING.png)

| Source:          | Destination    | Transfer Size (MB) | Peak Rate (MB/s) | % of Theoretical Rate |
| :--------------- | :------------- | :----------------- | :--------------- | :-------------------- |
| Stream Generator | Cached DDR     | 0.52               | 931              | 47%                   |
| Stream Generator | Non-Cached DDR | 1.00               | 926              | 46%                   |

### Executing from: Scratchpad Memory

![scratchpad_stream_transfer](images/CoreAXI4_DMA_Controller/SCRATHCPAD-STREAMING.png)

| Source:          | Destination    | Transfer Size (MB) | Peak Rate (MB/s) | % of Theoretical Rate |
| :--------------- | :------------- | :----------------- | :--------------- | :-------------------- |
| Stream Generator | Cached DDR     | 1.00               | 932              | 47%                   |
| Stream Generator | Non-Cached DDR | 1.00               | 925              | 46%                   |

### Executing from: DDR

![ddr_stream_transfer](images/CoreAXI4_DMA_Controller/CACHED_DDR-STREAMING.png)

| Source:          | Destination    | Transfer Size (MB) | Peak Rate (MB/s) | % of Theoretical Rate |
| :--------------- | :------------- | :----------------- | :--------------- | :-------------------- |
| Stream Generator | Cached DDR     | 0.46               | 940              | 47%                   |
| Stream Generator | Non-Cached DDR | 1.00               | 936              | 47%                   |
