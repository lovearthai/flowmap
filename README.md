

---

# FlowMap

**High-performance memory-mapped streaming dataset loader for PyTorch.**

`FlowMap` is a high-performance dataset framework designed for PyTorch, built specifically for efficient large-scale data processing. By leveraging memory-mapping (`mmap`) techniques, `FlowMap` enables ultra-fast data streaming with minimal memory overhead, making it ideal for deep learning tasks that require loading massive amounts of sequential data.

---

## Key Features

* **Ultra-Fast Performance**: Built on `mmap` for zero-copy file reading, eliminating traditional I/O bottlenecks.
* **Streaming Architecture**: Inherits from `torch.utils.data.IterableDataset`, enabling true stream-based processing for datasets that exceed available RAM.
* **Memory-Efficient**: Utilizes OS-level memory mapping to load data pages on-demand, significantly reducing memory pressure.
* **Easy Integration**: Seamlessly integrates into your existing PyTorch training pipelines with minimal code changes.
* **Production-Ready**: Built-in data integrity verification and optimized for multi-process distributed training.

---

## Quick Start

### Installation

```bash
pip install flowmap

```

# Usage

Run the following command in your terminal to scan a data directory and perform a stream iteration test:

```bash
flowmap-test /path/to/your/data
```

## What to expect

The tool will automatically detect the data path, scan recursively for binary shards, and iterate through the data stream.

You will see output similar to this:

```plaintext
2026-07-08 06:18:00 | INFO | 🔍 Starting scan and initializing FlowMapDataset: /data/raw_signals
2026-07-08 06:18:05 | INFO | 📊 Total rows in dataset: 1048576
2026-07-08 06:18:06 | INFO | 🚀 Starting data stream iteration test...
2026-07-08 06:18:10 | INFO | Step 0: Distribution [0:128, 1:128, 2:128, 3:128]
...
2026-07-08 06:18:25 | INFO | ✅ Test passed: Recursive directory scan successful, data stream is fully operational!
```

# Usage Example

```python
from flowmap import FlowMapDataset
from torch.utils.data import DataLoader

# Initialize the dataset using recursive directory/glob support
dataset = FlowMapDataset(shard_paths=["/data/signals/**/*.npy"], verbose=True)

# Wrap with standard PyTorch DataLoader
dataloader = DataLoader(dataset, batch_size=512, num_workers=2)

print(f"Dataset ready with {len(dataset)} items.")

for step, batch in enumerate(dataloader):
    # Data is streamed directly from disk via mmap
    process_data(batch)
```

---

## Why FlowMap?

When dealing with massive sequential data (e.g., high-throughput signal data, large logs, or complex time-series data), traditional file loading methods often suffer from I/O bottlenecks, causing GPU starvation. `FlowMap` bypasses conventional file system overhead by mapping files directly into memory, allowing data throughput to approach native memory read speeds.

---

## Contributing

Contributions are welcome! If you have ideas for performance improvements, feature requests, or bug reports, feel free to open an Issue or submit a Pull Request.

## License

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE).

---

### Tips for your repository:

1. **Add Benchmarks**: Including a simple chart in your README comparing `FlowMap`'s throughput against standard PyTorch `Dataset` implementations will be a powerful proof of concept for new users.
2. **Add an Examples Directory**: Create a `/examples` folder with a simple `train_demo.py` script so users can verify their setup immediately.
3. **Select a License**: Ensure you add a `LICENSE` file to your GitHub repository to define your distribution rights clearly.
