# Optimisation-des-processus-de-reporting-Visualisation-des-données-Baccarat
## Projets : Optimisation d’un reporting commercial avec Excel, Power Query & Power BI   
Un fichier Excel non optimisé, multi-années, non exploitable pour le pilotage, l'analyse et la visualisation des indicateurs clés de performances.

### Contexte & Besoin
- Analyse de ventes Spontanés
- Conception de Dashboard intuitif
- Performance du rapport et des requêtes
- Fiabilité des données mais aucune necessité de les avoir en temps réel
- Mesure DAX complexe, Analyse temporelle
- Anticipé les Tableaux reporting locaux pour les 5 prochaines années
- Assurer une lecture des indicateurs directement dans les fichiers de reporting - reduire les interractions Power BI
  
### Problème rencontré 
- Données dispersées sur plusieurs feuille et dans plusieurs dossiers
- Pas de Formatage des colonnes (dates, CA HT, ventes, Articles,  passages, Qte Remise, Remise HT, Qte Détaxe, Détaxe HT, Qte VAD, VAD ht, full prices, Qte Parfum, Parfum Ht, Qté Diversification, Diversification HT)
- Pas de mise en forme conditionnel relative au weekend
- Pas de suivi dynamique d’une année à l’autre
- Calcul manuel des indicateurs : Panier moyen, Detaxe/CA, VAD/CA, Catégorie de produit (Full price, Parfum, Diversification)/CA par semaine/Mois/Année
  
  ---
  ### Tableaux de reporting Anticipé :
  - Création de fichiers reporting anticipant les futures années
  - Production de fichiers Excel optimisés avec des tableaux permettant le calcul automatisé des indicateurs,
  - Ajout de nouvelles fonctionnalités (mise en forme conditionnelle des week-ends, filtre par semaine, CA réalisé vs Objectif),

  le but est de simplifier les étapes de transformation Power Query à venir afin de gagner en performance tout en simplifiant la lecture des données lors du reporting sans avoir besoin d'ouvrir Power BI. 

  ### Étapes de traitement 
 **Power Query**  
- Filtre des sous totaux
- suppression des colonnes
- Homogénéisation des caractères
- Formatage des colonnes
- Fusion des requêtes multi-mois : les classeurs possèdent 12 feuilles mensuelles.
Après la fusion, le fichier obtenu est renommé "Données_ventesYYYY" chargé en tableau et rangé avec les autres années.

  **Power BI**
  - Fusion des requêtes multi-année : après création, transformation et fusion multi-mois des classeurs annuels, je procède à la fusion multi-année des fichiers "Donnée_ventesYYYY"
  pour obtenir une table de faits unique centralisant toutes les ventes passées et futures 2024-2030, facilitant ainsi les calculs et l’application des mesures DAX
- Création d’une table calendrier (Date Table) afin de piloter le filtrage des données de ventes:
  `Calendar = ADDCOLUMNS(
    CALENDAR(DATE(2024,01,01),DATE(2030,12,01)),
"ANNEE",YEAR([Date]),
"SEMESTRE",IF(MONTH([Date])>=6,"S2","S1"))

  **Modélisation des données**
- Table de fait : Ventes 2019-2030
- Table de dimension 1 : Table Date (clé commune = Date "JJ/MM/AAAA")
- Modèle de donnée : Modèle semantique
- Type de modèle : Star Schema
- cardinalité : 1 à plusieurs entre la table de dimension et la table de fait
- relation : filtre à sens unique
   
  **Mesures DAX** 
  - `CA = SUM(Donnée_vente[CAHT])`  
  - `CA N-1 = CALCULATE([CA], SAMEPERIODLASTYEAR(Calendar[Date]))` 
  - `Ecart = divide([CA] - [CA N-1],[CA N-1])`
  - `Panier moyen = divide([CA],sum(donnée_vente[ventes]))`
  - `PM N-1 = CALCULATE([Panier moyen], SAMEPERIODLASTYEAR(Calendar[Date]))` 
- Filtres dynamiques (année, mois) synchronisation des filtre, Page1,2,3

  **Visualisation**
   histogrammes combiné,  donut chart, Cartes 123, matrice, mise en forme conditionnel
Certaines interractions ont été modifié volontairement de sorte à ce que les visuels concernés soient dissociées de certains filtres afin de préserver une lecture stratégique globale .
En effet, Le graphique représentant l'Evolution du CA au fil des mois est indépendant du filtre "Mois" car cela nous permet de conserver une vision complète des tendances temporelles tout en garantissant une analyse de la dynamique globale du business.
   ---
  
#### Résultats quantitatifs  
- Réduction du temps de rapport manuel de 1h30 à 20 minutes automatisées (gain de productivité de 78%)
- Fiabilité des données : 98%
- Adoption de l’outil par les équipes de ventes / manager au quotidien et lors des rapports mensuels à la hiérarchie

---

#### Résultats qualitatifs   
- Visualisations intuitives et interactive permettant à des non-techniciens de comprendre les performances en un coup d’œil 
- Renforcement de la confiance du manager dans les données utilisées au quotidien
- Suivi clair des écarts année N / N-1 ainsi que des indicateurs N/N-1

---

#### Résultats personnels  
- Acquisition de compétences clés en **Excel, Power Query avancé, PowerBI, DAX et modélisation relationnelle**  
- Développement d’une pédagogie pour vulgariser la donnée auprès d’équipes non techniques  
- Capacité à mener un projet complet, de l'observation terrain à un outil exploitable et adopté  
- Démonstration d’une capacité d'adaptation et d’apprentissage rapide 
- Amélioration de ma rigueur analytique et de ma capacité à transformer les chiffres en recommandations stratégiques
- Résilience face aux difficultés techniques par la recherche et l'expérimentation


