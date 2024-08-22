# Les interfaces et le tri avec les listes dynamiques.

## Les interfaces
En Java, une interface est un fichier particulier qui définit un contrat que les classes qui l'implémentent doivent respecter. Une interface définit un ensemble de méthodes, mais elle ne fournit pas l'implémentation de celle-ci. Cela permet de créer des classes qui respectent la même nomenclature de méthodes et qui peuvent être interchangeables facilement.

On peut voir une interface comme un "savoir-faire", et les classes qui implémentent cette interface s'engagent à réaliser ce "savoir-faire".

### Caractéristiques principales des interfaces en Java :

**Déclaration des méthodes** : Une interface ne contient que les signatures des méthodes (nom de la méthode, paramètres, et type de retour) sans implémentation.</br>
**Pas d'attributs d'instance** : Contrairement aux classes, les méthodes listées dans les interfaces ne doivent pas contenir d'attributs d'instance (public, private, ...). Elles peuvent cependant contenir des déclarations de constantes (avec les attribus `public`, `final` et `static`).</br>
**Implémentation multiple** : une classe peut implémenter plusieurs interfaces (plusieurs savoir-faires) mais ne peut hériter que d'une seule (is-a).

### Exemple d'interface :

```java
public interface IVolant {
    void voler();
    int getNombreDAiles();
}
```

Une classe qui doit implémenter cette interface doit le faire grâce au mot-clé **`implements`**. Voici un exemple d'implémentation de l'interface précédemment définie :

```java
public class Oiseau implements IVolant {
    @Override
    public void voler() {
        System.out.println("L'oiseau bat des ailes et s'envole dans le ciel.");
    }

    @Override
    public int getNombreDAiles() {
        return 2;
    }
}

public class Libellule implements IVolant {
    @Override
    public void voler() {
        System.out.println("La libellule bat rapidement des ailes au-dessus de l'étang.");
    }

    @Override
    public int getNombreDAiles() {
        return 4;
    }
}
```

## Les interfaces pour le tri avec les listes dynamiques.

Pour pouvoir trier des choses, il faut nécessairement pouvoir les comparer entre-elles. On pourra ainsi déterminer laquelle vient avant, vient après, ... en comparant ces choses entre-elles.

Java souhaitant dès sa création mettre à disposition des outils pour trier et des collections triées, s'est trouvée dans la même situation. Or on ne compare pas de la même façon deux nombres, deux chaînes de caractères, deux vélos, deux girafes, ... sans parler que cela peut changer d'une fois à l'autre (on peut vouloir trier des voitures par km, et une autre fois par prix).

La solution élégante trouvée et utilisée dans de nombreux languages est de laisser ce travail de se comparer à d'autres comme nous à la classe elle-même, seule à savoir le faire (l'interface `Comparable` présentée ci-dessous).

Ainsi, pour votre classe TrucMachinChose, l'implementation facile de ce "savoir-faire" vous permettra d'ensuite demander à Java de vous trier et d'automatiquement bénéficier de centaines de classes qui sauront en tirer profit automatiquement (des collections de TrucMachinChose automatiquement triées, ...).

### L'interface `Comparable`

L'interface Comparable est une interface générique fournie par Java, qui se trouve dans le package `java.lang`. Elle permet de définir de quelle manière les objets doivent être ordrés en implémentant la méthode `compareTo`.

#### Signature de l'interface Comparable :

```mermaid
classDiagram  
class Comparable["Comparable&lt;T&gt;"] {
    <<interface>>
    compareTo(T objetAComparer) int
}
```
```java
public interface Comparable<T> {
    int compareTo(T objetAComparer);
}
```
> [!IMPORTANT]  
> Dans cet example le `T` peut prendre la forme de n'importe quel type d'objet.

#### Fonctionnement de la méthode `compareTo` :

- Elle compare l'objet actuel (this) à l'objet spécifié en paramètre (objetAComparer).
- Elle retourne un entier :
  - négatif : si l'objet actuel (this) est "moins que" l'objet comparé (objetAComparer)
  - zéro : si les deux objets sont égaux
  - positif : si l'objet actuel (this) est "plus que" l'objet comparé (objetAComparer)

#### Exemple d'implémentation avec une classe `Personne` :

Supposons que vous ayez une classe Personne avec un attribut nom et un prénom, et que vous souhaitiez trier les personnes par leur nom par ordre alphabétique.


```mermaid
classDiagram
direction LR
class Comparable["Comparable&lt;T&gt;"] {
    <<interface>>
    compareTo(T objetAComparer) int
}
class Personne {
    -String nom
    -String prenom
    +Personne(String nom, String prenom)
    +getNom() String
    +getPrenom() String
    +toString() String
    compareTo(Personne autrePersonne) int
}
Personne ..|> Comparable : implements
```
```java
public class Personne implements Comparable<Personne> {
    private String nom;
    private String prenom;

    public Personne(String nom, String prenom) {
        this.nom = nom;
        this.prenom = prenom;
    }

    public String getNom() {
        return nom;
    }

    public String getPrenom() {
        return prenom;
    }

    @Override
    public int compareTo(Personne autrePersonne) {
        return this.nom.compareTo(autrePersonne.getNom());
    }

    @Override
    public String toString() {
        return nom + " " + prenom;
    }
}
```

