# Structural Modeling and Allosteric Site Identification of Thyroid Peroxidase (TPO) 🧬
![TPO Protein Visualization](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/protein_dark_highres.png)

## 📌 Project Overview
Thyroid Peroxidase (TPO) is a crucial enzyme responsible for thyroid hormone synthesis and is the primary target implicated in hypothyroidism and autoimmune thyroid diseases (e.g., Hashimoto's thyroiditis). Due to its large size and complexity, a complete 3D experimentally determined structure is currently unavailable. 

This project aims to computationally model the 3D structure of mature TPO, analyze its topological domains, and identify novel **allosteric binding sites** distant from the catalytic heme region for potential and highly specific drug targeting.

## 🔬 Methodology & Computational Pipeline

The workflow of this project was executed using a combination of bioinformatics tools and molecular modeling software:

### 1. Sequence Analysis & Signal Peptide Cleavage
* **Tool:** SignalP (version used, e.g., 6.0)
* **Action:** The raw amino acid sequence of TPO was analyzed to identify and remove the secretory signal peptide, mimicking the physiological maturation process of the enzyme.
* **Results:** 
    * **Signal Peptide Probability:** 99.98%
    * **Cleavage Site:** Between amino acids 18 and 19.
    * **Outcome:** Residues 1 through 18 were successfully cleaved. The resulting sequence (starting from residue 19) represents the **mature TPO**, which was subsequently used for all downstream topological and structural modeling.


![signal peptide plot](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/%D9%84%D9%82%D8%B7%D8%A9%20%D8%B4%D8%A7%D8%B4%D8%A9%202026-02-27%20211856.png)

### 2. Transmembrane Topology Prediction
* **Tool:** DeepTMHMM
* **Action:** To understand the spatial orientation and functional regions of the mature TPO enzyme, a comprehensive transmembrane topology prediction was performed. This step is crucial for accurate 3D modeling and ensuring that pocket identification targets the correct physiological domains.
* **Results:** The analysis of the mature TPO sequence revealed a classic single-pass transmembrane architecture, distributed as follows:
    * **Extracellular/Luminal Domain (Outside):** Residues 1 – 831. This massive domain houses the primary catalytic core and the heme-binding region.
    * **Transmembrane Helix (TM):** Residues 832 – 852. A highly hydrophobic alpha-helix responsible for anchoring the enzyme to the apical membrane of thyroid follicular cells.
    * **Intracellular Domain (Inside):** Residues 853 – 915. A short cytosolic tail.
* **Significance:** Accurately mapping these topological domains ensured that downstream structural preparation and allosteric site searches avoided the membrane-embedded TM helix (which is typically poorly druggable) and focused on the accessible extracellular regions.

![plot](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/%D9%84%D9%82%D8%B7%D8%A9%20%D8%B4%D8%A7%D8%B4%D8%A9%202026-02-27%20213121.png)
![predict](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/%D9%84%D9%82%D8%B7%D8%A9%20%D8%B4%D8%A7%D8%B4%D8%A9%202026-02-27%20213138.png)

### 3. 3D Structure Generation
* **Tool:** AlphaFold 
* **Action:** Due to the lack of a full PDB structure, a high-confidence 3D model of the mature TPO was generated utilizing AlphaFold's deep learning predictive capabilities.

![Insert Image of your AlphaFold 3D model here](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/120649A081B0F2E6.png)


### 4. Protein Preparation & Energy Minimization
**Tools:**
* **Schrödinger Suite** (Protein Preparation Wizard)
* **MOE - Molecular Operating Environment** (Structure Preparation & Protonate 3D)

**Action:**
The AlphaFold-generated model of TPO was subjected to a rigorous refinement protocol to resolve initial structural inconsistencies. Preliminary preparation was conducted using **Schrödinger’s Protein Preparation Wizard** to assign bond orders and optimize the H-bond network. To ensure physiological relevance, the model was migrated to **MOE** for **Protonate 3D** analysis (pH 7.0, 300K). A final **Energy Minimization** was performed using the **Amber14:EHT Force Field** with an RMS gradient of 0.1 kcal/mol/Å². This process successfully eliminated atomic clashes and corrected hybridization errors, stabilizing the protein for downstream analysis.

### 5. Structural Validation Outcomes
To ensure the reliability of the refined TPO model, multiple validation servers were utilized via the **SAVES v6.0** platform. The outcomes confirmed a high-quality, stereochemically stable structure:

* **Verify3D:** Successfully improved from **78.46% (Fail)** to **80.26% (Pass)**, confirming the compatibility of the 3D atomic model with its 1D amino acid sequence.
* **ERRAT:** Achieved an overall quality factor of **84.67**, indicating a high-confidence distribution of non-bonded atomic interactions.
* **Ramachandran Plot:** Analysis via **PROCHECK** confirmed a stereochemically sound structure, with the vast majority of residues located in the favored and allowed regions, ensuring proper backbone geometry.
* **WHATCHECK:** Summary reports indicated a reliable model with normalized stereochemical parameters suitable for allosteric site identification.


### 6. Binding Site Identification (SiteMap)
* **Tool:** Schrödinger (SiteMap)
* **Action:** An extensive search for potential binding pockets was conducted to identify an allosteric site. 
* **Findings:** 10 potential pockets were identified.

![sitmap](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/%D9%84%D9%82%D8%B7%D8%A9%20%D8%B4%D8%A7%D8%B4%D8%A9%202026-02-27%20211303.png)


## 🛠️ Tools Used
* SignalP
* DeepTMHMM
* AlphaFold
* PyMol
* Schrödinger Suite (Protein Preparation Wizard, SiteMap)
* MOE - Molecular Operating Environment (Structure Preparation & Protonate 3D)
* SAVES Server 

## 🚀 Future Work
* Selection Allosteric Site.
* Perform virtual screening (Molecular Docking) NAMs the identified allosteric pocket.
* Conduct Molecular Dynamics (MD) simulations to validate the stability of the protein-ligand complexes.
