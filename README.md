# Protein Desgin and Allosteric Site Identification of Thyroid Peroxidase (TPO) 🧬
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
The AlphaFold-generated model of TPO was subjected to a rigorous refinement protocol to resolve initial structural inconsistencies. Preliminary preparation was conducted using **Schrödinger’s Protein Preparation Wizard** to assign bond orders and optimize the H-bond network. To ensure physiological relevance, the model was migrated to **MOE** for **Protonate 3D** analysis (pH 7.0, 300K). A final **Energy Minimization** was performed using the **Amber:EHT Force Field**. To achieve optimal structural relaxation, this step was evaluated iteratively using two different RMS gradients (**0.1** and a more stringent **0.01** kcal/mol/Å²). This process successfully eliminated atomic clashes, corrected hybridization errors, and stabilized the protein for downstream analysis.

### 5. Structural Validation Outcomes
To ensure the reliability of the refined TPO model, multiple validation servers were utilized via the **SAVES v6.0** platform. A comparative evaluation of the minimized models revealed that the structure minimized with the stricter **0.01 RMS gradient** yielded superior stereochemical stability and improved non-bonded interactions. Therefore, it was selected as the final model. The outcomes for this chosen model confirmed its high quality:

* **Verify3D:** Successfully improved to **80.39% (Pass)**, confirming the robust compatibility of the 3D atomic model with its 1D amino acid sequence.
* **ERRAT:** Achieved an outstanding overall quality factor of **87.21** (improved from 84.67), indicating a highly confident distribution of non-bonded atomic interactions.
* **Ramachandran Plot:** Analysis via **PROCHECK** confirmed a stereochemically sound structure, with the vast majority of residues located in the favored and allowed regions, ensuring proper backbone geometry.
* **WHATCHECK:** Summary reports indicated a reliable model with normalized stereochemical parameters suitable for allosteric site identification.


![Image](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/%D9%84%D9%82%D8%B7%D8%A9%20%D8%B4%D8%A7%D8%B4%D8%A9%202026-03-04%20143537.png)

![Image](https://github.com/abdulaziz-khaled/Structural-Modeling-and-Allosteric-Site-Identification-of-Thyroid-Peroxidase-TPO-/blob/main/%D9%84%D9%82%D8%B7%D8%A9%20%D8%B4%D8%A7%D8%B4%D8%A9%202026-03-04%20131302.png)


### 6. Targeted Structural Refinement and Visualization
**Via `SAVES Server` and `PyMol`** 

* Following the initial structural validation, localized geometric deviations—identified as unstable regions in the ERRAT plot—required further optimization. Using the Molecular Operating Environment (MOE) software, these specific problematic loops and individual amino acid residues were manually selected for targeted energy minimization. By applying the AMBER:EHT force field exclusively to these selected regions while keeping the rest of the protein fixed, steric clashes were successfully resolved, and local geometries were optimized without disrupting the overall stable backbone fold.

`energy mini tpo moe .pdb`


* Subsequently, the refined three-dimensional model was exported to PyMOL for proper structural formatting and visual inspection. Since the prior preparation and minimization procedures had temporarily merged the multi-chain complex into a single continuous sequence, PyMOL was utilized to accurately reassign and segregate the protein into its constituent chains (e.g., Chain A, B, and C) based on their specific residue ranges. Finally, each defined chain was distinctly color-coded to enhance structural visualization and confirm the integrity of the complex. This correctly formatted and validated structure was established as the final TPO model, serving as the sole and definitive structural basis for all subsequent downstream computational applications, including allosteric site identification and molecular docking studies.
The following command-line script was executed within PyMOL to restore the multimeric structural integrity:

```pymol
alter (resi 5-305), chain='A'
alter (resi 306-606), chain='B'
alter (resi 607-827), chain='C'
sort
```

`tpo prep PyMol.pdb`

### 7. Allosteric Site Identification

Following the finalization of the 3D structure, the identification of a prospective allosteric binding pocket was conducted using the **Autochem agent v1** on the [**PAULING.AI**](https://www.pauling.ai/) platform. The objective was to locate a well-defined cavity distinct from the primary orthosteric active site, specifically targeting regions capable of allosteric communication and conformational control.

The automated site-finding algorithm evaluated potential binding pockets across the fully prepared TPO complex. **Site ID 1252** was selected as the optimal primary allosteric target based on its strategic location at the domain-domain interface between **Chain A** and **Chain B**. Structural analysis indicated that this pocket exhibits a highly favorable druggability profile for small-molecule modulation, characterized by:
* **Pocket Score:** 36.56
* **Probability Score:** 0.96

#### Selected Allosteric Site Details (Residues)
The spatial boundaries of this selected allosteric site involve specific regulatory structural elements from both interacting chains. The key residues forming the predicted cavity include:

- **Chain A:** 56, 60, 213, 217, 220, 221, 224, 225, 226, 228, 270, 271, 272.
- **Chain B:** 378, 381, 382, 384, 468, 473, 476, 479, 480, 482, 483, 505, 542, 546, 547, 557, 560, 561, 564.

> **Note on Downstream Application:** > The identification of this highly probable interfacial pocket provided a precisely defined target matrix. This strategically selected site was subsequently utilized for the molecular docking pipeline to screen and identify potential partial-occupancy **Negative Allosteric Modulators (NAMs)** capable of interfering with signal propagation and destabilizing the active conformation of the TPO structure.

## 🛠️ Tools Used
* SignalP
* DeepTMHMM
* AlphaFold
* Schrödinger Suite (Protein Preparation Wizard)
* MOE - Molecular Operating Environment (Structure Preparation, Protonate 3D, Energy Minimization)
* SAVES Server 
* PyMol
* PAULING AI (Autochem agent v1)

## 💬 Contact of Discussion

•	**Project Author**: Abdulaziz Khaled

•	**GitHub**: https://github.com/abdulaziz-khaled￼

•	**Email**: abdelaziz.khaled.eg@gmail.com
	
•	**LinkedIn**: https://www.linkedin.com/in/abdul-aziz-khaled

• **Telegram**: https://t.me/zizo_elamir
