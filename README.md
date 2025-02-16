# Genome Transition Zones Extraction Project

This project focuses on extracting transition zones from genomic nucleotide strings obtained from Ensembl (ensembl.org) using human genome chromosomes. The processed data will be used for training machine learning models using AutoML frameworks such as AutoGluon and experiment tracking with MLflow.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Project Structure](#project-structure)
3. [Data Sources](#data-sources)
4. [Data Extraction Process](data_extraction/README.md)
5. [Getting Started](#getting-started)
6. [Future Development](#future-development)
7. [License](#license)

## Project Overview

The objective of this project is to extract specific genomic transition zones from raw nucleotide strings. These transition zones include:
- **EI (Exon → Intron)**
- **IE (Intron → Exon)**
- **ZE (Intergenic Zone → First Exon)**
- **EZ (Last Exon → Intergenic Zone)**

The extraction is performed using a Jupyter Notebook (`genomic_data.ipynb`) located in the `data_extraction` folder. The extracted transitions are saved into CSV files in the `data` folder, which will later be used to train machine learning models.

## Project Structure

```
project_root/
│
├── data/
│   ├── data_ei.csv        # Extracted Exon → Intron transitions
│   ├── data_ie.csv        # Extracted Intron → Exon transitions
│   ├── data_ze.csv        # Extracted Intergenic Zone → First Exon transitions
│   └── data_ez.csv        # Extracted Last Exon → Intergenic Zone transitions
│
├── data_ensembl/
│   └── 21-1-46709983.txt  # Raw Ensembl data file (or test.txt for testing)
│
├── data_extraction/
│   ├── genomic_data.ipynb # Jupyter Notebook for data preprocessing and extraction
│   └── README.md          # Detailed explanation of the data extraction process
│
└── README.md              # This file
```

## Data Sources

The raw genomic data used in this project is obtained from Ensembl (ensembl.org). The raw data files are stored in the `data_ensembl` folder and include chromosome information from the human genome.

## Getting Started

1. **Install Dependencies:**  
   Clone the repository and install all required packages by running:
   ```bash
   pip install -r requirements.txt```

2. **Prepare the Data:**  
   - Place the raw data files in the `data_ensembl` folder.
   - Ensure the directory structure is as described above.


3. **Run Data Extraction:**  
   Open the `genomic_data.ipynb` notebook located in the `data_extraction` folder with Jupyter Notebook. Execute all cells to process the raw data and generate the CSV files in the `data` folder.


4. **Next Steps:**  
   After data extraction, you can use the processed CSV files to train machine learning models and track experiments with MLflow.

## Future Development

In future iterations, additional folders will be introduced, such as:
- **models/** – For storing trained model files and related scripts.
- **experiments/** – For experiment configurations and additional tracking details.
- **notebooks/** – For further exploratory analysis and model evaluation.

## License

This project is licensed under the [MIT License](LICENSE).