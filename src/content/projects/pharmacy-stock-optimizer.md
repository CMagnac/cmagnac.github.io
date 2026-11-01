---
title: "Un outil d'analyse et de suivi des stocks en pharmacie"
description: "Un projet Python pour analyser les stocks et explorer des méthodes d'optimisation en pharmacie d'officine."
github_url: "https://github.com/CMagnac/pharmacy-stock-optimizer"
demo_url: ""
featured: true
draft: false
---

La gestion des stocks est l'une des préoccupations d'une pharmacie d'officine. L'enjeu est de disposer des médicaments nécessaires pour répondre aux besoins des patients, tout en évitant les **immoblisations financières**. À cela s'ajoutent les contraintes de stockage, les risques de péremption et les particularités de certains produits comme les **médicaments thermosensibles**.

Au cours d'un contrat de six mois, j'ai décidé d'explorer ce sujet sous l'angle de l'analyse de données. Je voulais aller plus loin et comprendre comment Python pouvait m'aider à analyser les stocks de la pharmacie.

C'est ainsi qu'est né le projet **Pharmacy Stock Optimization & Historical Monitoring System**. J'ai développé ce projet avec l'aide de ChatGPT. L'objectif n'est pas de produire du code, mais de construire un système d'analyse adapté à une problématique réelle.

## 1. Définir un périmètre réaliste et réalisable en six mois

Une pharmacie gèrent des milliers de références. Pour des raisons de temps, j'ai choisi de commencer par un groupe de médicaments répartis en deux catégories :

- Les médicaments génériques administrés par voie orale ;
- Les médicaments thermosensibles.

J'ai réalisé personnellement les inventaires mensuelles de ces deux catégories.

Le but est de construire une méthode **améliorable** dans le temps et **réplicable** dans d'autres pharmacies.

## 2. Transformer les données brutes en informations exploitables

Le projet repose sur **trois caractéristiques complémentaires** :

- des inventaires mensuelles ciblant les deux catégories citées précédemment ;
- l'historique des dispensations d'octobre 2025 à octobre 2026 ;
- un travail de préparation des données.

### 2.1 Utilisation des inventaires comme base de l'analyse de stock

Le premier inventaire **localisé**, réalisé en août 2026, constitue le point de départ du suivi des 699 produits. Ce chiffre pourra évoluer d'un mois sur l'autre en fonction des pharmaciens qui commandent et de la demande. Nous essayons de suivre une politique de deux semaines de stock sur certains produits commme les médicaments génériques administrés par voie orale.

Le second **inventaire est complet**. Il a été réalisé en septembre 2026 par une équipe spécialisée. Cette inventaire n'avait pas été réalisé depuis dix ans. L'**inventaire complet** de septembre contient **5 674 codes produits uniques** après nettoyage.

Ces données permettent d'étudier :

- la valeur estimée des médicaments ;
- les écarts d'inventaire ;
- les quantités en stock.

Lorsqu'un produit présent dans un inventaire précédent est absent du suivant, son stock n'est pas nécessairement nul. Il peut s'agir d'une erreur de comptage. Le traitement des données conserve cette distinction.

### 2.2 Historique des facturations de 2025 à 2026

La deuxième source est un **historique de facturation** couvrant une année, du **11 octobre 2025 au 10 octobre 2026**.

Après nettoyage, le jeu de données contient :

- **274 032 boîtes enregistrées comme délivrées** ;
- **6 324 codes produits uniques** ;
- **161 978 enregistrements**.

Le nettoyage a consisté à supprimer les doublons, à écarter les mouvements sans code produit et à harmoniser les quantités utilisées pour l'analyse.

### 2.3 Le travail de préparation des données

Le travail de préparation consiste à nettoyer les données pour les rendres exploitables et fiables.
J'ai donc plusieurs scripts pour importer les fichiers, normaliser les colonnes, nettoyer les enregistrements et préparer les jeux de données destinés à l'analyse.

Les fichiers bruts sont conservés séparément des données traitées. Cette organisation permet de reprendre les transformations, de vérifier les résultats et de faire évoluer le projet sans perdre les sources initiales.

Une analyse pertinente commence par des données **correctement préparées et comprises**.

## 3. Méthodes d'étude des stocks

La méthode d'étude des stocks répond à la question : comment déterminer quels médicaments méritent une attention particulière ? J'ai choisi d'explorer trois modes de classification : ABC, XYZ et FSN.

### 3.1 Mesure de l'importance économique d'un produit

L'**analyse ABC** classe les produits selon leur contribution à la **valeur totale consommée** sur une **période donnée**.

- la **classe A** : 20 % des références qui représentent 80 % de la valeur.
- la **classe B** : 30 % des références qui représentent 15 % de la valeur.
- la **classe C** : 50 % des références qui représentent 5 % de la valeur.

Cette classification aide à identifier les produits sur lesquels une **attention particulière** est nécessaire pour suivre l'économie de l'officine.