> [!IMPORTANT]  
> Toutes les classes de Java comme `String`, les wrappers `Integer`, `Double`, ... implémentent déjà l'interface `Comparable`.
> C'est la raison pour laquelle on peut facilement leur déléguer cette tâche de comparaison comme ci-dessus.
> En gros, si vous voulez trier des 'choses' demandez-leur de se comparer l'une à l'autre !

#### Utilisation avec une ArrayList :

Une fois l'interface `Comparable` implémentée, vous pouvez facilement trier une ArrayList de personnes, grâce à la méthode `sort()` se trouvant dans la classe `Collections`:

```java
import java.util.ArrayList;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        ArrayList<Personne> personnes = new ArrayList<Personne>();
        personnes.add(new Personne("Poppins", "Marie"));
        personnes.add(new Personne("Voyante", "Claire"));
        personnes.add(new Personne("Dente", "Al"));

        Collections.sort(personnes);

        for (Personne p : personnes) {
            System.out.println(p);
        }
    }
}
```

#### Résultat sur la console :

```text
Dente Al
Poppins Marie
Voyante Claire
```

## ArrayList vs HashSet vs TreeSet

Java met à disposition de très nombreuses structures de données ayant des comportements différents et utiles dans différentes situations (mais nous allons revenir là-dessus plus en détail dans une prochaine activité).

Par exemple :
- `ArrayList` qui est une liste non ordonnée, respectant l'ordre d'insertion, permettant des doublons, pouvant être triée avec `Collections.sort`
- `HashSet` qui est un ensemble non ordonné, ne permettant pas les doublons, offrant des performances rapides pour les opérations de base
- `TreeSet` qui est un ensemble trié automatiquement selon les éléments contenus (leur implémentation de `Comparable`), ne permettant pas les doublons

Le choix entre l'une ou l'autre dépendra de la nécessité de gérer des doublons, de maintenir un ordre, des exigences de performance, ...

Voici un schéma vous aidant a trouver la bonne structure de donnée à utiliser pour gérer une liste :

```mermaid
flowchart TD
    A[Liste] --> B{Doit être triée?}
    B --> |Oui| C{Peut avoir des doublons?}
    B --> |Non| D{Peut avoir des doublons?}  

    C -->|Oui| E["ArrayList<> + Collections.sort()"]
    C -->|Non| F["TreeSet<> (Attention, le null est interdit)"]

    D -->|Oui| G[ArrayList<> ou Vector<>]
    D -->|Non| H[HashSet<> ou LinkedHashSet<>]
```

# Exercices

## Partie 1 : Utilisation de structure de tri

[Exercice1](/Exercice1.md)

## Partie 2 : L'interface Comparable

[Exercice2](/Exercice2.md)

## Partie 3 : Le Comparator

Pour les plus observateurs, vous avez pu remarquer qu'il y a 2 méthodes `sort()` dans la classe `Collections`.

La premières implémentation que vous avez normalement du utiliser dans la partie 2
```java
Collections.sort(List<T> list);
```
> [!IMPORTANT]  
> Dans cet exemple le `T` peut prendre la forme de n'importe quel type d'objet.

Et la deuxième implémentation, une surcharge qui ajoute un `Comparator`:
```java
Collections.sort(List<T> list, Comparator<T> c);
```
Le `Comparator` permet de définir des critères de tri différents par rapport au comportement par défaut de la classe (= son implémentation de `Comparable`). Et ce sans avoir modifier le code de la classe elle-même, car celui-ci sera fourni directement "à la volée". La méthode `Collections.sort(...)` utilise une implémentation de `Comparator` directement passée en paramètre afin de trier la liste selon ces nouvelles règles-là. 

Ce `Comparator` doit implémenter la méthode `compare(T o1, T o2)` qui retourne un entier : 
- un nombre négatif si le premier objet doit précéder le second
- zéro s'ils sont égaux
- un nombre positif si le premier objet doit suivre le second.

L'utilisation d'un `Comparator` est particulièrement utile lorsqu'on souhaite trier des objets selon différents critères que ceux implémentés dans la classe ou lorsque la classe des objets à trier ne peut pas être modifiée (on ne peut pas changer son implémentation de `Comparable`).

### Exemple

Si l'on reprend la classe `Personne` vue plus haut, nous voyons dans la méthode `compareTo` que les objets `Personne` seront trié par leur nom. Exceptionnellement dans notre méthode main nous voulons les ordrer par prénom. Nous allons donc changer le comportement par défaut avec notre tri:

```java
import java.util.ArrayList;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        ArrayList<Personne> personnes = new ArrayList<Personne>();
        
        personnes.add(new Personne("Poppins", "Marie"));
        personnes.add(new Personne("Voyante", "Claire"));
        personnes.add(new Personne("Dente", "Al"));

        Collections.sort(personnes, new Comparator<Personne>() {

            @Override
            public int compare(Personne personne1, Personne personne2) {
                return personne1.getPrenom().compareTo(personne2.getPrenom());
            }
        });

        for (Personne p : personnes) {
            System.out.println(p);
        }
    }
}
```

#### Résultat attendu sur la console

```text
Dente Al
Voyante Claire
Poppins Marie
```

### Exercice

[Exercice3](/Exercice3.md)