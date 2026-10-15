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

Clone the repo (fastest; the file lands in `IoT2026/lab2/data/`):

```bash
git clone --depth 1 https://github.com/arpangl/IoT2026.git
```

Or download the repo as a zip: https://github.com/arpangl/IoT2026/archive/refs/heads/main.zip

Or fetch just the file / read it straight into pandas (works in Colab). This goes through
`raw.githubusercontent.com`, which can be slow on some networks; use the clone if it crawls.

```bash
wget https://github.com/arpangl/IoT2026/raw/main/lab2/data/ciciot2023_clean.parquet
```

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

## `lab3/data` – IoT-23, cleaned

`iot23_clean.parquet` (5.6 MB) has 717,667 rows × 59 columns:

- 54 flow features: 10 numeric Zeek fields (ports, duration, bytes, packets) and 0/1 columns for `proto`, `service`,
  `conn_state`, and the TCP flags in `history`
- `scenario`: IoT-23 capture (23 values); `malware`: its malware name (or the device, for the 3 benign captures)
- `detailed_label`: IoT-23 detailed label (16 classes)
- `family`: traffic category (7 classes: Benign, PortScan, DDoS, C&C, Okiru, Attack, FileDownload)
- `is_attack`: 0 = Benign, 1 = Malicious

It was built from the `conn.log.labeled` Zeek logs of all 23 scenarios (325M flows). The IP addresses, timestamps, and
connection ids were dropped. Most flows are copies of the same scan or flood connection, so at most 50,000 different
flows were kept per (scenario, detailed label); smaller groups are complete. Unset values (`-`) were set to 0, and
duplicates across scenarios and feature vectors that carry more than one label were removed.
[`CLEANING.md`](lab3/data/CLEANING.md) lists every step with row counts and the counts per scenario. Scaling and
train/test splitting are not applied.

### Download

Clone the repo (fastest; the file lands in `IoT2026/lab3/data/`):

```bash
git clone --depth 1 https://github.com/arpangl/IoT2026.git
```

Or download the repo as a zip: https://github.com/arpangl/IoT2026/archive/refs/heads/main.zip

Or fetch just the file / read it straight into pandas (works in Colab):

```bash
wget https://github.com/arpangl/IoT2026/raw/main/lab3/data/iot23_clean.parquet
```

```python
import pandas as pd

df = pd.read_parquet("https://github.com/arpangl/IoT2026/raw/main/lab3/data/iot23_clean.parquet")
```

SHA-256: `00ce69fe04c1a52201a61f7a22e78497147aafaf3eaccc8626c2f3524e6427cf`

### Source

S. Garcia, A. Parmisano, and M. J. Erquiaga, "IoT-23: A labeled dataset with malicious and benign IoT network
traffic," Stratosphere Laboratory, Prague, 2020. https://doi.org/10.5281/zenodo.4743746 –
https://www.stratosphereips.org/datasets-iot23. Please cite it when using this data.
