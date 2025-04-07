# FindOrtho

# Gestionnaire de Dalles Lambert-93

## Aperçu

Ce projet fournit un ensemble d'outils pour gérer et identifier des dalles de 200m x 200m dans le système de projection Lambert-93 (EPSG:2154). Il est conçu pour déterminer quelle dalle contient un point donné ou si un polygone est complètement contenu dans une seule dalle.

## Fonctionnalités

- Calcul de l'identifiant de dalle pour tout point en coordonnées Lambert-93
- Vérification si un polygone est entièrement contenu dans une seule dalle
- Approche orientée objet avec la classe `DalleManager`
- Approche fonctionnelle avec des fonctions autonomes

## Installation

```bash
git clone https://github.com/votrenomdutilisateur/gestionnaire-dalles-lambert93.git
cd gestionnaire-dalles-lambert93
pip install -r requirements.txt
```

## Prérequis

- NumPy

## Utilisation

### En tant que module

```python
import numpy as np
from dalle_manager import DalleManager

# Créer une instance de DalleManager
dalle_manager = DalleManager()

# Trouver la dalle pour un point spécifique
x, y = 796700.85, 6302710.26  # Coordonnées Lambert-93
id_dalle = dalle_manager.dalle_pour_point(x, y)
print(f"L'identifiant de dalle est: {id_dalle[0]}_{id_dalle[1]}")  # Sortie: 7966_63028

# Vérifier si un polygone est dans une seule dalle
coords_polygone = [
    (796795.74, 6302603.69), 
    (796795.74, 6302603.69), 
    (796795.74, 6302603.69), 
    (796795.74, 6302603.69)
]
resultat = dalle_manager.verifier_polygone_dans_une_dalle(coords_polygone)
print(f"Statut de dalle du polygone: {resultat}")  # Sortie: 7966_63028 ou "hors dalle"
```

### Approche fonctionnelle

```python
from dalle_functions import trouver_dalle_hectometre_pair, verifier_polygone_dans_une_dalle

# Trouver la dalle pour un point spécifique
x, y = 796700.85, 6302710.26  # Coordonnées Lambert-93
nom_dalle = trouver_dalle_hectometre_pair(x, y)
print(f"Le nom de la dalle est: {nom_dalle}")  # Sortie: 7966_63028

# Vérifier si un polygone est dans une seule dalle
coords_polygone = [
    (796795.74, 6302603.69), 
    (796795.74, 6302603.69), 
    (796795.74, 6302603.69), 
    (796795.74, 6302603.69)
]
resultat = verifier_polygone_dans_une_dalle(coords_polygone)
print(f"Statut de dalle du polygone: {resultat}")  # Sortie: 7966_63028 ou "hors dalle"
```

## Détails techniques

### Système de dalles

- Chaque dalle mesure 200m × 200m
- Les identifiants de dalle sont exprimés en hectomètres (unités de 100m)
- Le format d'identifiant est `x_y` où:
  - `x` est la coordonnée est du coin supérieur gauche en hectomètres
  - `y` est la coordonnée nord du coin supérieur gauche en hectomètres

### Fonctions et méthodes

#### `trouver_dalle_hectometre_pair(x, y)`

Calcule l'identifiant de dalle pour un point donné.

- **Paramètres:**
  - `x` (float): Coordonnée X en Lambert-93
  - `y` (float): Coordonnée Y en Lambert-93
- **Retourne:**
  - Chaîne au format "x_y" représentant l'identifiant de la dalle

#### Classe `DalleManager`

- **`dalle_pour_point(x, y)`**
  - Calcule les coordonnées du coin supérieur gauche (en hectomètres) de la dalle contenant le point donné
  - Retourne un tuple d'entiers `(x_hm, y_hm)`

- **`verifier_polygone_dans_une_dalle(coords)`**
  - Vérifie si un polygone (défini par une liste de tuples de coordonnées) est entièrement dans une seule dalle
  - Retourne la chaîne d'identifiant de dalle si contenu dans une dalle, sinon retourne "hors dalle"

## Licence

[Spécifiez votre licence ici]

## Contributeurs

[Votre nom et autres contributeurs]
