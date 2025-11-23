# README – Système de Suspension Automobile (Passive, Semi-Active Skyhook, Active Skyhook + LQR)

## 1. Présentation générale

Ce projet présente la modélisation, la simulation et l’analyse comparative de trois architectures de suspension automobile pour un quart de véhicule (modèle 2DDL) :

* Suspension passive
* Suspension semi-active commandée par la loi Skyhook
* Suspension active utilisant une stratégie hybride Skyhook + LQR

L’objectif est d’évaluer l’impact de chaque architecture sur le confort, la tenue de route et la dynamique verticale du véhicule sous une même excitation route.

## 2. Objectifs du projet

* Modéliser chaque suspension selon la littérature académique.
* Développer les modèles sous MATLAB/Simulink.
* Comparer les réponses temporelles pour une même excitation.
* Étudier :

  * Les accélérations de la masse suspendue (confort)
  * Le déplacement de la masse non suspendue (tenue de route)
  * La rapidité d’amortissement
* Démontrer l’apport des stratégies Skyhook et LQR.

## 3. Structure du dépôt

```
/models        → modèles Simulink (passive, semi-active, active)
/equations     → équations du mouvement et matrices d’état
/simulations   → résultats des simulations et figures
index.md
/Images        → schémas Simulink, equations, résultats
README.md
```

## 4. Modélisation théorique

### 4.1. Modèle 2DDL – Suspension passive

* Deux masses : masse suspendue (châssis) et masse non suspendue (roue).
* Un ressort et un amortisseur linéaire.
* Entrée : excitation route.

Les équations du mouvement décrivent :

* Le confort : accélérations de la masse suspendue.
* La tenue de route : variation du contact roue-sol.

### 4.2. Suspension semi-active – Skyhook

* Amortissement ajusté dynamiquement.
* Loi Skyhook appliquée sur la vitesse absolue du châssis.
* Amélioration du confort et de la dissipation oscillatoire.

### 4.3. Suspension active – Skyhook + LQR

* Ajout d’un actionneur produisant une force contrôlée.
* Utilisation d’un régulateur LQR pour le calcul du gain optimal.
* Stratégie hybride : Skyhook étendu + contrôle optimal.

## 5. Modèles Simulink

Les fichiers Simulink incluent :

* Structure du modèle passif
* Modèle semi-actif avec gestion de l’amortissement contrôlé
* Modèle actif intégrant l’actionneur et la commande LQR

Les schémas détaillés sont disponibles dans `/images`.

## 6. Simulation et analyse

Les simulations utilisent les paramètres issus de travaux académiques, notamment la thèse de Damien Sammier.

### 6.1 Suspension passive

Caractéristiques observées via les courbes :

* Vibrations élevées
* Temps d’amortissement long
* Réactivité faible

### 6.2 Suspension semi-active

Améliorations :

* Réduction significative des oscillations
* Dissipation plus rapide

### 6.3 Suspension active

Performances supérieures :

* Réduction des vibrations : **91,9 %**
* Temps d’amortissement réduit : **85,1 %**
* Vitesse de réponse augmentée d’un facteur **≈ 6,7**

Les courbes sont disponibles dans `/simulations`.

## 7. Exécution des modèles

### Ouvrir et lancer les simulations

1. Ouvrir MATLAB/Simulink
2. Charger les fichiers `.slx` dans `/models`
3. Lancer la simulation depuis Simulink
4. Visualiser les résultats dans `/simulations`

## 8. Références

* Sammier D., Étude des suspensions actives et semi-actives, thèse académique.
* Ressources institutionnelles sur la dynamique verticale du véhicule.

## 9. Licence

Projet académique libre d’utilisation dans un cadre non commercial.