- la **classe A** nécessite un contrôle strict, un suivi quotidien et une attention prioritaire pour éviter les ruptures.
- la **classe B** fait l'objet d'un contrôle régulier et d'une gestion intermédiaire.
- la **classe C** demande un contrôle simple, minimal ou automatisé.

L'analyse ABC se réfère au **principe de Pareto**. Il s'agit de rentabiliser la politique d'approvisionnement et de définir un stock de sécurité.

### 3.2 Evaluation de la demande d'un produit

La **méthode XYZ** s'intéresse à la variabilité de la demande. Elle repose sur le coefficient de variation (CV), qui se calcule en divisant l'écart-type par la moyenne de la demande.

- la **classe X :** une demande stable et prévisible.
- la **classe Y :** une demande modérément variable.
- la **classe Z :** une demande imprévisible.

L'analyse repose ici sur les quantités délivrées chaque mois. Elle détermine si la consommation d'un produit suit un rythme relativement régulier ou si elle fluctue fortement.

Une année de données permet d'étudier certains comportements de consommation, mais ne suffit pas toujours à établir une saisonnalité fiable.

Par la suite, il est possible de combiner la matrice ABC avec XYZ. En croisant la valeur financière (ABC) et la régularité de la demande (XYZ), on obtient 9 profils stratégiques. Je n'ai pas traité ce cas de figure.

### 3.3 Fréquence de délivrance d'un produit

La **méthode FSN** classe les produits selon la fréquence de leurs entrées/sorties pendant une période de temps déterminée. C'est un outil de classification qui catégorise les articles selon leur **vitesse de rotation** et leur **fréquence d'utilisation**.

- **F comme Fast-moving :** les produits à **mouvements fréquents**. Ils nécessitent une surveillance étroite et un stock de sécurité suffisant pour éviter les ruptures.
- **S comme Slow-moving :** les produits à **mouvements moins fréquents**. Ils immobilisent du capital s'ils ne sont pas optimisés.
- **N comme Non-moving :** les produits **sans mouvement** enregistré. Ils correspondent souvent à à des excédents.

### 3.4 Intérêt de combiner ces méthodes

Les **outils ABC, XYZ et FSN** apportent trois dimensions :

- La variabilité de la demande ;
- La fréquence des mouvements ;
- L'importance économique.

L'intérêt du projet est de comparer leurs résultats, puis d'étudier ce que leur combinaison peut apporter à la gestion quotidienne.

## 4. Construction d'un outil d'analyse de stock avec Python

J'ai organisé le code en **modules distincts**, consacrés au chargement des données, aux transformations, à la validation, à l'historique et à l'analyse.

Les scripts du dossier `scripts/` permettent d'exécuter les différentes étapes du traitement. Les modules réutilisables sont regroupés dans le paquet Python `pharmacy_stock`.

Cette organisation présente plusieurs avantages :

- Les tests automatisés contribuent à vérifier que le code se comporte comme prévu ;
- Les transformations peuvent être réutilisées d'un mois à l'autre ;
- Chaque étape peut être examinée et améliorée séparément.

J'utilise Pandas pour manipuler les données, le format Parquet pour stocker les jeux de données traités et Pytest pour les tests.

Le [projet est versionné sur GitHub](https://github.com/CMagnac/pharmacy-stock-optimizer), pour suivre son évolution et documenter les choix techniques.

L'architecture n'est pas figée et évoluer au fur et à mesure que le projet avance.

## 5. De la classification à la décision

La prochaine étape consiste à utliser les résultats de ces analyses pour répondre à des questions de gestion de stock.

- Peut-on estimer une couverture de stock pertinente à partir des quantités disponibles et de la consommation moyenne ?
- Pour quels produits le stock disponible paraît-il insuffisant au regard de la demande observée ?
- Quelle part du capital est immobilisée dans des médicaments ?
- Comment évolue le stock d'un produit au fil des inventaires ?
- Quels produits semblent présenter un risque de surstock ?
- Quels produits présentent des écarts récurrents ?

## 7. Les limites du projet

Ce projet est un **prototype analytique**.

Tout d'abord, quelques inventaires successifs ne suffisent pas à décrire une évolution de stock sur une longue période. La poursuite des **inventaires mensuels** permettraient d'enrichir l'historique et d'obtenir des résultats plus pertinents.

---

En travaillant sur ce sujet, j'ai rapproché deux domaines qui m'intéressent : **la pratique officinale et le développement informatique**.

Python m'offre la possibilité de transformer des fichiers de gestion en **données structurées**
, de **tester différentes méthodes d'analyse** et de **construire progressivement un outil** adapté à un problème réel. ChatGPT m'accompagne dans ce travail, comme un **outil d'assistance et de réflexion**.

Il ne s'agit pas de remplacer le jugement professionnel du pharmacien, ni les procédures existantes, mais de disposer d'informations supplémentaires pour mieux comprendre les stocks et éclairer certaines décisions.
