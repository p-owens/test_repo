# Concurrent DMA Transfer Benchmarks

- [Concurrent DMA Transfer Benchmarks](#concurrent-dma-transfer-benchmarks)
  - [Results - Block Transfers](#results---block-transfers)
    - [CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Cached DDR to Cached DDR](#coreaxi4-dma-cached-ddr-to-cached-ddr-pdma-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Cached DDR to Non-Cached DDR](#coreaxi4-dma-cached-ddr-to-cached-ddr-pdma-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Cached DDR](#coreaxi4-dma-cached-ddr-to-cached-ddr-pdma-non-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR](#coreaxi4-dma-cached-ddr-to-cached-ddr-pdma-non-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Cached DDR](#coreaxi4-dma-cached-ddr-to-non-cached-ddr-pdma-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Non-Cached DDR](#coreaxi4-dma-cached-ddr-to-non-cached-ddr-pdma-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Cached DDR](#coreaxi4-dma-cached-ddr-to-non-cached-ddr-pdma-non-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR](#coreaxi4-dma-cached-ddr-to-non-cached-ddr-pdma-non-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Cached DDR to Cached DDR](#coreaxi4-dma-non-cached-ddr-to-cached-ddr-pdma-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Cached DDR](#coreaxi4-dma-non-cached-ddr-to-cached-ddr-pdma-non-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Cached DDR to Non-Cached DDR](#coreaxi4-dma-non-cached-ddr-to-cached-ddr-pdma-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR](#coreaxi4-dma-non-cached-ddr-to-cached-ddr-pdma-non-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Cached DDR](#coreaxi4-dma-non-cached-ddr-to-non-cached-ddr-pdma-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Non-Cached DDR](#coreaxi4-dma-non-cached-ddr-to-non-cached-ddr-pdma-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Cached DDR](#coreaxi4-dma-non-cached-ddr-to-non-cached-ddr-pdma-non-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR](#coreaxi4-dma-non-cached-ddr-to-non-cached-ddr-pdma-non-cached-ddr-to-non-cached-ddr)
  - [Results - Stream Transfers](#results---stream-transfers)
    - [CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Cached DDR to Cached DDR](#coreaxi4-dma-stream-transfer-to-cached-ddr-pdma-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Cached DDR to Non-Cached DDR](#coreaxi4-dma-stream-transfer-to-cached-ddr-pdma-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Non-Cached DDR to Cached DDR](#coreaxi4-dma-stream-transfer-to-cached-ddr-pdma-non-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR](#coreaxi4-dma-stream-transfer-to-cached-ddr-pdma-non-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Cached DDR to Cached DDR](#coreaxi4-dma-stream-transfer-to-non-cached-ddr-pdma-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Cached DDR to Non-Cached DDR](#coreaxi4-dma-stream-transfer-to-non-cached-ddr-pdma-cached-ddr-to-non-cached-ddr)
    - [CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Non-Cached DDR to Cached DDR](#coreaxi4-dma-stream-transfer-to-non-cached-ddr-pdma-non-cached-ddr-to-cached-ddr)
    - [CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR](#coreaxi4-dma-stream-transfer-to-non-cached-ddr-pdma-non-cached-ddr-to-non-cached-ddr)


## Results - Block Transfers

### CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Cached DDR to Cached DDR

![coreaxi4dma_cachedDDR_cachedDDR-PDMA_cachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-CACHED_DDR1+PDMA_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Cached DDR to Non-Cached DDR

![coreaxi4dma_cachedDDR_cachedDDR-PDMA_cachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-CACHED_DDR1%2BPDMA_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Cached DDR

![coreaxi4dma_cachedDDR_cachedDDR-PDMA_cachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR

![coreaxi4dma_cachedDDR_cachedDDR-PDMA_noncachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Cached DDR

![coreaxi4dma_cachedDDR_noncachedDDR-PDMA_cachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-NON_CACHED_DDR1%2BPDMA_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Non-Cached DDR

![coreaxi4dma_cachedDDR_noncachedDDR-PDMA_cachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-NON_CACHED_DDR1%2BPDMA_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Cached DDR

![coreaxi4dma_cachedDDR_cachedDDR-PDMA_cachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-NON_CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR

![coreaxi4dma_cachedDDR_noncachedDDR-PDMA_noncachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_CACHED_DDR0-NON_CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Cached DDR to Cached DDR

![coreaxi4dma_noncachedDDR_cachedDDR-PDMA_cachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-CACHED_DDR1%2BPDMA_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Cached DDR

![coreaxi4dma_noncachedDDR_cachedDDR-PDMA_noncachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-CACHED_DDR1+PDMA_NON_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Cached DDR to Non-Cached DDR

![coreaxi4dma_noncachedDDR_cachedDDR-PDMA_cachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-CACHED_DDR1+PDMA_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR

![coreaxi4dma_noncachedDDR_cachedDDR-PDMA_noncachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-CACHED_DDR1+PDMA_NON_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Cached DDR

![coreaxi4dma_noncachedDDR_noncachedDDR-PDMA_cachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-NON_CACHED_DDR1+PDMA_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Cached DDR to Non-Cached DDR

![coreaxi4dma_noncachedDDR_noncachedDDR-PDMA_cachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-NON_CACHED_DDR1%2BPDMA_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Cached DDR

![coreaxi4dma_noncachedDDR_noncachedDDR-PDMA_noncachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-NON_CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Non-Cached DDR to Non-Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR

![coreaxi4dma_noncachedDDR_noncachedDDR-PDMA_noncachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR/CDMA_NON_CACHED_DDR0-NON_CACHED_DDR1+PDMA_NON_CACHED_DDR0-NON_CACHED_DDR1.png)

## Results - Stream Transfers

### CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Cached DDR to Cached DDR

![coreaxi4dma_stream_cachedDDR-PDMA_cachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-CACHED_DDR1%2BPDMA_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Cached DDR to Non-Cached DDR

![coreaxi4dma_stream_cachedDDR-PDMA_cachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-CACHED_DDR1%2BPDMA_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Non-Cached DDR to Cached DDR

![coreaxi4dma_stream_cachedDDR-PDMA_noncachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Stream Transfer to Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR

![coreaxi4dma_stream_cachedDDR-PDMA_noncachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Cached DDR to Cached DDR

![coreaxi4dma_stream_noncachedDDR-PDMA_cachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-NON_CACHED_DDR1%2BPDMA_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Cached DDR to Non-Cached DDR

![coreaxi4dma_stream_noncachedDDR-PDMA_cachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-NON_CACHED_DDR1%2BPDMA_CACHED_DDR0-NON_CACHED_DDR1.png)

### CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Non-Cached DDR to Cached DDR

![coreaxi4dma_stream_noncachedDDR-PDMA_noncachedDDR_cachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-NON_CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-CACHED_DDR1.png)

### CoreAXI4 DMA: Stream Transfer to Non-Cached DDR, PDMA: Non-Cached DDR to Non-Cached DDR

![coreaxi4dma_stream_noncachedDDR-PDMA_noncachedDDR_noncachedDDR](images/concurrent_dma_transfers/CACHED_DDR-STREAMING/CDMA_STREAM_GEN-NON_CACHED_DDR1%2BPDMA_NON_CACHED_DDR0-NON_CACHED_DDR1.png)
