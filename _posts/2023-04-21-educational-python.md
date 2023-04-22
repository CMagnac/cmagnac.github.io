---
layout: post
<<<<<<< HEAD:_posts/2023-04-21-educational-python.md
title:  Protein
date:   2023-04-21 08:00:00
=======
title:  About protein mass
date:   2023-04-22 08:00:00
>>>>>>> 9d3501f78a27bebbeb364ab8d72466533903a51d:_posts/2023-04-22-educational-python.md
description: A brief lecture on protein
tags: false
categories: Educational
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Alanine_500.png" title="chemical 2D structure of alanine" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Histidine_500.png" title="chemical 2D structure of histidine" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Serine_500.png" title="chemical 2D structure of serine" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<div class="caption">
    Alanine, Histidine and Serine
</div>

<br>

Teaching can be challenging, especially when it comes to abstract concepts. As a pharmacist, I teach basic knowledge to future pharmacy technicians. Recently, I used a new approach for those interested in informatics, combining Python with a short presentation on proteins.

I choose an example of the [Rosalind plateform](https://rosalind.info).

<br>

## The monoisotopic mass

The wikipedia definition of the monoisotopic:

<blockquote>
    Monoisotopic mass (Mmi) is one of several types of molecular masses used in mass spectrometry. The theoretical monoisotopic mass of a molecule is computed by taking the sum of the accurate masses (including mass defect) of the most abundant naturally occurring stable isotope of each atom in the molecule.
</blockquote>

It's the first peak mass of isotopic profil. The one that only take the mass of the most stable isotopes.

## Rosalind

It is an educational resource and web project for learning bioinformatics through problem solving and computer programming.

You can read the problem [here](https://rosalind.info/problems/prtm/).

### My solution

Create a json file where each letters corresponds to the protein and each float corresponds to the monoisotopic mass.

```json
{
    "A":[71.03711, "alanine", "ala"],
    "C":[103.00919, "cysteine", "cys"],
    "D":[115.02694, "aspartic acid", "asp"],
    "E":[129.04259, "glutamic acid", "glu"],
    "F":[147.06841, "phenylalanine", "phe"],
    "G":[57.02146, "glycine", "gly"],
    "H":[137.05891, "histidine", "his"],
    "I":[113.08406, "isoleucine", "ile"],
    "K":[128.09496, "lysine", "lys"],
    "L":[113.08406, "leucine", "leu"],
    "M":[131.04049, "methionine", "met"],
    "N":[114.04293, "asparagine", "asn"],
    "P":[97.05276, "proline", "pro"],
    "Q":[128.05858, "glutamine", "gln"],
    "R":[156.10111, "arginine", "arg"],
    "S":[87.03203, "serine", "ser"],
    "T":[101.04768, "threonine", "thr"],
    "V":[99.06841, "valine", "val"],
    "W":[186.07931, "tryptophan", "trp"],
    "Y":[163.06333, "tyrosine", "tyr"]
}
```

Create a python file named prtm.py where you write the code.

```python
import argparse
import json
import re

# open and load the json file
with open("aminoacid_dict.json","r",encoding="utf-8") as jsonfile:
    aminoacid_dict = json.load(jsonfile)

def protein_mass(protein_string) -> float:
    """ Return the sum of the protein string rounded with 3 digits
    """
    return round(sum([aminoacid_dict[p][0] for p in protein_string]), 3)

def has_valid_pattern(input_string) -> bool:
    """ Return a boolean value to check the integrity of the input
    """
    pattern = re.compile(r'^[ACDEFGHIKLMNPQRSTVWY]+$')
    return bool(pattern.match(input_string))

if __name__ == "__main__":
    # Create ArgumentParser object
    dscp = "Calculate the protein mass of a protein string P of length at most 1000 aa."
    parser = argparse.ArgumentParser(description=dscp)
    # Define the arguments
    parser.add_argument('-i', '--input', type=str, required=True, help='Input a protein string')
    # Parse the arguments
    args = parser.parse_args()
    # Access the argument values
    input_string = args.input
    # Check the conditions
    if has_valid_pattern(input_string) and len(input_string) <= 1000:
        print("The protein mass is:", protein_mass(input_string))
    else:
        print("Enter a valid pattern")

```

Run the code in the command line with the protein string.

```bash
python prtm.py -i SKADYEK
```

This should output 821.392.

<br>

## Applications

There are many applications of mass spectrometry in medicine, such as bacteriology-mycology (identification and therapeutic strategy), biochemistry, therapeutic and pharmacological follow-up, and toxicology dosage.

The **MALDI-TOF** (Matrix Assisted Lazer Desorption / Ionization – Time of Flight) spectrometry was invented by Joseph Thomson in 1912.

Micro-organisms co-crystallized with a matrix are deposited onto a slide. The laser disintegrates the crystals, breaks apart the micro-organisms, and ionizes the fragments.

Positively charged peptides/proteins are propelled through an electric field and pass through a vacuum tube.

At the other end, a negatively charged detector is placed. The time it takes for the molecules to reach the detector is proportional to their mass: the smallest and lightest peptides/proteins will reach the detector the fastest.

Mass spectrometry of the peptides/proteins can be performed, with the resulting spectrum being specific to an organism and available in a database for the identification of the corresponding germ.

This procedure from sample deposition to result takes 5 to 10 minutes. The sample can consist of bacteria from a blood culture.

### References

* [alanine](https://pubchem.ncbi.nlm.nih.gov/compound/5950)
* [histidine](https://pubchem.ncbi.nlm.nih.gov/compound/6274)
* [serine](https://pubchem.ncbi.nlm.nih.gov/compound/5951)
