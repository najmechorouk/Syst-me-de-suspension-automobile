# SYSTÈMES DE SUSPENSION PASSIVE, SEMI-ACTIVE (SKYHOOK) ET ACTIVE (SKYHOOK + LQR)  
Modélisation et simulation d’un quart de véhicule sous MATLAB/Simulink

Ce dépôt contient l’ensemble des modèles, équations, figures et résultats de simulation liés à l’étude comparative de trois architectures de suspension automobile : passive, semi-active commandée par Skyhook, et active commandée par une stratégie hybride (Skyhook + LQR).  
Les modèles sont réalisés sous MATLAB/Simulink et reposent sur un modèle à quart de véhicule (2DDL), suivant la littérature spécialisée et les ressources académiques de référence (Sammier, thèses et travaux institutionnels sur la dynamique verticale du véhicule).

---

## 1. Présentation générale

L’objectif de ce projet est l’analyse, la modélisation et la comparaison des performances dynamiques de trois systèmes de suspension :

- Suspension passive  
- Suspension semi-active (commande Skyhook)  
- Suspension active (Skyhook étendu + commande LQR)

Le modèle utilisé représente un quart de véhicule composé d’une masse suspendue, d’une masse non suspendue, d’un ressort, d’un amortisseur et éventuellement d’un actionneur.

---

## 2. Objectifs du projet

- Comparer les réponses temporelles pour une même excitation route.  
- Évaluer le confort (accélération de la masse suspendue).  
- Examiner la tenue de route (dynamique de la masse non suspendue).  
- Étudier l'apport des stratégies Skyhook et LQR.  
- Démontrer l’intérêt des suspensions actives.

---

## 3. Modélisation théorique


### Modèles Simulink

| Fichier Simulink | Description |
|------------------|-------------|
| `quart_vehicule_suspension_passive.slx` | Modèle 2DDL de la suspension passive |
| `quart_vehicule_suspension_semi_active.slx` | Modèle avec amortissement contrôlé (Skyhook) |
| `quart_vehicule_suspension_active.slx` | Modèle avec actionneur (Skyhook + LQR) |


### 3.1. Suspension passive
La suspension passive est composée principalement d’un ressort, qui assure le support de la charge et absorbe les irrégularités de la route, et d’un amortisseur, qui dissipe l’énergie des oscillations pour limiter les vibrations du châssis. 
La modélisation mathématique d’une suspension passive repose sur un modèle à deux degrés de liberté (2DDL) dans le cas d’un quart de véhicule, où la masse suspendue représente une partie du châssis et la masse non suspendue correspond à la roue et aux composants attachés.

![la modélisation de la suspension passive d’un quart véhicule](susp passive model quart vehicul.PNG)

Les équations du mouvement sont obtenues en appliquant la deuxième loi de Newton à chaque masse, intégrant les forces exercées par le ressort et l’amortisseur ainsi que l’excitation induite par le profil de la route. Ce modèle permet d’analyser la réponse du système en termes de confort (accélérations du châssis) et de tenue de route (contact roue-sol).

![Les équations du mouvement obtenues](equation de susp passive.PNG)  

avec:
x0 : Entrée de la route (excitation de la route), représentant les irrégularités du sol.
x1 : Déplacement de la masse suspendue (châssis ou carrosserie du véhicule).
x2 : Déplacement de la masse non suspendue (roue et suspension inférieure).
m1/m2 : masse du châssis/masse du pneu.
Les paramètres mécaniques du système sont :
k1 : Raideur du ressort de suspension (relie la masse suspendue à la masse non suspendue).
k2 : Raideur du pneu (relie la roue au sol, modélisant la rigidité du pneu).
c1 : Coefficient d’amortissement de l’amortisseur de suspension (dissipe l’énergie des oscillations entre la masse suspendue et la masse non suspendue).
c2 : Coefficient d’amortissement du pneu (modélise l’amortissement interne du pneu).

Le schéma en bloc obtenu à l’aide du Simulink :
![le schéma bloc de la modélisation de la suspension passive d’un quart véhicule sur SImulink](sus passive.png) 

---

### 3.2. Suspension semi-active (Skyhook)
La suspension semi-active est une technologie qui améliore le confort et la stabilité d'un véhicule en contrôlant activement la rigidité de ses amortisseurs. Contrairement aux systèmes de suspension passive, qui sont rigides et ne peuvent pas ajuster leurs propriétés pendant le fonctionnement, les suspensions semi-actives modifient la réponse du système en fonction des conditions de conduite, telles que la vitesse ou la qualité de la route.

