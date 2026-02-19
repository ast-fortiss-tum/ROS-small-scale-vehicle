# Replication of "A Multi-Modality Evaluation of the Reality Gap in Autonomous Driving Systems"

This repository contains the replication package for the paper:

**"A Multi-Modality Evaluation of the Reality Gap in Autonomous Driving Systems"** In Proceedings of the *40th IEEE/ACM International Conference on Automated Software Engineering*, 2025.

A preprint version of the paper is available on [arXiv](https://arxiv.org/abs/2509.22379).


## Repository Structure

- **`./mixed_reality/`**  
  A ROS package that implements the testbed for Simulation-in-the-Loop (SiL), Vehicle-in-the-Loop (ViL), Mixed-Reality (MR), and Real-World (RW) autonomous driving experiments.

- **`./ASE_2025_appendix.pdf`**  
  Supplementary material including detailed figures, tables, and experimental data that were omitted from the main paper for brevity.

- **`./RQgeneration/`**  
  Python scripts and tools used to process `.bag` files and generate data used to answer the research questions in the study.

- **`./simulator_binary/`**  
  Unity-based Digital Twin of the small scale vehicle. Aready compiled for usage on Ubuntu systems.

## Usage

Refer to the `README.md` files inside each subfolder for setup instructions, usage examples, and experiment details.

---

## Reference
If you use our work in your research, if it helps your work, or if you simply find it useful, please cite the paper in your publications. An example BibTeX entry is provided below:

```bibtex
@inproceedings{2025-Lambertenghi-ASE,
	author       = {Stefano Carlo Lambertenghi and Mirena Flores Valdez and Andrea Stocco},
	title        = {A Multi-Modality Evaluation of the Reality Gap in Autonomous Driving Systems},
	booktitle    = {Proceedings of the 40th IEEE/ACM International Conference on Automated Software Engineering},
	series       = {ASE '25},
	publisher    = {IEEE},
	abbr         = {ASE},
	year         = 2025
}
``` 
