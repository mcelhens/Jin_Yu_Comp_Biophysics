# Example set of input files for simulation nucleotide fidelity of SARS-CoV-2 RdRp using dATP

## Please include the following citations:

ATP and Remdesivir-TP:

```
@article{romero_probing_2021,
	title = {Probing remdesivir nucleotide analogue insertion to {SARS}-{CoV}-2 {RNA} dependent {RNA} polymerase in viral replication},
	volume = {6},
	issn = {2058-9689},
	url = {https://pubs.rsc.org/en/content/articlelanding/2021/me/d1me00088h},
	doi = {10.1039/D1ME00088H},
	language = {en},
	number = {11},
	urldate = {2022-01-21},
	journal = {Molecular Systems Design \& Engineering},
	author = {Romero, Moises Ernesto and Long, Chunhong and Rocco, Daniel La and Keerthi, Anusha Mysore and Xu, Dajun and Yu, Jin},
	month = nov,
	year = {2021},
	note = {Publisher: The Royal Society of Chemistry},
	keywords = {RdRp, read},
	pages = {888--902},
}

dATP and GTP:

@article{romero_trapping_2023,
	title = {Trapping non-cognate nucleotide upon initial binding for replication fidelity control in {SARS}-{CoV}-2 {RNA} dependent {RNA} polymerase},
	copyright = {All rights reserved},
	issn = {1463-9084},
	url = {https://pubs.rsc.org/en/content/articlelanding/2024/cp/d3cp04410f},
	doi = {10.1039/D3CP04410F},
	language = {en},
	urldate = {2023-12-11},
	journal = {Physical Chemistry Chemical Physics},
	author = {Romero, Moises Ernesto and McElhenney, Shannon J. and Yu, Jin},
	month = dec,
	year = {2023},
	note = {Publisher: The Royal Society of Chemistry},
}
```

## Included files

### PDBs:

dATP_umbrella_open_ref.pdb

> SARS-CoV-2 RdRp structural model of initial binding with dATP
> water and ions not included

dATP_umbrella_closed_ref.pdb

> SARS-CoV-2 RdRp structural model of insertion with dATP
> water and ions not included

### MDP (Gromacs run generating files):

minimize.mdp

> minimization file generator
> may also be used for ionization

nvt.mdp

> thermalization file generator

npt_eq.mdp

> equilibrium simulation file generator
> uses the modified Brensden barostat

npt_es.mdp

> simulation file generator for enhanced sampling runs
> uses the Paranello-Rahman barostat

### Enhanced sampling run files (*.dat, for Plumed):

TMD_plumed.dat

> targeted MD generator

Umbrella_plumed.dat

> umbrella sampling generator

SMD_plumed.dat

> steered MD generator

## How to generate

1. Generate water box with ions using a cubic box of 1.5 nm margins and 100 mM of neutralizing NaCl
2. Minimize with minimize.mdp
3. Thermalize with nvt.mdp
4. Equilibrate with npt_eq.mdp
5. Prepare targeted MD by selecting quasi-equilbrium structure
6. Perform targeted MD with TMD_plumed.dat and npt_es.mdp
7. Select windows and perform umbrella sampling with Umbrella_plumed.dat and npt_es.mdp
8. Standard parameters for WHAM (see WHAM documentation) are used for reweighting removing 10 ns of each window for equilibration
9. Steered MD may be performed if desired on umbrella window results using SMD_plumed.dat and npt_es.mdp
