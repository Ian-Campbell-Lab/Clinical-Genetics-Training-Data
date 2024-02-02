## Clinical Genetics Training Data
This repo contains human clinician annotated dysmorphology physical exam observations. It was initially released as part of the [BioCreative VIII](https://biocreative.bioinformatics.udel.edu/tasks/biocreative-viii/track-3/).

#### Dysmorphology Physical Exam
The dysmorphology physical examination is a critical component of the diagnostic evaluation in clinical genetics. This process catalogues often minor morphological differences of the patient's facial structure or body, but it may also identify more general medical signs such as neurologic dysfunction. The findings enable correlation of the patient with known rare genetic diseases. They therefore directly influence clinical diagnosis, the selection of genetic testing, and the interpretation of results---particularly when testings reveals variants of uncertain clinical significance. Beyond the clinic, such information is also useful to researchers attempting to delineate undescribed genetic conditions or to further our understanding of existing ones.

Whereas the medical findings are key information, they are nearly always captured within the electronic health record (EHR) as unstructured free text, making it unavailable for downstream computational analysis. Advanced Natural Language Processing methods are therefore required to retrieve the information from the records.

Dysmorphology physical examinations are frequently documented in the EHR as a series of organ system observations. For example:
```
PHYSICAL EXAMINATION
FACE: slightly inverted triangular face shape
EYES: long palpebral fissures with slight downslant. Sparse lateral eyebrows.
EARS: Thin inferior helices, low-set
NOSE: Short, wide nasal bridge. Anteverted nares.
MOUTH: thin upper lip; palate intact
CHEST: supernumerary nipple inferior to left nipple
HANDS FEET: Long fingers, normal toes
NEUROLOGIC: Resting tremor. Wide-based, unsteady gate.
```

#### Dataset
Our dataset consists of 3,136 organ system observations extracted from dysmorphology physical examinations of 1,652 pediatric patients evaluated at the Children's Hospital of Philadelphia. Four physicians and one medical student annotated all mentions of key positive findings as well as normal findings in the observations. They assigned each finding to its most detailed and unambiguous term in the HPO ontology. To preserve patient privacy, we automatically de-identified the text using NLM Scrubber and manually reviewed its outputs during our annotation process. We double-annotated a subset of 890 observations in our corpus and found 76% of complete agreement between the annotators.

For each observation, the publicly available dataset contains: i. the observation ID identifying uniquely the observation in our corpus; ii. the text of the observation; it always starts with an organ system followed by the description of the findings, in free text; iii. a term ID from the HPO ontology associated to a finding mentioned in the observation; iv. the starts and ends of the spans of text denoting the finding; v. polarity of the finding, if the cell is empty, the finding is a key finding, if the cell contains an X, the finding is normal.
```
Observation ID    Text                                                    HPO Term    Spans         Polarity
D433F04E6AD5E56   EYES: partial synophrys, long lashes, horizontal slant  HP:0000664  14-23	
D433F04E6AD5E56   EYES: partial synophrys, long lashes, horizontal slant  HP:0000527  25-36            	
8A1EEF66A345576   MOUTH: normal lips, tongue, high palate                 HP:0000218  28-39            	
8A1EEF66A345576   MOUTH: normal lips, tongue, high palate                 HP:0000159  7-18          X
8A1EEF66A345576   MOUTH: normal lips, tongue, high palate                 HP:0000157  7-13, 20-26   X
879246677902DE5   NEUROLOGIC: very active                                 NA          NA            NA
```
Note 1: If an observation mentions 2 or more findings, the observation is repeated 2 or more times, one finding per repetition as shown in the table above (for ex. observation 8A1EEF66A345576). The test set will just contain the observation ID and the text of the observation.<br>
Note 2: Mentions of findings can span multiple and discontinuous segments of text. When they do, we report the start and end positions of each segment in order of occurrence in the text, all segments separated by commas.<br>
Note 3: The HPO ontology does not have terms to denote normal findings. As an alternative to this current limitation, when this was possible, we normalized normal findings with the most generic terms of their corresponding key findings in the ontology and negated the findings; when it was not possible, i.e. no generic terms were available to normalize the findings, we just normalized the finding with Not Available (NA).<br>
Note 4: Not all terms in the HPO are observable during a dysmorphology physical examination and can be ignored by a normalizer. The list of irrelevant terms for the task will be shared with the registered participants.<br>

For more information, see our pre-print here: [PhenoID, a language model normalizer of physical examinations from genetics clinical notes](https://www.medrxiv.org/content/10.1101/2023.10.16.23296894v2)

