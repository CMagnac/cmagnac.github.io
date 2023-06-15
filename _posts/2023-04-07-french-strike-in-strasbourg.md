---
layout: post
title:  French Strike in Strasbourg
date:   2023-04-07 08:00:00
description: The Double-Edged Sword 
tags: false
categories: Nohealth-actuality
---

The 49.3 is a constitutional provision that the government can use to pass a bill without a vote. It has been used by Elizabeth Born eleven times since 2022, which engages the government's responsibility. Only a motion of censure can be voted to kick off the law.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/barchart1.png" title="The bar chart shows the government's commitments and censorship motions since 1958" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/barchart2.png" title="Another bar chart displays the number of demonstrators throughout France since the start of the strikes on January 19th, 2023." class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<div class="caption">
    Michel Rocard had used the most government commitments.<br>
    The gap between the General Confederation of Labour (GCL) and the Minister of the Interior's (MI) estimation is huge.
</div>

Compared to other European countries, France possesses one of the lowest rates of pensioners at risk of poverty. However, the new financial reform will raise the retirement age to 64 or 65 from 62. A series of strikes began on January 19th, 2023. These strikes are a "rare show of unity" and involve many workers such as transport and energy workers, teachers, dockers, and public sector workers.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/manif1.jpg" title="The head of the procession with banner '49.3 or not: for withdrawal we continue' at Place Broglie" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/manif2.jpg" title="A SUD rail union demonstrator with a red smoke device" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Head of the procession at Place Broglie (Bröjel) & a SUD rail Union demonstrator.
</div>

On March 28, 2023, 13000 security agents were deployed across France. While these deployments are necessary for the security of the demonstrators, a few groups known as "Black block" challenge police security.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/manif3.jpg" title="A demonstrator holds a caricatural sign of Emmanuel Macron " class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/manif4.jpg" title="Security personnel facing demonstrators at Place Kléber" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Emmanuel Macron caricature & the security personnels at Place Kléber (Kleberplatz).
</div>

Despite the support of 70% of the French population, the government has not bowed yet. A question still remains unanswered: even if the 49.3 is a constitutional text, is it really democratic?

## Chart Code

```python
## import pandas in both cases
import pandas as pd
#################
## First chart ##
#################
prime_minister = ["E.Borne", "E.Philippe", "M.Valls", "D.Villepin", "JP.Raffarin", 
                  "A.Juppé", "E.Balladur", "P.Bérégovoy", "E.Cresson", "M.Rocard",
                  "J.Chirac", "L.Fabius", "P.Mauroy", "R.Barre", "G.Pompidou", "M.Debré"]
liability_commitments = [11, 1, 6, 1, 2, 2, 1, 3, 8, 28, 8, 4, 7, 8, 6, 4]
censorship_motions = [12, 1, 3, 0, 2, 2, 1, 1, 2, 5, 7, 1, 6, 7, 4, 4]
df = pd.DataFrame({"corresponding censorship motions": censorship_motions,
                   "number of liability commitments": liability_commitments},
                   index=prime_minister)
ax = df.plot.barh(title="Government commitments and censorship motions since 1958")
for container in ax.containers:
    ax.bar_label(container,padding=1,fontsize=6)
##################
## Second chart ##
##################
date = ["28/03","23/03","15/03","11/03","07/03","16/02","11/02","07/02","31/01","19/01"]
# General Confederation of Labour
gcl = [2000000,3500000,1700000,1000000,3500000,1300000,2500000,2000000,2800000,2000000]
# Minister of the Interior
minister_interior = [740000,1080000,480000,368000,1280000,440000,963000,757000,1270000,1120000]
df = pd.DataFrame({"GCL": gcl,
                   "MI": minister_interior},
                   index=date)
ax = df.plot.barh(title="Number of demonstrators throughout France since the start of strikes")
for container in ax.containers:
    ax.bar_label(container,padding=1,fontsize=6)
```

<br>

### References

* The [official data](https://www.assemblee-nationale.fr/dyn/decouvrir-l-assemblee/engagements-de-responsabilite-du-gouvernement-et-motions-de-censure-depuis-1958) about the government commitments and censorship motions.
* An [article](https://www.vie-publique.fr/fiches/19494-le-recours-larticle-493-de-la-constitution) on the 49.3.
* The [data](https://fr.wikipedia.org/wiki/Mouvement_social_contre_le_projet_de_r%C3%A9forme_des_retraites_en_France_de_2023#Nombre_de_manifestants_et_manifestantes) that I used for the number of demonstrators chart.
