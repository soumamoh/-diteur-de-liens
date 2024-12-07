# Réalisation d'un éditeur de liens | Phase de réimplantation

## **Objectif du projet**
L'objectif principal de ce projet est d'implémenter une sous-partie d'un éditeur de liens. Plus précisément, il se concentre sur la **dernière phase**, appelée **phase de réimplantation**, qui est exécutée par l'éditeur de liens.

Le projet est structuré en plusieurs étapes, incluant la création de divers outils intermédiaires. Cela permet :
- De mieux comprendre les principales notions associées à la réimplantation.
- De simplifier et découper les différentes tâches pour une progression méthodique.

---

## **Descriptif de la structure du code développé**

### **Fichiers et leurs fonctions**

#### `getELF.c`
- Ensemble de fonctions permettant de lire les différentes parties d’un fichier objet ELF.
- Renvoie une structure de données propre à chaque partie du fichier ELF.
- **Fonction principale :** `lireFichierELF()` :
  - Utilise les autres fonctions de `getELF.c` pour lire et stocker en mémoire un fichier ELF entier.

---

#### `getELFHeader.c`
- Programme qui prend en argument un fichier objet.
- **Fonction principale :** `afficherELFHeader()` :
  - Utilise une fonction de `getELF.c` pour lire le header ELF du fichier.
  - Affiche le header au format de `readelf -h`.

---

#### `getSectionHeaderTable.c`
- Programme qui prend en argument un fichier objet.
- **Fonction principale :** `afficherSectionHeaderTable()` :
  - Se déplace aux bons endroits dans le fichier avant d’appeler les fonctions de `getELF.c` pour lire la section header table.
  - Affiche la table au format de `readelf -S`.

---

#### `getSection.c`
- Programme qui prend en argument un numéro ou un nom de section et un fichier objet.
- **Fonctions principales :**
  - `afficherSectionNum()` :
    - Se déplace aux bons endroits dans le fichier pour lire la section donnée.
    - Affiche la section au format de `readelf -x`.
  - `trouverNumSection()` :
    - Renvoie le numéro d’une section à partir de son nom.

---

#### `getSymbolTable.c`
- Programme qui prend en argument un fichier objet.
- **Fonction principale :** `afficherSymbolTable()` :
  - Se déplace aux bons endroits dans le fichier pour lire la table des symboles.
  - Affiche la table au format de `readelf -s`.

---

#### `getRelocationTable.c`
- Programme qui prend en argument un fichier objet.
- **Fonction principale :** `afficherRelocationTable()` :
  - Se déplace aux bons endroits dans le fichier pour lire les tables de réimplantations.
  - Affiche les tables au format de `readelf -r`.

---

#### `fusionELF.c`
- Programme qui prend en argument deux fichiers objets.
- **Fonctions principales :**
  - `FusionSectionsCode()` :
    - Fusionne les sections de code des deux fichiers donnés en argument.
    - Remplit la structure du fichier résultat.
  - `Fusionrenumerotationsymboles()` :
    - Fusionne la table des symboles des deux fichiers donnés en argument.
    - Remplit la structure du fichier résultat.
  - `afficherELF()` :
    - Prend la structure du fichier résultat en argument et affiche son contenu.

---

## **Liste des fonctionnalités**

### **Fonctionnalités implémentées :**
- Lecture et stockage d’un fichier ELF en mémoire.
- Affichage d’un fichier ELF au format de `readelf` pour toutes les étapes de la phase 1.
- Fusion des sections de code et de la table des symboles de deux fichiers objets.
- Affichage du fichier ELF fusionné dans la console (sections de code + table des symboles).

### **Fonctionnalités manquantes :**
- Correction des numéros des sections et des valeurs des symboles.
- Fusion et correction des tables de réimplantations.
- Production d’un fichier résultat au format ELF.

---

## **Liste des éventuels bogues connus**
- Aucun bogue révélé lors des tests.

---

## **Liste et description des tests effectués**

### **Script de test : `test.sh`**
- Parcourt tous les fichiers du répertoire de tests donné en argument.
- Pour chaque fichier de test, tous les programmes de la phase 1 sont exécutés et l’affichage est comparé à celui de `readelf`.
- Pour les tests du programme `getSection` :
  - Une variable est incrémentée pour exécuter le test avec tous les numéros de section.
  - Les tests s’arrêtent lorsqu’une erreur indique que toutes les sections ont été testées.

### **Création des fichiers tests :**
- Les fichiers tests sont générés à partir de 9 programmes C de 5 à 250 lignes.

### **Procédure de tests :**
1. Se déplacer dans le dossier `tests` :
   ```bash
   ./compile.sh
```
