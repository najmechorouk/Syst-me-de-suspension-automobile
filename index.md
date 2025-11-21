
# SYSTÈMES DE SUSPENSION PASSIVE, SEMI-ACTIVE (SKYHOOK) ET ACTIVE (SKYHOOK + LQR)  
Modélisation et simulation d’un quart de véhicule sous MATLAB/Simulink

Ce dépôt contient l’ensemble des modèles, équations, figures et résultats de simulation liés à l’étude comparative de trois architectures de suspension automobile : passive, semi-active commandée par Skyhook, et active commandée par une stratégie hybride (Skyhook + LQR).  
Les modèles sont réalisés sous **MATLAB/Simulink** et reposent sur un **modèle à quart de véhicule (2DDL)**, suivant la littérature spécialisée et les ressources académiques de référence (Sammier, thèses et travaux institutionnels sur la dynamique verticale du véhicule).

---

## 1. Présentation générale

L’objectif de ce projet est l’analyse, la modélisation et la comparaison des performances dynamiques de trois systèmes de suspension :

- Suspension **passive**
- Suspension **semi-active (commande Skyhook)**
- Suspension **active (Skyhook étendu + commande LQR)**

Le modèle utilisé représente un **quart de véhicule**, constitué d’une masse suspendue, d’une masse non suspendue, d’un ressort de suspension, d’un amortisseur et, selon le cas, d’un actionneur capable de générer une force contrôlée.

---

## 2. Structure du dépôt

### Modèles Simulink

| Fichier Simulink | Description |
|------------------|-------------|
| `quart_vehicule_suspension_passive.slx` | Modèle 2DDL de la suspension passive |
| `quart_vehicule_suspension_semi_active.slx` | Modèle avec amortissement commandé (Skyhook) |
| `quart_vehicule_suspension_active.slx` | Modèle avec force d’actionneur contrôlée (Skyhook + LQR) |

### Figures – Équations – Modèles

| Élément | Fichiers associés |
|--------|--------------------|
| Équations de modélisation – Suspension passive | `equation de susp passive.PNG` |
| Figure du modèle passif | `susp passive model quart vehicul.PNG` |
| Équations de modélisation – Suspension semi-active | `equation de susp semiactive.PNG` |
| Figure du modèle semi-actif | `susp semiactive model quart vehicul.PNG` |
| Équations de modélisation – Suspension active | `equation de susp active.PNG` |
| Valeurs numériques des paramètres | `valeur des cst.PNG` |

### Figures de simulation

| Type | Fichiers associés |
|------|-------------------|
| Courbes suspension passive | `corb sus pass.png` / `sus passive.png` / `courbe de la suspension passive.png` |
| Courbes suspension semi-active | `courb sus semi.png` / `sus semi.png` / `courbe de la suspension semi_active.png` |
| Courbes suspension active | `corb sus activ.png` / `sus activ.png` / `courbe de la suspension active.png` |

---

## 3. Modélisation théorique

### 3.1. Suspension passive

La suspension passive repose sur un système **ressort–amortisseur**, sans actionneur.  
Le modèle 2DDL comprend :

- Masse suspendue : \( m_1 \)  
- Masse non suspendue : \( m_2 \)  
- Raideurs : \( k_1 \) (suspension), \( k_2 \) (pneu)  
- Amortissements : \( c_1 \), \( c_2 \)  
- Entrée route : \( x_0 \)  

Les équations du mouvement (voir `equation de susp passive.PNG`) décrivent les dynamiques couplées des masses \(m_1\) et \(m_2\).

**Figures correspondantes :**  
`equation de susp passive.PNG`  
`susp passive model quart vehicul.PNG`

---

### 3.2. Suspension semi-active (Skyhook)

La suspension semi-active conserve la structure passive mais contrôle **le coefficient d’amortissement** via une loi Skyhook :

\[
F_a = C_s ( \dot{x}_1 - 0 )
\]

où \(C_s\) est modulé pour s’opposer au mouvement absolu du châssis.

Le modèle incorpore l’action du contrôleur et les équations associées (voir `equation de susp semiactive.PNG`).

**Figures correspondantes :**  
`equation de susp semiactive.PNG`  
`susp semiactive model quart vehicul.PNG`

---

### 3.3. Suspension active (Skyhook + LQR)

La suspension active ajoute un **actionneur contrôlé** produisant une force :

\[
F_a = C_r(\dot{x}_1 - \dot{x}_2) - K\, X
\]

où :

- \(C_r\) est l’amortissement relatif (Skyhook étendu)
- \(K\) est le gain matriciel issu du régulateur LQR
- \(X\) est le vecteur d’état

Le modèle complet est illustré dans `equation de susp active.PNG`.

**Figures correspondantes :**  
`equation de susp active.PNG`

---

## 4. Simulation et analyse

Les paramètres utilisés proviennent notamment du travail de référence de Damien Sammier (thèse : *Sur la modélisation et la commande de suspension de véhicules automobiles*).  
Les valeurs sont listées dans le document :

- `valeur des cst.PNG`

### 4.1. Résultats – Suspension passive

Figures correspondantes :  
`corb sus pass.png`  
`sus passive.png`  
`courbe de la suspension passive.png`

### 4.2. Résultats – Suspension semi-active

Figures correspondantes :  
`corb sus semi.png`  
`sus semi.png`  
`courbe de la suspension semi_active.png`

### 4.3. Résultats – Suspension active

Figures correspondantes :  
`corb sus activ.png`  
`sus activ.png`  
`courbe de la suspension active.png`

---

## 5. Contenu complémentaire du dépôt

Des figures extraites des modèles Simulink sont incluses :

- `figure de la suspension active dans le document slx.png`
- `figure de la suspension passive dans le document slx.png`
- `figure de la suspension semi_active dans le document slx.png`
- `figure de la suspension passive model quart vehicul.PNG`
- `figure de la suspension semiactive model quart vehicul.PNG`

---

## 6. Objectifs du projet

- Comparer les réponses temporelles des trois systèmes pour une même excitation route.
- Évaluer le confort (accélération de la masse suspendue).
- Examiner la tenue de route (déplacement de la masse non suspendue).
- Étudier l'effet des stratégies de contrôle Skyhook et LQR.
- Vérifier l’apport des systèmes actifs par rapport aux systèmes passifs classiques.

---

## 7. Références principales

- Travail académique : **Damien Sammier – Modélisation et commande de suspension de véhicules automobiles** (thèse).  
- Ouvrages spécialisés en dynamique automobile et vibrations.  
- Publications de recherche sur les modèles 2DDL, Skyhook, LQR et contrôle actif des suspensions.  
- Articles scientifiques et rapports institutionnels traitant de la dynamique verticale du véhicule et des suspensions intelligentes.

---

