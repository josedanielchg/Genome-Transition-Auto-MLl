## Installation Guide

### 1. Prerequisites

| Requirement | Recommended version | Notes |
|-------------|---------------------|-------|
| **Python**  | 3.9.5 (64‑bit)      | AutoGluon 1.2 ships wheels for these versions. <br>Later versions (3.11+) *may* work but are not officially tested. |
| **Git**     | ≥ 2.30              | For cloning / pulling updates |
| **curl / Postman** | *Optional*          | Handy for testing the `/predict` endpoint |
| **GPU drivers & CUDA** | *Optional*          | AutoGluon can leverage NVIDIA GPUs if CUDA 11.0+ is available |

### 2. Clone the repository

```bash
# Windows PowerShell / Git Bash / Linux / macOS
git clone https://github.com/josedanielchg/Genome-Transition-Auto-MLl.git
cd Genome-Transition-Auto-MLl
````

### 3. Create & activate a virtual environment

| OS                       | Command                                                |
| ------------------------ |--------------------------------------------------------|
| **Windows (PowerShell)** | `py -3.9 -m venv .venv`<br>`.\.venv\Scripts\Activate`  |
| **Linux / macOS**        | `python3 -m venv .venv`<br>`source .venv/bin/activate` |

### 4. Install dependencies

```bash
pip install -r requirements.txt
```


### 5. Fetch large data (optional) & models (required)

The `data/`, `data_ensembl/`, and `models/` directories are excluded from Git.
Download the ZIP from Google Drive, extract it at the project root, and make sure the three folders sit alongside `README.md`. Deails about how to download and use data and models are available at docs/data_usage.md.

### 6. Run a quick self‑test

```bash
# still inside the virtual‑env
uvicorn api.main:app --port 8000 --reload
```

* Uvicorn will start FastAPI on **[http://127.0.0.1:8000](http://127.0.0.1:8000)**.

---

## 🔌 API smoke test (placeholder)

```bash
curl -X POST "http://127.0.0.1:8000/predict" ^
     -H "Content-Type: application/json" ^
     -d "{\"sequence\":\"ttcctagaccttatatgtctaaactggggcttcctgacataaaactatgcttaccggccaggaatctgttagaaaactcagagctcagtagaaggaacactggctttggaatgtggaggtctggttttgctcaaagtgtgcagtatgtgaaggagaacaatttactgaccattactctgccttactgattcaaattctgaggtttattgaataatttcttagattgccttccagctctaaatttctcagcaccaaaatgaagtccatttcaatctctctctctctctttccctcccgtacatatacacacactcatacatatatatggtcacaatagaaaggcaggtagatcagaagtctcagttgctgagaaagagggagggagggtgagccagaggtaccttctcccccattgtagagaaaagtgaagttcttttagagccccgttacatcttcaaggctttttatgagataatggaggaaataaagagggctcagtccttctactgtccatatttcattctcaaatctgttattagaggaatgattctgatctccacctaccatacacatgccctgttgcttgttgggccttcctaaaatgttagagtatgatgacagatggagttgtctgggtacatttgtgtgcatttaagggtgatagtgtatttgctctttaagagctgagtgtttgagcctctgtttgtgtgtaattgagtgtgcatgtgtgggagtgaaattgtggaatgtgtatgctcatagcactgagtgaaaataaaagattgtataaatcgtggggcatgtggaattgtgtgtgcctgtgcgtgtgcagtatttttttttttttaagtaagccactttagatcttgtcacctcccctgtcttctgtgattgattttgcgaggctaatggtgcgtaaaagggctggtgagatctgggggcgcctcctagcctgacgtcagagagagagtttaaaacagagggagacggttgagagcacacaagccgctttaggagcgaggttcggagccatcgctgctgcctgctgatccgcgcctagagtttgaccagccactctccagctcggctttcgcggcgccgagatgctgtcctgccgcctccagtgcgcgctggctgcgctgtccatcgtcctggccctgggctgtgtcaccggcgctccctcggaccccagactccgtcagtttctgcagaagtccctggctgctgccgcggggaagcaggtaaggagactccctcgacgtctcccggattctccagccctccctaagccttgctcctgccccattggtttggacgtaagggatgctcagtccttctaaagagttttggtgcttttctgggtccctcagctcccgaagctcttgagaaaactatcaaaggctagaatccccttctaactctttttttcccccatgataagcgcagtcggtcacagttcaggtgagttcttacttggcattcaagaaaattacaaaatctgggtagttgtctgggcacgaagcgacaatggcgtctatccctggtgctgaccctgggaagcgctgacccaggtgctgaaacgcagacctctgaagctgctacctcttagcgtacctcacttccaaacgtcgggactagggcaaaggggcaatctaaagaccgaacgccgtatgtttgagattgtgagaagtctcgttcccctacagtttacttggtaaaaatggtaaaacaattctactttgtagctcgtgatgtgaaaattgaattaaactgttggcacacactttatcttaccagaacggtctttatgtgtgtgtgtgtgtgtgtgtgtgtgtttgtgcgtgtgtgtgtgtgtgtgtgtgtgttaagtctacagggacagaaaggttgcagaaacatttgagctcttaaagcctttttgtgtaacttggtaattatagcaactatccttatttttatatccttgattgattttaaatgtgacaaaaaatgcgcagctgtaaaaactggattttgtgtgtgaccaaatctgttctttaatttaggcttttcaaattttttccattgtcctccccacttctctttctctctttttctatcccttctgccctatacaggaactggccaagtacttcttggcagagctgctgtctgaacccaaccagacggagaatgatgccctggaacctgaagatctgtcccaggctgctgagcaggatgaaatgaggcttgagctgcagagatctgctaactcaaacccggctatggcaccccgagaacgcaaagctggctgcaagaatttcttctggaagactttcacatcctgttagctttcttaactagtattgtccatatcagacctctgatccctcgcccccacaccccatctctcttccctaatcctccaagtcttcagcgagacccttgcattagaaactgaaaactgtaaatacaaaataaaattatggtgaaattatgaaaaatgtgaatttggtttctattgagtaaatctttttgttcaataatacataataagcttgagtggcggtttcagtaaagttatttgagataggtactccaatgttcacaaacatctatttaaaattctcggtggcaataaagtttacattttaaatgataactattataacatgagtcattttaaacagaaataatttcacataactctatgcattcaaactttaattcaatgataattactgggagaggctgacataaacattaattacatattaagtacacctaaattatatgttggactattgaaatgagtgtgtgtgaatagttaggctgaaaaatccaactatctaccaggttgatatgtaaaatacataacatatgaaaagatggaaggaacaaagtcatttggtggttgagaaaaaatctgacttaaatagctaaaatgaggttctgaatttgtttctagtttgtaaacatttatctagagaaataccattgcttttgtgtcttctttgacaatcctctctaattgaacagtgctaaatgactgttttaaaagcaagcttttaagatattttttctcagggagaaatatcacttttattataagattccttctggaagtactataggttgcaagaaatgcatattggcttacctcactgagtgctatctatattgcaggtattggagctcaaaatcataattatgaaatagctgaaggagatatctcaagtcttctcttaattctatcaatatgggagtcaaataaaaacacaaaaattattcttaaacactcagtaaaggtgatagtcttataacaacatgctaaatgggatcactcaagacagaatgtaaacattgctaatttaacttcctgagacctaaagagatatcctttgggggatgtgtgttttagctatcaactgcatttctgcatagctactggaataaaaaccaaacataaatatgtatgctcaatataaatccttgtagtataaa\"}"
```

Expected response (example):

```jsonc
{
"ei":[118,386,397,911,1241,1461,1571,1843,2794,3165],
"ie":[232,760,1209,1368,1874,2043,2115,3064,3163,3398],
"ze":[678,696,699,700,739,743,752,765,776,818],
"ez":[455,739,1686,1693,1951,2410,2633,2634,2705,2821]
}
```

> The `/predict` endpoint accepts a JSON payload with a single key `sequence` (uppercase/lowercase nucleotides are accepted).
> A full description of request/response formats is available at **docs/api.md**.
