

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

### Usage Example

Easily plug `FlowMap` into your existing PyTorch data pipeline:

```python
from flowmap import FlowMapDataset
from torch.utils.data import DataLoader

# Initialize the dataset
dataset = FlowMapDataset(
    data_path="path/to/your/data",
    chunk_size=1024,
    shuffle=True
)

# Use DataLoader for distributed loading
dataloader = DataLoader(dataset, batch_size=32, num_workers=4)

for batch in dataloader:
    # Train your model...
    pass

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
