---
title: "Pharmaceutical Services in French Community Pharmacy"
description: "Simplify the collection and storage of patient data for community pharmacists"
github_url: "https://github.com/CMagnac/Pharmaceutical-Services"
demo_url: "https://github.com/CMagnac/Pharmaceutical-Services/blob/main/Img/demo.png"
featured: true
draft: true
---
Today French Pharmacists are allowed to diagnose 2 diseases using a RADOT (Rapid Antigen Diagnostic Orientation Test) :

* Tonsillitis ;
* Cystitis.

If the RADOT is positive the pharmacist prescribe an antiobiotic.

The idea came from the fact that the available tool wasn't so practical. I prefer to decide base on my own method and not just on a binary decision tree.

The major problem is that we tend to think that RADOT gives us the result. No matter the clinic is. That's indeed a wrong way of thinking.

First the exclusion criteria, then the clinical analysis without forgetting the history of the patient. For tonsillitis we need to observe the amygdalis and touch the neck of the patient.

Second we need to be aware that both test are not hundred percent sure and make the difference between sensitivity and sensibility.

Evaluation des performances diagnostics
Sensibilité → capacité du test à détecter les personnes malades → taux de vrais positifs
Spécificité → capacité du test à identifier les personnes non malades → taux de vrais négatifs.
étude d'exactitude diagnostique diagnostic accuracy study

## 1. Tonsillitis RADOT diagnostic accuracy study

RADOT confirm the etiology of SGA.

Sensibility is upper than 90%
Specificity is upper than 95%

## 2. Cystitis RADOT diagnostic accuracy study

Paramètre TROD Sensibilité Spécificité
leucocytes 70-85% 85-95%
nitrites 50-70% 90-98%
leucocytes ou nitrites 75-90% 70-90%
leucocytes et nitrites plus faible très élevé

comparaison par rapport un ECBU

## Bibliography

[TROD Angine](https://www.ameli.fr/medecin/exercice-liberal/memos/pathologies-orl/depistage-prevention/test-diagnostic-rapide-trod-angine)

L'utilisation des Tests Rapide d'Orientation Diagnostic (TROD) en Pharmacie ont explosés depuis la pandémie de Covid de 2021. Le TROD oriente le pharmacien et aide au diagnostic. Cette démarche médicale ne peut se dissocier d'un examen clinique.

Apprendre à mieux manipuler les TRODs revient à comprendre la différence entre la sensibilité et la spécificité d'un test. La sensibilité mesure la capacité d'un test à donner un résultat positif quand l'hypothèse est vérifiée. La spécificité mesure la capacité d'un test à donner un résultat négatif quand l'hypothèse n'est pas vérifiée.

Les résultats de l'évaluation d'un test sont classés en quatre catégories :

* vrais positifs, (nombre d'individu positif au test et étant malade) ;
* faux positifs, (nombre d'individu positif au test et n'étant pas malade) ;
* faux négatifs, (nombre d'individu négatif au test et étant malade) ;
* vrais négatifs, (nombre d'individu négatif au test et n'étant pas malade).

Les résultats d'un test sont présentés dans le tableau suivant.

| Résultat du Test | Malade       | Non Malade   |
| ---------------- | :----------: | :----------: |
| Test Positif     | Vrai Positif | Faux Positif |
| Test Négatif     | Faux Négatif | Vrai Négatif |

Avec :

* Sensibilité = Vrai Positif / Vrai Positif + Faux Négatif
* Spécificité = Vrai Négatif / Vrai Négatif + Faux Positif

Exemples d'évaluation des TRODs :

| Pathologies                    | Sensibilité      | Spécificité |
| ------------------------------ | :--------------: | :---------: |
| Covid-19                       | >90%             | >99%        |
| Grippe                         | 70%              | >99%        |
| Hépatite  B                    | 60-95%           | >99%        |
| Hépatite C                     | 97%              | >99%        |
| Paludisme                      |  95%             | 95%         |
| Streptocoque A bêta-hémolytique|  85%             | 95%         |
| Syphilis                       |  >95%            | >95%        |
| VIH                            |  >99%            | >99%        |
| VRS                            |  75%             | >99%        |

## Bibliographie

* Référence tableau Pathologies Sensibilité Spécificité : Dorozs 2026

* Source : [OpenHealht](https://success.openhealth.fr/fr/articles/3928135-sensibilite-et-specificite-d-un-test)

[Tests rapides d’orientation diagnostique (TROD) et bon usage des antibiotiques](https://www.sciencedirect.com/science/article/pii/S0987798326000733#sec0030)
