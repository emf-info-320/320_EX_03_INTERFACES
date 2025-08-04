# Exercice 1 : Utilisation de structure de tri

[Revenir à la consigne principale](/README.md)

## Objectif: (Durée 60')

- Se familiariser avec les structures de données dynamiques et leur tri.

## Travail à réaliser

Ouvrez le fichier [Exercice1.java](/Interfaces/src/Exercice1.java). Vous verrez que son constructeur appelle déjà 3 méthodes et c'est elles qu'il vous faudra coder par vous-même :

1. **collection_avecDoublonsTrier()**  
   doit trier une collection simple (=pas triée et autorisée à contenir des doublons) dans laquelle vous mettrez les noms de fruits ci-dessous et dont vous afficherez le contenu après l'avoir trié.

2. **collection_dejaTrieeEtSansDoublons()**  
   pour utiliser une collection intelligente (=déjà automatiquement triée et garantie sans doublons) dans laquelle vous mettrez les noms de fruits ci-dessous et dont vous afficherez le contenu.
3. **tableau_trier()**  
   pour trier un tableau [] (à l'ancienne) dans lequel vous mettrez là-aussi les noms de fruits ci-dessous et dont vous afficherez le contenu après l'avoir trié. **Trouvez par vous-même comment trier un tableau à l'ancienne !**
  
Voici les fruits que vous devrez à chaque fois mettre dans vos 3 structures de données :

- Pomme
- Banane
- Orange
- Pomme
- Fraise
- Banane
- Raisin
- Orange
- Pomme
- Banane

> [!CAUTION]  
> Vous devez ajouter les éléments dans votre liste dans l'ordre donné ci-dessus !

## Résultat attendu sur la console

```text
-------------------------
1a : tri d'une collection
-------------------------
Banane
Banane
Banane
Fraise
Orange
Orange
Pomme
Pomme
Pomme
Raisin
-------------------------------------------
1b : collection déjà triée et sans doublons
-------------------------------------------
Banane
Fraise
Orange
Pomme
Raisin
------------------------
1c : tri d'un tableau []
------------------------
Banane
Banane
Banane
Fraise
Orange
Orange
Pomme
Pomme
Pomme
Raisin
```
