---
layout: post
title:  Fighting cancerous cells resistance
date:   2023-03-31 08:00:00
description: chemotherapy treatment
tags: false 
categories: Strasbourg-institute Disease-treatment
---

In 2020, 347,000 people were treated with chemotherapy in France. A major concern in chemotherapy treatment is the emergence of cancer-resistant cells. Based on principles of evolution, new therapeutic strategies rely on adaptive therapy, which consists of alternating between treatment and no treatment periods. However, as with any public health issue, prevention is always the best approach to prevent the increase of cancer incidence.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/icans.jpg" title="Strasbourg Europe Cancer Institute" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Strasbourg Europe Cancer Institute
</div>
## Cancer types and risk-factors

Cancer is one of the leading causes of death in the richest countries. Four types of cancer represent 78% of chemotherapy sessions. Although some cancers cannot be avoided, having a healthy lifestyle may play an important role.

40% of cancers could be avoided. The proportion of cancers related to the main risk factors are: tobacco (19.8%), alcohol (8%), unbalanced diet (5.4%), overweight (5.4%), some infections (4%), occupational exposure (3%), UV radiation (3%), ionizing radiation (1.8%), lack of physical activity (0.9%), and hormonal treatment (0.6%).

The global hospital activity related to chemotherapy has increased since 2016. Health professionals are better prepared to help patients with cancer.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/chart1.png" title="Pie chart of cancer types treat by chemotherapy in France" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/chart2.png" title="Line chart of number of hospitalizations with chemotherapy in France" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Two figures on chemotherapy in France
</div>

Python code for **the pie chart**.

```python
import pandas as pd
df = pd.DataFrame({'cancer type': ["Digestive", "Breast", "Others", "Haematological", "Respiratory"],
                   '': [22, 20, 22, 20, 16]})
df.groupby(['cancer type']).sum().plot(kind="pie", y="", autopct='%1.0f%%', legend=False, 
                                       title="Cancer types treat by chemotherapy in France")
```

Python code for **the line chart**.

```python
import pandas as pd
df = pd.DataFrame({'Million per year':[2794761, 2966691, 3015831, 3124696, 3119159],
                    }, index=[2016, 2017, 2018, 2019, 2020])
lines = df.plot.line(title='Number of hospitalizations with chemotherapy in France')
```

Many types of cancer treatment depend on the type of cancer and how advanced it is. Biomarker testing is done during daily hospital practice, and it can provide information about cancer. The types of cancer treatment are: chemotherapy, hormone therapy, hyperthermia, immunotherapy, photodynamic therapy, radiation therapy, stem cell transplant, surgery, and targeted therapy.

The conventional strategy in chemotherapy was to eradicate all cancerous cells. Despite these solutions, cells can become resistant in a similar cellular mechanism that occurs during bacterial treatment resistance to antibiotics. One solution is **adaptive therapy**.

## The adaptative therapy

In 2009, Robert Gatenby proposed a new way of cancer treatment: adaptive therapy. Based on the principles of evolution by Charles Darwin, doctors administer low doses of chemotherapy drugs to reduce the selection pressure on cancerous cells. They aim to control the cancer rather than eradicate it completely. Adaptive therapy is used for incurable cancer, and the purpose of this therapy is to alternate between treatment and no treatment periods. This approach is less aggressive on the cancerous cells and decreases the natural selection of the strongest cells. However, this therapy is still under development.

### References

1. A new approach to treat cancer with adaptative therapy on [The Conversation](https://theconversation.com/traitement-du-cancer-leradication-a-tout-prix-nest-pas-forcement-la-bonne-approche-153429.
2. How to attenuate tumoral resistance ? Read this [article](https://www.letemps.ch/sciences/une-piste-attenuer-resistances-tumorales) from Le Temps.
3. You can find more informations on the data use to write this article [here](https://www.e-cancer.fr/Professionnels-de-sante/Les-traitements/Chimiotherapie/Chiffres-cles-de-la-chimiotherapie).
4. What are the different treatment type of cancer ? Read this [article](https://www.cancer.gov/about-cancer/treatment/types) to learn more about it.
5. The [Montpellier Molecular Genetics Institute](https://www.igmm.cnrs.fr/doses-faibles-de-medicaments-anticancereux-pourraient-etre-plus-efficaces/) gives us more informations on the adaptative therapy.
