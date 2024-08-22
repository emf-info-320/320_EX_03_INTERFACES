# Exercice 2 : L'interface Comparable

[Revenir à la consigne principale](/README.md)

## Objectif: (Durée 90')

- Mettre en oeuvre l'interface `Comparable` sur une classe 
- Implémenter une méthode de comparaison
- Documenter

## Travail à réaliser
- Ouvrez le fichier Exercice2.java
- Ajoutez une classe représentant des `Fruit` dans un package `models`, qui sera définie par les attributs et méthodes suivants:
  - Un nom en String
  - Un nombre de graine en int
  - S'il est comestible en boolean
  - Les getters pour les différents attributs
  - La méthode compareTo:
    - Ordonne les fruits par nombre croissant de graînes et s'il y a une égalité, par ordre alphabétique.
  - La méthode toString:
    - Le nom du fruits, suivi du nombre de graines entre parenthèses, suivi d'une * s'il n'est pas comestible. (par ex. "Pomme (4)" ou "Solanum(50)*")
- Dans le constructeur, créez les objets fruits suivant cette liste : 
  - Pomme - Graines : 4, Comestible : Oui
  - Banane - Graines : 0, Comestible : Oui
  - Manchineel - Graines : 333, Comestible : Non
  - Orange - Graines : 10, Comestible : Oui
  - Pomme - Graines : 4, Comestible : Oui
  - Fraise - Graines : 200, Comestible : Oui
  - Banane - Graines : 0, Comestible : Oui
  - Solanum - Graines : 50, Comestible : Non
  - Raisin - Graines : 4, Comestible : Oui
  - Orange - Graines : 10, Comestible : Oui
  - Pomme - Graines : 4, Comestible : Oui
  - Banane - Graines : 0, Comestible : Oui
- Ajoutez les objets dans une liste pour qu'il soit trié comme implémenté dans la classe `Fruit` les doublons sont autorisés.

## Résultat attendu sur la console

```text
Banane (0)
Banane (0)
Banane (0)
Pomme (4)
Pomme (4)
Pomme (4)
Raisin (4)
Orange (10)
Orange (10)
Solanum (50)*
Fraise (200)
Manchineel (333)*
```

# Exercice 2' - Optionnel

Changez l'ordre de tri pour que les fruits non comestibles soient en premier dans la liste s'il y a égalité il faut que le fruit soit trié par nombre de graines et ensuite par ordre alphabétique.

## Résultat attendu sur la console

```text
Solanum (50)*
Manchineel (333)*
Banane (0)
Banane (0)
Banane (0)
Pomme (4)
Pomme (4)
Pomme (4)
Raisin (4)
Orange (10)
Orange (10)
Fraise (200)
```