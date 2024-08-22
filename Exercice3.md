## Exercice 3 : Le Comparator

[Revenir à la consigne principale](/README.md)

## Objectif: (Durée 60')

- Implémenter un comparator
- Documenter son fonctionnement et la différence avec la méthode CompareTo.

### Travail à réaliser

- Ouvrez le fichier Exercice3.java
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
- Implémentez un tri pour vos fruits pour que exceptionnellement ils soit trié uniquement par ordre alphabétique.

#### Résultat attendu sur la console

```text
Banane (0)
Banane (0)
Banane (0)
Fraise (200)
Manchineel (333)*
Orange (10)
Orange (10)
Pomme (4)
Pomme (4)
Pomme (4)
Raisin (4)
Solanum (50)*
```
