---
layout: post
title:  Focus on DNA
date:   2023-05-13 08:00:00
description: Object-Oriented Programming in Python
---

Last week, students asked me to explain a fundamental concept in biology: the translation and transcription process.

This gave me the idea to use our knowledge in computer science to apply theory in an experimental way. Indeed, we are all addicted to Python.

On one hand, I presented a brief summary of the definition because basics are so important.

On the other hand, we implemented a Python object solution to two questions from the Rosalind platform.

Finally, I will describe some diseases that result from genetic disorders.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/brightdna.jpg" title="blue dna chromosome banner with white background" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <a href="https://www.freepik.com/free-vector/dna-chromosome-banner-concept_10817264.htm#query=genetic&position=10&from_view=search&track=sph">Image by zaie</a> on Freepik
</div>

<br>

## Bunch of Definitions

Let's begin with two Wikipedia definitions about DNA and RNA.

<blockquote>
The DeoxyriboNucleic Acid or DNA is a polymer composed of two polynucleotide chains that coil around each other to form a double helix.

The RiboNucleic Acid or RNA is a polymeric molecule essential in various biological roles in coding, decoding, regulation and expression of genes.
</blockquote>

**Transcription** is the process of copying a segment of DNA into RNA.

**Translation** is the process in which ribosomes synthesize proteins after the transcription process.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/genetics.png" title="diagram to explain the transcription and translation process" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    From genotype to phenotype diagram.
</div>

<br>

## Our Solutions

I choose two examples from the Rosalind website. In Python

