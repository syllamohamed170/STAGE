# Bibliothèque MATLAB pour le Traitement des Modèles Numériques de Terrain (MNT)

Cette bibliothèque regroupe des fonctions MATLAB dédiées au **prétraitement**, **débruitage**, **segmentation**, et **modélisation** des Modèles Numériques de Terrain (MNT).

---

## 📌 Fonctions Principales

### 1. **Segmentation et Modélisation**
#### [`modelisation_polynomiale_superpixels.m`](https://github.com/votre-repo/modelisation_polynomiale_superpixels.m)
**Objectif** : Segmenter un MNT en superpixels (algorithme SLIC), détecter les dépressions, et approximer les régions par des surfaces polynomiales.
**Paramètres clés** :
- `MNT` : Matrice du modèle numérique de terrain.
- `n_superpixels` : Nombre de superpixels souhaités.
- `compactness` : Paramètre de compacité pour SLIC.
- `visualize` : Booléen pour afficher les résultats.
**Retourne** :
- Métriques des régions (aire, volume).
- Équations polynomiales pour chaque région.
- Visualisations 2D/3D.

**Exemple** :
```matlab
[metrics, poly_eq] = modelisation_polynomiale_superpixels(MNT, 200, 10, true);
```

#### [`approx_ellipsoide_dep.m`](https://github.com/votre-repo/approx_ellipsoide_dep.m)
**Objectif** : Approximer les dépressions d’un MNT par des formes géométriques simples (ellipses, demi-ellipses).
**Paramètres clés** :
- `MNT` : Matrice d’élévation.
- `shape_type` : Type de forme (`'ellipse'`, `'semi-ellipse'`).
**Retourne** :
- Paramètres des formes ajustées (centre, axes).
- Visualisation des dépressions modélisées.

---

### 2. **Débruitage**
#### [`debruitage_random_forest.m`](https://github.com/votre-repo/debruitage_random_forest.m)
**Objectif** : Débruiter un MNT via un modèle Random Forest.
**Paramètres clés** :
- `mnt` : MNT bruité (matrice).
**Retourne** :
- `mnt_denoised` : MNT débruité.

**Exemple** :
```matlab
mnt_clean = debruitage_random_forest(mnt);
```

#### [`fonction_min_local.m`](https://github.com/votre-repo/fonction_min_local.m)
**Objectif** : Identifier les minima locaux et appliquer un filtre gaussien pour le débruitage.
**Paramètres clés** :
- `su` : MNT d’entrée.
- `T` : Seuil pour la détection des minima.
- `sigma` : Écart-type du filtre gaussien.

---

### 3. **Prétraitement**
#### [`readFile2.m`](https://github.com/votre-repo/readFile2.m)
**Objectif** : Lire un fichier binaire et convertir les données en matrice MNT.
**Paramètres clés** :
- `filename` : Chemin vers le fichier binaire.
**Retourne** :
- `MNT` : Matrice transposée et mise à l’échelle (facteur 1/5).

**Exemple** :
```matlab
MNT = readFile2('data.bin');
```

#### [`division2.m`](https://github.com/votre-repo/division2.m)
**Objectif** : Diviser un MNT en 4 quadrants pour analyse locale.
**Paramètres clés** :
- `MNT` : Matrice d’entrée.
- `display` : Booléen pour afficher les quadrants.

---

### 4. **Fusion et Registration d’Images**
#### [`SURFMatrice.m`](https://github.com/votre-repo/SURFMatrice.m)
**Objectif** : Aligner et fusionner deux images MNT usando des caractéristiques SURF.
**Paramètres clés** :
- `image1`, `image2` : Matrices des images à fusionner.
**Retourne** :
- `fused_image` : Image fusionnée avec correction de biais.

#### [`fusionSURFPourSH.m`](https://github.com/votre-repo/fusionSURFPourSH.m)
**Variante** : Version optimisée pour les données SH (ex : images satellite).

---

### 5. **Simplification de Régions**
#### [`simplifie.m`](https://github.com/votre-repo/simplifie.m)
**Objectif** : Simplifier les régions d’une image binaire en cercles/rectangles.
**Paramètres clés** :
- `binary_image` : Image binaire d’entrée.
**Retourne** :
- `simplified_image` : Image avec formes géométriques simplifiées.

---

##  Dépendances

   - MATLAB R2020a ou supérieur.
   - Boîte à outils *Image Processing Toolbox* (pour SURF, SLIC).
   - Boîte à outils *Statistics and Machine Learning Toolbox* (pour Random Forest).

---

## 📂 Structure du Projet
```
matlab-mnt-toolbox/
├── debruitage/
│   ├── debruitage_random_forest.m
│   └── fonction_min_local.m
├── segmentation/
│   ├── modelisation_polynomiale_superpixels.m
│   └── approx_ellipsoide_dep.m
├── pretraitement/
│   ├── readFile2.m
│   └── division2.m
└── fusion/
    ├── SURFMatrice.m
    └── fusionSURFPourSH.m
```

---



## 📄 Exemples d'utilisation


### Exemple 1 : Segmenter un MNT et approximer les dépressions
```matlab
MNT = readFile2('NomMNT.sh');
[metrics, poly_eq] = modelisation_polynomiale_superpixels(MNT, 200, 10, true);
```

### Exemple 2 : Débruiter un MNT avec Random Forest
```matlab
mnt_clean = debruitage_random_forest(mnt);
```

### Exemple 3 : Diviser un MNT en quadrants
```matlab
quadrants = division2(MNT, true);
```

### Exemple 4 : Fusionner deux images MNT
```matlab
fused_image = SURFMatrice(image1, image2);
```

---


## 📝 Changelog

### Version 1.0.0
- Ajout des fonctions de segmentation et débruitage.
- Support initial pour la lecture des fichiers binaires.



---



## 📚 Références

- [Documentation MATLAB](https://www.mathworks.com/help/index.html)
- [Image Processing Toolbox](https://www.mathworks.com/products/image.html)
- [Statistics and Machine Learning Toolbox](https://www.mathworks.com/products/statistics.html)

# Bibliographie

## Articles scientifiques
- **Dusséaux & Vannier (2022)**
  *Soil surface roughness modelling with the bidirectional autocorrelation function*
  **Biosystems Engineering**, 220, 87–102.
  [DOI:10.1016/j.biosystemseng.2022.05.012](https://doi.org/10.1016/j.biosystemseng.2022.05.012)

- **Li & Chen (2014)**
  *Superpixel segmentation using linear spectral clustering*
  **IEEE Transactions on Image Processing**, 23(7), 3041–3051.

- **Hernandez et al. (2013)**
  *Image inpainting using sparse representations and iterative methods*
  **Journal of Mathematical Imaging and Vision**, 47(1-2), 151–165.

- **Bayliss (2012)**
  *Survey of SIFT and SURF image feature detection and description techniques*
  **International Journal of Computer Vision and Image Processing**, 2(2), 1–22.

## Conférence
- **Bay et al. (2006)**
  *SURF: Speeded Up Robust Features*
  **European Conference on Computer Vision (ECCV)**, 404–417.

## Stage
- **Zeggai (2024)**
  *Étude de la variabilité spatiale d’une surface agricole à petite échelle, avec la superposition de composantes*
  **Rapport de stage de Master**, Université Paris-Saclay (LATMOS).

---
