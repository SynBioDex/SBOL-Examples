# Host Context / Ontologies for Experiments

## 1 Mixtures via Components

Any `Component` can be interpreted as specifying a mixture of the material entity (SBO:0000240) `Features` that it includes. The amount of each such instance included in the mixture SHOULD be specified by attaching a `om:Measure` with a `type` set to the appropriate SBO term. The SBO terms that are RECOMMENDED as appropriate are members of the Systems Description Parameter (SBO:0000545) branch of SBO. Examples include: 

 - SBO:0000540: fraction of an entity pool (e.g.,1/3 CHO cells, 2/3 HEKcells)
 - SBO:0000472: molar concentration of an entity (e.g.,1mM arabinose)
 - SBO:0000361: amount of an entity pool (e.g.,200 uL M9 media)
 
 Mixtures MAY be defined recursively, as mixtures of mixtures of mixtures, etc.
 
 ## 2 Media, Inducers, and Other Reagents
 
 Each reagent, whether “atomic” (e.g., rainbow bead control) or mixture (e.g., M9 media), SHOULD be represented as a `Component` and/or as a `Feature` of a `Component` in which the reagent is used. For example, a custom media mixture might be defined as a `Component` and used as a `SubComponent`, while a commercially supplied reagent might be used as an `ExternallyDefined` feature linking to its PubChem identifiers.
 
 The roles of reagents may vary in context: for example, arabinose may serve as an inducer or as a media carbon source. As such, contextual `role` SHOULD be indicated by an NCI Thesaurus (NCIT) term in a role property of the `Feature`. Examples include:
 
  - NCIT:C64356: PositiveControl
  - NCIT:C48694: Cell
  - NCIT:C85504: Media
  - NCIT:C14419: Strain
  - NCIT:C120268: Inducer

For more information on representing cells, strains, plasmids, and genomes, see BP0010.

## 3 Samples

A complete specification of a sample SHOULD be a `Component` that includes at least:

 - A `Feature` instantiating each strain in the sample
 - A `Feature` for the media or buffer
 - A `Feature` for each additional reagent added to the media(e.g.,inducers,antibiotics)
 - `om:Measures` on each of these specifying the amount in the sample
 - `om:Measures` on the `Component` for each environmental parameter (e.g.,temperature,pH,culturingtime)
 
 ## 4 Other Experimental Parameters
 
 In order to deal with parameters associated with the context in general but not specific instances, e.g., temperature, pH, total sample volume, the `hasMeasure` property of `Identified` can be used. The `hasMeasure` of a `Component` provides context-free information (e.g., the pH of M9 media, the GC-content of a GFP coding sequence), while the `hasMeasure` of a material entity (SBO:0000240) `Feature` provides a measurement in context (e.g., the dosage of arabinose in a sample).
 
 Values of these parameters SHOULD be specified by attaching a `om:Measure` with a `type` set to the appropriate SBO term. The SBO terms that are RECOMMENDED as appropriate are members of the Systems Description Parameter (SBO:0000545) branch of SBO. Examples include:
 
  - SBO:0000147: thermodynamic temperature (e.g.,culturing at 27 C)
  - SBO:0000332: half-life of an exponential decay(e.g.,decay rate of a gRNA)
  - SBO:0000304: pH(e.g.,pH of M9 media)
