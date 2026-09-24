# IoT2026

Shared data for INF6953QE – Internet of Things Security (Fall 2026).

## `lab2/data` – CICIoT2023, cleaned

`ciciot2023_clean.parquet` (29.5 MB) has 918,764 rows × 40 columns:

- 37 flow features
- `Label`: original attack name (34 classes)
- `family`: attack category (8 classes: Benign, DDoS, DoS, Mirai, Recon, Spoofing, Web, BruteForce)
- `is_attack`: 0 = BENIGN, 1 = attack

It was built from `Merged01.csv` + `Merged02.csv` of the official CICIoT2023 `MERGED_CSV` release. The cleaning removed
NaN/inf rows, exact duplicates, and feature vectors that carry more than one label, and dropped two redundant columns.
[`CLEANING.md`](lab2/data/CLEANING.md) lists every step with row counts and the per-class counts. Scaling, sampling,
and train/test splitting are not applied.

### Download

Command line:

```bash
wget https://github.com/arpangl/IoT2026/raw/main/lab2/data/ciciot2023_clean.parquet
```

Or read it straight into pandas (works in Colab):

```python
import pandas as pd

df = pd.read_parquet("https://github.com/arpangl/IoT2026/raw/main/lab2/data/ciciot2023_clean.parquet")
```

SHA-256: `17e098c1cee713f5b1af79b918ae7ba59611c30a3bc609237d7afa7e9a97f8b1`

### Source

E. C. P. Neto, S. Dadkhah, R. Ferreira, A. Zohourian, R. Lu, and A. A. Ghorbani, "CICIoT2023: A real-time dataset and
benchmark for large-scale attacks in IoT environment," *Sensors*, vol. 23, no. 13, p. 5941, 2023.
Original data: Canadian Institute for Cybersecurity, University of New Brunswick –
https://www.unb.ca/cic/datasets/iotdataset-2023.html. Please cite the paper when using this data.
