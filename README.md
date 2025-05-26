
---

# TCM-Navigator: Command-Line Toolkit for Molecular Generation and Evaluation

`TCM-Navigator` is a two-component command-line toolkit designed to streamline **molecular generation** and **property evaluation**, particularly for traditional Chinese medicine (TCM)-related ligands and target-specific drug discovery.

##  Toolkit Overview

| Component           | Purpose                                          |
| ------------------- | ------------------------------------------------ |
| 🔬 `TCM-Generator`  | Generate molecules (TCM-like/Target-specific) |
| 📊 `TCM-Identifier` | Evaluate molecules using a TCM-score predictor   |

---


# TCM-Generator: Molecule Generation Tool

A flexible CLI for generating molecules using chemical language models. It supports **TCM-like molecules genaration/Target specific molecules genaration** .

### ⚙️ Usage

```bash
./Generator [COMMAND] [OPTIONS]
```

### 📘 Commands

#### 1. `generate1`: General TCM-like Molecule Generation

Generate molecules based on traditional molecular patterns.

```bash
./Generator generate1 -n 128 -o output1.smi
```

| Option                   | Description                                                 |
| ------------------------ | ----------------------------------------------------------- |
| `-c` / `--checkpoint`    | Path to model checkpoint (default: `Generate1/finetune.pt`) |
| `-n` / `--num_molecules` | Number of molecules to generate                             |
| `-o` / `--output`        | Output SMILES file                                          |

---

#### 2. `generate2`: Target-Specific TCM-like Molecule Generation

Generate molecules with activity toward specific biological targets (e.g., DRD1, EGFR, Mpro, SIRT1).

```bash
./Generator generate2 -c Generate2/EGFR.pt -n 200 -o EGFR_output.smi
```

| Option                   | Description                     |
| ------------------------ | ------------------------------- |
| `-c` / `--checkpoint`    | Target-specific model path      |
| `-n` / `--num_molecules` | Number of molecules to generate |
| `-o` / `--output`        | Output SMILES file              |

---

#### 3. `eval`: Evaluate Molecule Properties

Evaluate a generated SMILES file for validity, diversity, drug-likeness, ADMET properties,etc.

```bash
./Generator eval -i output1.smi -o evaluation_results.csv
```

| Option            | Description            |
| ----------------- | ---------------------- |
| `-i` / `--input`  | Input SMILES file      |
| `-o` / `--output` | Evaluation result file |

---

# TCM-Identifier: Molecule Evaluation Tool

A command-line utility to score TCM-relevant compounds using a pre-trained AttentiveFP model. Designed for **high-throughput screening**.

### ⚙️ Usage

```bash
./Identifier -i <input.csv> -o <output.csv>
```

| Argument          | Description                                                    |
| ----------------- | -------------------------------------------------------------- |
| `-i` / `--input`  | Input CSV with `smiles` column                                 |
| `-o` / `--output` | Output file for prediction (default: `prediction_results.csv`) |

### Input Format

CSV file must contain a `smiles` column. Example:

```csv
id,smiles
cmpd1,CCO
cmpd2,C1=CC=CC=C1
cmpd3,CC(=O)OC1=CC=CC=C1C(=O)O
```

### Features

* Predicts TCM-score for input molecules
* Automatically caches features (`.pickle`)
* Invalid SMILES are skipped with warnings

---


---

## 🆘 Help and Support

For help with commands:

```bash
./Generator --help
./Identifier --help
```

For technical issues, contact: [cfy2yue@sjtu.edu.cn]