![la modélisation de la suspension semi-active d’un quart véhicule](susp semiactive model quart vehicul.PNG)

La modélisation de la suspension semi-active peut se faire en utilisant des équations différentielles qui décrivent la dynamique du véhicule, en incluant des éléments comme des ressorts, des amortisseurs et un dispositif de contrôle pour ajuster l’amortissement.
Les contrôleurs, comme les algorithmes de contrôle optimal ou les systèmes de commande adaptatifs, sont utilisés pour déterminer les réglages optimaux des amortisseurs en fonction des conditions.

La suspension semi-active ajuste dynamiquement l’amortissement selon une loi Skyhook :
![Les équations du mouvement obtenues](equation de susp semiactive.PNG)  
où :
Cs : (Amortissement Skyhook) : contrôle l'amortissement en fonction de la vitesse absolue du châssis pour améliorer le confort.
Fa : la force d'amortissement liée à la vitesse du châssis par rapport à un "ancre" fixe (Skyhook). Il aide à réduire les oscillations en s'opposant au mouvement du châssis seul, indépendamment de la roue.

Le schéma en bloc obtenu à l’aide du Simulink :
![le schéma bloc de la modélisation de la suspension semi-active d’un quart véhicule sur SImulink](sus semi.png) 

---

### 3.3. Suspension active (Skyhook + LQR)
La modélisation d’une suspension active repose sur une approche dynamique qui intègre à la fois la mécanique des systèmes et les principes de contrôle en temps réel.
Techniquement, la suspension active est représentée par un ensemble de masses suspendues, des ressorts, des amortisseurs et des actionneurs électromécaniques ou hydrauliques capables de générer des forces de suspension contrôlées. 

Le système est modélisé par des équations différentielles qui décrivent le comportement de la masse
suspendue (le véhicule) et non suspendue (les roues).
Le contrôle de cette suspension active implique l'utilisation d'un régulateur, souvent basé sur des stratégies de contrôle optimal ou adaptatif, qui ajuste les forces en fonction des informations recueillies par des capteurs mesurant les déplacements et les vitesses relatives. Ces forces agissent sur les actionneurs pour maintenir une réponse dynamique optimale, réduisant ainsi les vibrations et améliorant la stabilité du véhicule dans des conditions de conduite variées.

La commande utilisée combine la commande LQR et la commande Skyhook étendue qui combine l'amortissement Skyhook classique (qui dépend uniquement du mouvement du châssis) avec un terme d'amortissement relatif (qui dépend du mouvement relatif entre le châssis et la roue).
En d'autres termes, cette formulation ajuste la force de commande en fonction à la fois de la vitesse du châssis et de la différence de vitesse entre le châssis et la roue, ce qui permet d'obtenir un contrôle plus efficace des oscillations.

![Les équations du mouvement obtenues](equation de susp active.PNG)
Où:
Cr (Amortissement relatif) : agit entre la roue et le châssis pour optimiser la tenue
de route.
K : gain matriciel LQR

Nous utilisons la commande Skyhook étendue pour modéliser et contrôler la force Fa des actionneurs et l’algorithme de LQR pour avoir la valeur du gain pour l’expression de Fa.

Le schéma en bloc obtenu à l’aide du Simulink :
![le schéma bloc de la modélisation de la suspension active d’un quart véhicule sur SImulink](sus activ.png) 

---

## 4. Simulation et analyse

Les valeurs des paramètres proviennent de travaux académiques et notamment de la thèse de Damien Sammier.

![Valeurs paramètres](valeur des cst.PNG)

---

### 4.1. Simulation – Suspension passive

![courbe de la suspension passive](corb sus pass.png) 


---

### 4.2. Simulation – Suspension semi-active

![courbe de la suspension semi_active](courb sus semi.png) 

---

### 4.3. Simulation – Suspension active

![courbe de la suspension active](corb sus activ.png)  


---

## 4.4 Résultats générals
L’analyse met en évidence l’apport déterminant de la suspension active par rapport à la suspension passive. Les résultats montrent une réduction des vibrations de 91,9 %, traduisant une nette amélioration du confort et de la stabilité. Le temps d’amortissement diminue de 85,1 %, ce qui confirme une capacité accrue à dissiper rapidement l’énergie vibratoire. Enfin, la vitesse de réponse est environ 6,7 fois plus élevée, démontrant une réactivité supérieure du système actif face aux irrégularités de la route. L’ensemble de ces indicateurs confirme la supériorité fonctionnelle de la suspension active dans les conditions étudiées.




