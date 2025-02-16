# Data Extraction for Genomic Transition Zones

This folder contains the code for extracting transition zones from genomic nucleotide strings. The extraction is performed by the `genomic_data.ipynb` notebook. The goal is to identify key transition regions within each gene and save them into separate CSV files for further analysis with AutoML.

## Extraction Overview

For each gene in the Ensembl data, the extraction process identifies four types of transitions:

1. **Exon → Intron (EI) Transition**
2. **Intron → Exon (IE) Transition**
3. **Intergenic Zone → First Exon (ZE) Transition**
4. **Last Exon → Intergenic Zone (EZ) Transition**

### Data Structure

The data file contains lines with gene information followed by one or more lines of transcript (exon) details. The structure is as follows:

1. **Gene Information Line:**

   ```
   ([GEN_ID],[Cord_inicio_gen],[Cord_final_gen],[string_nucleotides],[chromosome_number],[Cord_global_inicio_gen],[Cord_global_final_gen],strand)
   ```

   *Example:*

   ```
   ([ENSG00000157005.4],[1000],[2482],[...],[3],[187667913],[187671395],false)
   ```

2. **Transcript Information Lines:**

   ```
   ([transcript_exon1_start, transcript_exon1_end],[transcript_exon2_start, transcript_exon2_end],...,[transcript_exonN_start, transcript_exonN_end],[transcript_count])
   ```

   *Example:*

   ```
   ([1000,1240],[2117,2482],[1])
   ```

   **Note:** Some genes might not have transcript lines. In such cases, only the gene information line is present.

## Detailed Extraction Process

The extraction logic implemented in `genomic_data.ipynb` performs the following steps for each gene that contains transcript data:

### 1. Exon → Intron (EI)

- **Locate Transition:**  
  Identify the end position of the first exon (e.g., 1240).

- **Determine Intron Start:**  
  The intron is assumed to start at `exon_end + 1` (i.e., 1241).

- **Validation:**  
  Confirm that the intron starts with the nucleotides `"gt"`, which should be located at positions 1241–1242.

- **Extraction:**  
  - Extract 5 characters immediately to the left of the intron start.
  - Extract 5 characters immediately to the right of the intron start.
  - Concatenate these substrings to form a 12-character sequence.

- **Storage:**  
  Save the result into `data_ei.csv`. Each character of the sequence is stored in its own column (B1, B2, …, B12).

### 2. Intron → Exon (IE)

- **Locate Transition:**  
  Identify the start position of the second exon (e.g., 2117).

- **Determine Intron End:**  
  The intron is assumed to end at `exon_start - 1` (i.e., 2116).

- **Validation:**  
  Confirm that the intron ends with `"ag"`, found at positions 2115–2116.

- **Extraction:**  
  - Extract 100 characters immediately to the left of the exon start.
  - Extract 5 characters immediately to the right of the exon start.
  - Concatenate these to form a 105-character sequence.

- **Storage:**  
  Save the result into `data_ie.csv`, with each character in a separate column (B1 to B105).

### 3. Intergenic Zone → First Exon (ZE)

- **Locate Transition:**  
  Use the start position of the first exon (e.g., 1000).

- **Extraction:**  
  - Extract 500 characters immediately to the left of the first exon.
  - Extract 50 characters immediately to the right of the first exon.
  - Concatenate these to form a 550-character sequence.

- **Storage:**  
  Save the result into `data_ze.csv`, with each character occupying its own column (B1 to B550).

### 4. Last Exon → Intergenic Zone (EZ)

- **Locate Transition:**  
  Use the end position of the last exon (e.g., 2482).

- **Extraction:**  
  - Extract 50 characters immediately to the left of the last exon.
  - Extract 500 characters immediately to the right of the last exon.
  - Concatenate these to form a 550-character sequence.

- **Storage:**  
  Save the result into `data_ez.csv`, with each character in its respective column (B1 to B550).

## Files and Outputs

After running the `genomic_data.ipynb` notebook, the following CSV files are generated in the designated data folder:

- **data_ei.csv:** Contains the EI transition sequences.
- **data_ie.csv:** Contains the IE transition sequences.
- **data_ze.csv:** Contains the ZE transition sequences.
- **data_ez.csv:** Contains the EZ transition sequences.

Each CSV file includes metadata (such as gene ID, chromosome number, and genomic coordinates) along with the extracted transition sequence distributed across multiple columns.

## Running the Extraction

1. Open `genomic_data.ipynb` in your Jupyter Notebook environment.
2. Ensure that your data files are located in the correct directory.
3. Execute the notebook to perform the data extraction.
4. Check the output CSV files for the extracted transition zones in the `/data` folder.