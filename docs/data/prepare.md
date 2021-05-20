# Prepare your data

## MS/MS

To use MetWork you need your MS/MS data in `.mgf` format. The recommanded way is to use the [GNPS platform](https://gnps.ucsd.edu) workflow. Once your job is finished, click on `Download Clustered Spectra as MGF` in the export section and extract the `.mgf` file in the download archive.

![.mgf from GNPS](/images/GNPS-MGF.png)


If you have `.mgf` generated in other way, make sure it has a `SCANS=` attribute for each ion with unique **feature id** associated as example bellow :

```{hl_lines="9"}
BEGIN IONS
PEPMASS=316.14001
CHARGE=1+
MSLEVEL=2
FILENAME=specs_ms.pklbin
ACTIVATION=CID
INSTRUMENT=ion trap
TITLE=Scan Number: 1
SCANS=1
43.01784114 1.53753298
61.02840582 1.55303643
73.02840582 0.7668902558
END IONS
```

## Annotations

The other data you need is at least one annotation file for each `.mgf`. these data annotate molecular structure in [SMILES](https://www.daylight.com/dayhtml/doc/theory/theory.smiles.html) format for a given feature.

3 formats are available :

### Default `.csv`

The `sourceId` first column correspond to the **feature id** of a given ion in the `.mgf`

```
IonId,name,smiles,source,sourceId
280,Corynantheidol,CC[C@@H]1CN2CCc3c([nH]c4ccccc34)[C@@H]2C[C@@H]1CCO,"GNPS : Isolated, Alexander Fox Ramos",483-27-2
265,Geissoschizine,C/C=C1/CN2CCc3c([nH]c4ccccc34)[C@@H]2CC1/C(=C/O)C(=O)OC,"GNPS : Isolated, Alexander Fox Ramos",439-66-7
```

### `.csv` with level info

Same as default `csv` with an additional `level` column to set the **status** of the annotation (*putative* or *validated*).

```
IonId,name,smiles,source,sourceId,level
280,Corynantheidol,CC[C@@H]1CN2CCc3c([nH]c4ccccc34)[C@@H]2C[C@@H]1CCO,"GNPS : Isolated, Alexander Fox Ramos",483-27-2,1
265,Geissoschizine,C/C=C1/CN2CCc3c([nH]c4ccccc34)[C@@H]2CC1/C(=C/O)C(=O)OC,"GNPS : Isolated, Alexander Fox Ramos",439-66-7,1
```

### GNPS `.tsv` format

From a GNPS job, use`.tsv` file in `result_specnets_DB` folder of cytoscape data from GNPS.
The `#Scan#` first column correspond to the **feature id** of a given ion in the `.mgf`

```
#Scan#	Adduct	CAS_Number	Charge	Compound_Name	Compound_Source	Data_Collector	ExactMass	INCHI	INCHI_AUX	Instrument	IonMode	Ion_Source	LibMZ	LibraryName	LibraryQualityString	Library_Class	MQScore	MZErrorPPM	MassDiff	Organism	PI	Precursor_MZ	Pubmed_ID	RT_Query	SharedPeaks	Smiles	SpecCharge	SpecMZ	SpectrumFile	SpectrumID	TIC_Query	UpdateWorkflowName	tags	
124	M+H	895096	0	5-HYDROXY-L-TRYPTOPHAN	Commercial standard	Prasad	220.085	N/A	N/A	Q-Exactive Plus	Positive	LC-ESI	221.09	lib-00012.mgf	Gold	1	0.949922	10.9736	0.00242615	GNPS-EMBL-MCF	Alexandrov Theodore	221.09	144	119.618	17	C1=CC2=C(C=C1O)C(=CN2)CC(C(=O)O)N	1	221.092	spectra/specs_ms.pklbin	CCMSLIB00000578036	3.98232e+08	UPDATE-SINGLE-ANNOTATED-GOLD	 
125	[M+H]+	78-40-0	1	MassbankEU:SM883101 Triethylphosphate|Triethyl phosphate	Isolated	Massbank	0.0	1S/C6H15O4P/c1-4-8-11(7,9-5-2)10-6-3/h4-6H2,1-3H3	N/A	LC-ESI-QFT	Positive	ESI	183.078	lib-00009.mgf	Bronze	3	0.977358	1.16684	0.000213623	MASSBANKEU	Massbank EU	183.078	N/A	898.417	6	CCOP(=O)(OCC)OCC	1	183.078	spectra/specs_ms.pklbin	CCMSLIB00000842082	3.48234e+07	UPDATE-SINGLE-ANNOTATED-BRONZE	 
```