* [Transcribing DNA to RNA](https://rosalind.info/problems/rna/)
* [Translating RNA into Protein](https://rosalind.info/problems/prot/)

<br>

### Focus on Property

In Python, *property()* is a **built-in function** that creates and returns a property object.

```python
property(fget=None, fset=None, fdel=None, doc=None)
```

* fget is function to **get value** of the attribute.
* fset is function to **set value** of the attribute.
* fdel is function to **delete** the attribute.
* doc is a string (like a comment).

It defines **the properties of an object**.

When it comes to coding, you always want to make things complex. As suggested in **PEP20**, simplicity is better than complexity.

<br>

### Simplify the Problem

Even though some RNA molecules, such as transfer RNA (tRNA) and ribosomal RNA (rRNA), have other functions in the cell and do not follow the **three-nucleotide codon rule**, I decided to narrow the scope to the three-length codon rule.

Note the difference between **continue** and **break** statement in the **rna_translation** definition.

If you replace **continue** with **break**, you won't get the expected output in the case of a stop codon.

**First step**: create a JSON file, **rnacodon_table.json**. We will use the file to translate RNA into the amino acids.

```json
{
    "UUU": "F", "CUU": "L", "AUU": "I", "GUU": "V", "UUC": "F", "CUC": "L",
    "AUC": "I", "GUC": "V", "UUA": "L", "CUA": "L", "AUA": "I", "GUA": "V",
    "UUG": "L", "CUG": "L", "AUG": "M", "GUG": "V", "UCU": "S", "CCU": "P",
    "ACU": "T", "GCU": "A", "UCC": "S", "CCC": "P", "ACC": "T", "GCC": "A",
    "UCA": "S", "CCA": "P", "ACA": "T", "GCA": "A", "UCG": "S", "CCG": "P",
    "ACG": "T", "GCG": "A", "UAU": "Y", "CAU": "H", "AAU": "N", "GAU": "D",
    "UAC": "Y", "CAC": "H", "AAC": "N", "GAC": "D", "UAA": "Stop", "CAA": "Q",
    "AAA": "K", "GAA": "E", "UAG": "Stop", "CAG": "Q", "AAG": "K", "GAG": "E",
    "UGU": "C", "CGU": "R", "AGU": "S", "GGU": "G", "UGC": "C", "CGC": "R",
    "AGC": "S", "GGC": "G", "UGA": "Stop", "CGA": "R", "AGA": "R", "GGA": "G",
    "UGG": "W", "CGG": "R", "AGG": "R", "GGG": "G"
}
```

<br>

**Second step**: Create a python file named **genetics.py**.

```python
import json

# load the rna codon table
with open("rnacodon_table.json", "r", encoding="utf-8") as jsonfile:
    codon_dict = json.load(jsonfile)


class NucleicAcid:
    def __init__(self, nuclacid_str=None):
        self.nuclacid_str = nuclacid_str

    def rna_translation(self) -> str:
        """Take the rna string input
        Return a string of amino-acids
        """
        codon_list = []
        for i in range(0, len(self.nuclacid_str), 3):
            codon = self.nuclacid_str[i:i+3]
            if codon_dict[codon] == 'Stop':
                continue
            codon_list.append(codon_dict[codon])
        return "".join(codon_list)

    def dna_transcription(self) -> str:
        """Take the dna string input
        Return the rna string
        """
        if "U" in self.nuclacid_str:
            return "Not a DNA string"
        return self.nuclacid_str.translate({ord("T"): "U"})

    @property
    def nuclacid_str(self) -> str:
        return self._nuclacid_str

    @nuclacid_str.setter
    def nuclacid_str(self, value):
        """Take the string value of user input
        Return an error if conditions are false 
        """
        dna_chars = set('ATCG')
        rna_chars = set('AUCG')
        if not set(value).issubset(dna_chars.union(rna_chars)):
            raise ValueError('Input string contains invalid characters')
        if len(value) % 3 != 0:
            # the three-nucleotide codon rule
            raise ValueError('Input string is invalid')
        self._nuclacid_str = value


if __name__ == "__main__":
    # first test
    sample_dataset = "GATGGAACTTGACTACGTAAATTT"
    sample_output = "GAUGGAACUUGACUACGUAAAUUU"
    dna = NucleicAcid(sample_dataset)
    print(dna.dna_transcription() == sample_output)
    # second test
    sample_dataset = "AUGGCCAUGGCGCCCAGAACUGAGAUCAAUAGUACCCGUAUUAACGGGUGA"
    sample_output = "MAMAPRTEINSTRING"
    rna = NucleicAcid(sample_dataset)
    print(rna.rna_translation() == sample_output)
```

**Final step**: Run the code in the command line interpreter.

```sh
python genetics.py
```

**Expected output**:

```sh
True
True
```

<br>

Obviously, there are many imperfections, but I encourage my students to think more about them.

I will conclude with rare diseases.

<br>

## Beyond the Course

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/igmasign.jpg" title="the genetic institut acronym on a sign" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/igma.jpg" title="the genetic institut building" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Institute of Medical Genetics of Alsace (IGMA, Institut de Génétique Médicale d'Alsace)
</div>

<br>

What is a rare disease ?

A disease is called "rare" when it affects less than one person in 2,000. Some are known to the public, such as albinism, sickle-cell disease, cystic fibrosis, hemochromatosis, Duchenne muscular dystrophy, etc.

80% of rare diseases are genetic.

In the *Grand Est* region, these diseases impact more than 200,000 people.

In France, a national program offers screening for rare diseases to newborns within the first three days.

The diseases screened for are:

* Phenylketonuria
* Congenital hypothyroidism
* Congenital adrenal hyperplasia
* Sickle cell disease
* Cystic fibrosis
* MCAD deficiency

Rare diseases are a **priority** in the [ARS](https://www.grand-est.ars.sante.fr/) (Regional Health Agency) Grand Est Regional Health Project.

The fight against diagnostic and therapeutic errors, the improvement of the care pathway, and access to information are the priorities of the rare disease pathway.

<br>

### References & Images Attribution

* [Inserm report on rare disease](https://www.inserm.fr/rapport/registres-maladies-rares-et-collections-de-donnees-sur-les-maladies-rares-en-france-mars-2022/).
* [Institute of Medical Genetics of Alsace](https://www.chru-strasbourg.fr/service/institut-genetique-medicale-alsace-igma/).
* [Image by brgfx](https://www.freepik.com/free-vector/animal-cell-diagram-colors_2480897.htm#query=eukaryotic%20cell&position=4&from_view=search&track=ais) on Freepik.
* [Image by macrovector](https://www.freepik.com/free-vector/scientific-molecular-abstract-concept-with-blue-connected-atoms-realistic-style-white-isolated_11241930.htm#query=dna%20helix&position=14&from_view=search&track=ais) on Freepik.
* [Image by Freepik](https://www.freepik.com/free-vector/human-figure-dots-illustration_712896.htm#query=RNA&position=3&from_view=search&track=sph).
