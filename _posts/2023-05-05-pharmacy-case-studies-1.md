---
layout: post
title:  Pharmacy Case Studies 1
date:   2023-05-05 18:00:00
description: Treatment of an Occupational Disease
---

Trichloroethylene is a chlorinated solvent used for cleaning metals. It is a carcinogenic compound that may cause kidney cancer, liver cancer, or non-Hodgkin's lymphoma. Exposure to it for a few months may be enough to inhale and further develop any of the aforementioned diseases. Countries have defined legal exposure values for workers, presented in the following chart.

Recently, a patient presented me with two prescriptions, which I will discuss later in this post.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Trichloroethylene_500.png" title="chemical 2D structure of trichloroethylene" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/barchart3.png" title="bar chart of occupational exposure limits for trichloroethylene worldwide" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
Trichloroethylene, Figure on exposure limits for trichloroethylene
</div>

<br>

The data came from GESTIS International Limit Values – Databases hazardous substances. Institute for Work Protection of the German Accident Insurance.

The International **Time-Weighted Averages** (TWAs, 8-hour time-weighted average) for trichloroethylene vary considerably from less than 100 mg/m<sup>3</sup> in Australia and many European countries to more than 500 mg/m<sup>3</sup> in the United Kingdom and the USA.

Some specificities depend on the country:

* In **Germany** where there are no TWA, the Committee on Hazardous Substances provides data.
* In **USA1**: Data were provided by the Occupational Safety and Health Administration.
* In **USA2**: Data were provided by American Conference of Governmental Industrial Hygienists.
* Both **Hungary** and **Sweden** had no TWA.

Chemical agent exposure is a matter of concern and depends on the profession. It may increase the risk of **serious illnesses**, such as cancer.

* Asbestos: lung cancer, larynx cancer, pleural mesothelioma, ovary cancer
* Silica: lung cancer, larynx cancer
* Benzene: leukemia
* Trichloroethylene: kidney cancer

<br>

## A Pharmacy Case

A 60-year-old male had been exposed during his military service when he was twenty years old.

He presented himself at the pharmacy with two prescriptions.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Peginterferon_Alfa_500.png" title="chemical 2D structure of Peginterferon-alfa-2a" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Escitalopram_500.png" title="chemical 2D structure of escitalopram" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Prazepam_500.png" title="chemical 2D structure of prazepam" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<div class="caption">
    Peginterferon &alpha;-2a, Escitalopram and Prazepam
</div>

<br>

The **first prescription** was established by an **oncologist** from the Strasbourg Europe Cancer Institute.

Pegasys: subcutaneous injection (SC) 90µg per week.

Pegasys is a pegylate interferon &alpha;-2a.
It's an **antiviral medicine**.

Some **characteristics** of it are:

* Its indications: chronic hepatitis (B and C), leukemia with tricholeucocyte, follicular lymphoma, malignant melanoma, multiple myeloma, late-stage kidney cancer and carcinoid tumors.
* It has a triple action: antiviral, immunomodulator and anti-proliferative.
* It requires special follow-up: a regular biological check-ups, a sufficient hydratation and neurological examinations.
* Salicylates and corticosteroids may interact with it.

One of the current side effects is anxiety and depression. That is why this patient had a **second prescription**.

* Escitalopram 10mg: 1 tablet/day
* Lysanxia&reg; 10 mg: 1 tablet if necessary

<blockquote>
    Escitalopram is a selective serotonin re-uptake inhibitor used in the treatment of major depressive disorder (MDD), generalized anxiety disorder (GAD), and other select psychiatric disorders such as obsessive-compulsive disorder (OCD).
</blockquote>

Extract from [drugbank on escitalopram](https://go.drugbank.com/drugs/DB01175).

<blockquote>
    Prazepam is a benzodiazepine used to manage more severe forms of anxiety disorders.
</blockquote>

Extract from [drugbank on prazepam](https://go.drugbank.com/drugs/DB01588).

<br>

### Bart Chart Python Code

```py
import pandas as pd

country_list = ["United Kingdom", "USA2", "France", "Hungary", "USA1", "Canada",
                "New Zealand", "Singapore", "Switzerland", "Germany", "Denmark","Belgium", "Australia", "Sweden", "Austria"]
concentration = [550, 537, 405, 270, 269, 269, 269, 269, 260, 60, 55, 55, 54, 50, 3.3]
df = pd.DataFrame({"concentration (mg/m$^3$)": concentration},
                   index = country_list)
ax = df.plot.barh(title = "Occupational exposure limits for trichloroethylene worldwide")
for container in ax.containers:
    ax.bar_label(container, padding=1, fontsize=8)
```

<br>

### Pubchem References

* [Escitalopram](https://pubchem.ncbi.nlm.nih.gov/compound/146570)
* [Peginterferon Alfa-2a](https://pubchem.ncbi.nlm.nih.gov/substance/135347948)
* [Prazepam](https://pubchem.ncbi.nlm.nih.gov/compound/4890)
* [Trichloroethylene](https://pubchem.ncbi.nlm.nih.gov/compound/6575)
