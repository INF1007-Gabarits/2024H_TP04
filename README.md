# TP04: Programmation orientée objet

- [TP04: Programmation orientée objet](#tp04-programmation-orientée-objet)
  - [Introduction](#introduction)
  - [Objectifs](#objectifs)
  - [Vue d'ensemble](#vue-densemble)
  - [1.1 Création de la classe abstraite `Pokemon`](#11-création-de-la-classe-abstraite-pokemon)
    - [1.1.1 Abstraction](#111-abstraction)
    - [1.1.2 Constructeur](#112-constructeur)
    - [1.1.3 Les propriétés en lecture (getters)](#113-les-propriétés-en-lecture-getters)
    - [1.1.4 Les propriétés en écriture (setters)](#114-les-propriétés-en-écriture-setters)
    - [1.1.5 Méthodes abstraites](#115-méthodes-abstraites)
    - [1.1.6 Méthodes concrètes](#116-méthodes-concrètes)
    - [1.1.7 Méthodes magiques](#117-méthodes-magiques)
  - [1.2 Création des classes abstraites `PokemonType`](#12-création-des-classes-abstraites-pokemontype)
    - [1.2.1 Héritage et Abstraction](#121-héritage-et-abstraction)
    - [1.2.2 Constructeur](#122-constructeur)
    - [1.2.3 Implémentation de `get_attack_multiplier`](#123-implémentation-de-get_attack_multiplier)
  - [1.3 Le Triptyque: `Squirtle`, `Charmander` et `Bulbasaur`](#13-le-triptyque-squirtle-charmander-et-bulbasaur)
    - [1.3.1 Héritage](#131-héritage)
    - [1.3.2 Constructeur](#132-constructeur)
    - [1.3.3 Implémentation de `evolve`](#133-implémentation-de-evolve)
    - [1.3.4 Implémentation de `get_signature_sound` 🎶](#134-implémentation-de-get_signature_sound-)
    - [1.4 Complétion de la classe `PokemonArena`](#14-complétion-de-la-classe-pokemonarena)
    - [1.5 Création du script principal](#15-création-du-script-principal)
  - [Remise](#remise)
  - [Barème](#barème)
  - [Annexe: Guide et normes de codage](#annexe-guide-et-normes-de-codage)
  - [Bon succès à tou(te)s! 🚀](#bon-succès-à-toutes-)

:alarm_clock: Date de remise le Dimanche 14 avril 23h59

## Introduction

<p align="justify"> Bienvenue dans ce second projet sur le monde fascinant des Pokémon ! Ce travail pratique vous plonge dans une simulation de combat tour par tour entre Pokémon, en utilisant les concepts de la programmation orientée objet. Êtes-vous prêts à faire partie des meilleurs dresseurs ? </p>

![Pythonmon](/assets/cover.png)

<p align="left"> <i>Crédits: <a href="https://openai.com/blog/dall-e/">DALLE 3</a></i></p>

## Objectifs

- Comprendre et appliquer les concepts de la programmation orientée objet, avec un accent particulier sur l'encapsulation, l'héritage, et le polymorphisme.

## Vue d'ensemble

Tout d'abord, vous développerez une classe abstraite `Pokemon` pour les caractéristiques communes à tous les Pokémon. Ensuite, vous développerez des sous-classes abstraites `PokemonType` pour trois différents types de Pokémon. Ces classes seront des enfants de la classe `Pokemon` et définiront des caractéristiques communes des Pokémon de ce type. Puis, vous développerez une sous-classe concrète représentant un Pokémon spécifique pour chaque type.

Par la suite, vous compléterez une fonction de la classe `PokemonArena` utilisant le polymorphisme pour simuler un combat entre deux Pokémon.

Finalement, vous écrirez un simple script principal pour tester le fonctionnement de votre code précédemment écrit.

![UML](/assets/UML.png)

## 1.1 Création de la classe abstraite `Pokemon`

Cette classe est la pierre angulaire de notre simulation. Elle représente les caractéristiques communes à tous les Pokémon. Vous devez compléter la classe `Pokemon` en suivant les directives suivantes:

### 1.1.1 Abstraction

Pour commencer, vous devez rendre la classe `Pokemon` abstraite afin qu'elle ne puisse pas être instanciée directement.

### 1.1.2 Constructeur

La méthode `__init__` est le constructeur de la classe. Elle est appelée lorsqu'une instance de la classe est créée. Vous devez compléter le constructeur de la classe `Pokemon`.

- Le constructeur doit prendre les paramètres suivants:
  - `name`: le nom du Pokémon;
  - `attack`: l'attaque du Pokémon;
  - `defense`: la défense du Pokémon;
  - `type`: le type du Pokémon.

Lors de cette initialisation, vous devez garder en mémoire les paramètres dans des attributs privés utilisant la convention du double underscore (ex: `name` devient `__name`). Vous devez également initialiser les attributs suivants:

- `__health`: la santé du Pokémon. Elle doit être initialisée à la valeur maximale de santé (voir la constante `MAX_HEALTH` dans le fichier `constants.py`);
- `__state`: l'état du Pokémon. Elle doit être initialisée à `NORMAL`;
- `__state_counter`: le compteur d'état du Pokémon. Il sera utilisé pour compter le nombre de tours restants d'un état induit (ex: empoisonné). Il doit être initialisé à 0;
- `__evolved`: un booléen indiquant si le Pokémon a évolué. Il doit être initialisé à `False`.

### 1.1.3 Les propriétés en lecture (getters)

Les propriétés en lecture permettent d'accéder aux attributs privés d'un objet. Les getters sont souvent utilisés pour obtenir les valeurs des attributs sans les exposer directement. Vous devez utiliser le décorateur [@property](https://docs.python.org/3/library/functions.html#property) pour la définition de chaque getter.

Voici la liste des getters à implémenter:

- `name`: retourne le nom du Pokémon (string);
- `attack`: retourne l'attaque du Pokémon (int);
- `defense`: retourne la défense du Pokémon (int);
- `type`: retourne le type du Pokémon (PokemonType);
- `health`: retourne la santé du Pokémon (int);
- `state`: retourne l'état du Pokémon (PokemonState);
- `state_counter`: retourne le compteur d'état du Pokémon (int);
- `evolved`: retourne un booléen indiquant si le Pokémon a évolué (bool).

### 1.1.4 Les propriétés en écriture (setters)

Les propriétés en écriture permettent de modifier les attributs privés d'un objet et de valider les valeurs données avant leur modification. Vous devez utiliser le décorateur [@attributename.setter](https://docs.python.org/3/library/functions.html#property) pour la définition de chaque setter. Vous devez également valider les valeurs données avant de les assigner aux attributs privés de l'objet.

Voici la liste des setters à implémenter:

- `name`: prend un nom en paramètre et assigne le nom à l'attribut `__name` seulement si le nom n'est pas une chaîne vide.
- `attack`: prend une attaque en paramètre et assigne l'attaque à l'attribut `__attack`. Si la valeur fournie est inférieure à 0, assignez 0. Cela assure que cet attribut ne prend jamais de valeurs négatives.
- `defense`: prend une défense en paramètre et assigne la défense à l'attribut `__defense`. Si la valeur fournie est inférieure à 0, assignez 0.
- `state`: prend un état en paramètre et assigne l'état à l'attribut `__state` seulement si l'état est un membre de l'énumération `PokemonState`.
- `state_counter`: prend un compteur d'état en paramètre et assigne le compteur d'état à l'attribut `__state_counter`. Si la valeur fournie est inférieure à 0, assignez 0.

### 1.1.5 Méthodes abstraites

Les méthodes abstraites sont des méthodes qui ne sont pas implémentées dans la classe abstraite, mais qui doivent l'être obligatoirement dans les sous-classes. Vous devez utiliser le décorateur [@abstractmethod](https://docs.python.org/3/library/abc.html#abc.abstractmethod) pour la déclaration de chaque signature des méthodes abstraites.

Voici la liste des méthodes abstraites à implémenter:

- a) `get_attack_multiplier`: prend un type de Pokémon en paramètre et retourne le multiplicateur d'attaque (double) du Pokémon en fonction du type du Pokémon attaqué (passé en paramètre). Cette méthode sera implémentée dans les sous-classes de `Pokemon`;
- b) `generate_random_induced_state`: retourne un tuple contenant un état induit aléatoirement (PokemonState) et le nombre de tours restants de l'état induit (int). Cette méthode sert à générer un état induit aléatoire lorsqu'un Pokémon attaque un autre Pokémon et sera implémentée dans les sous-classes de `Pokemon`;
- c) `get_signature_sound`: retourne le son de signature du Pokémon (string). Cette méthode sera implémentée dans les sous-classes de `PokemonType`;
- d) `evolve`: cette méthode ne reçoit aucun paramètre et ne retourne rien. Elle permet d'évoluer le Pokémon. Cette méthode sera implémentée dans les sous-classes de `PokemonType`.

### 1.1.6 Méthodes concrètes

Les méthodes concrètes sont des méthodes qui sont implémentées dans la classe abstraite et qui peuvent être utilisées directement par les sous-classes. Vous devez implémenter les méthodes suivantes:

- a) **`decrement_state_counter`**: Cette fonction ne reçoit aucun paramètre et ne retourne rien. Elle décrémente le compteur d'état du Pokémon de 1. Si le compteur d'état est déjà à 0, la fonction ne fait rien. Pour rappel, le compteur d'état est utilisé pour compter le nombre de tours restants d'un état induit (ex: empoisonné).

  **Exemple d'utilisation:**

  ```python
  print(pokemon.state_counter) # Retourne: 3
  pokemon.decrement_state_counter()
  print(pokemon.state_counter) # Retourne: 2
  ```

- b) **`is_knocked_out`**: Cette fonction ne reçoit aucun paramètre et retourne un booléen indiquant si le Pokémon est KO (True) ou non (False). Un Pokémon est KO si sa santé est à 0.

  **Exemple d'utilisation:**

  ```python
  print(pokemon.health) # Retourne: 10
  print(pokemon.is_knocked_out()) # Retourne: False
  pokemon.health = 0
  print(pokemon.is_knocked_out()) # Retourne: True
  ```

- c) **`heal`**: Cette fonction ne reçoit aucun paramètre et ne retourne rien. Elle remet la santé du Pokémon à la valeur maximale de santé (voir la constante `MAX_HEALTH` dans le fichier `constants.py`).

  **Exemple d'utilisation:**

  ```python
  print(pokemon.health) # 5
  pokemon.heal()
  print(pokemon.health) # 1000
  ```

### 1.1.7 Méthodes magiques

Les méthodes magiques sont des méthodes spéciales ayant des noms spécifiques (ex: `__init__`, `__str__`, `__repr__`, etc.) qui permettent de modifier le comportement de l'objet.

Nous allons les utiliser pour surcharger des opérateurs spécifiques ("+" et "-") ou lorsqu'on tente d'interpréter l'objet comme une chaîne de caractères (via `str(...)`, `print(...)`, etc.).

**a) def \_\_str\_\_(self):**
Cette méthode spéciale est appelée lorsqu'on tente d'interpréter l'objet comme une chaîne de caractères (ex: `str(pokemon)` ou `print(pokemon)`). Elle retourne une chaîne de caractères représentant le Pokémon.

La chaîne de caractères doit être de la forme suivante:
`<name> est de type <type>. Il a <attack> points d'attaque et <defense> points de défense.`.

**Exemple d'utilisation:**

```python
bulbasaur = Bulbasaur(...)
print(bulbasaur) # Retourne: Bulbasaur est de type GRASS. Il a 48 points d'attaque et 65 points de défense.
```

**b) def \_\_add\_\_(self, health: int):**
Cette méthode spéciale est appelée lorsqu'on tente d'ajouter un nombre à un Pokémon (ex: `pokemon + 10`). Elle ne retourne rien. Elle doit ajouter la valeur passée en paramètre à la santé du Pokémon. Si la valeur passée en paramètre est négative, la fonction ne fait rien. La santé du Pokémon ne peut pas dépasser la valeur maximale de santé (voir la constante `MAX_HEALTH` dans le fichier `constants.py`).

**Exemple d'utilisation:**

```python
print(pokemon.health) # Retourne: 5
pokemon + 10
print(pokemon.health) # Retourne: 15
```

**c) def \_\_sub\_\_(self, damage: int):**
Cette méthode spéciale est appelée lorsqu'on tente de soustraire un nombre à un Pokémon (ex: `pokemon - 10`). Elle ne retourne rien. Elle doit soustraire la valeur passée en paramètre à la santé du Pokémon. Si la valeur passée en paramètre est négative, la fonction ne fait rien. La santé du Pokémon ne peut pas être négative.

**Exemple d'utilisation:**

```python
print(pokemon.health) # Retourne: 25
pokemon - 10
print(pokemon.health) # Retourne: 15
```

## 1.2 Création des classes abstraites `PokemonType`

Les classes abstraites `PokemonTypeWater`, `PokemonTypeFire` et `PokemonTypeGrass` représentent les caractéristiques communes à tous les Pokémon de leur type.

### 1.2.1 Héritage et Abstraction

Pour commencer, vous devez faire hériter les trois classes de la classe abstraite `Pokemon`. Vous devez également rendre les trois classes abstraites afin qu'elles ne puissent pas être instanciées directement.

### 1.2.2 Constructeur

Le constructeur des trois classes doit prendre les paramètres suivants:

- `name`: le nom du Pokémon
- `attack`: l'attaque du Pokémon
- `defense`: la défense du Pokémon

Vous devez absolument utiliser le constructeur de la classe parent pour garder en mémoire les différents paramètres. Chaque sous-classe devra donc donner le type qui lui correspond dans cet appel. Le code des constructeurs ne doit pas dépasser une ligne de code.

### 1.2.3 Implémentation de `get_attack_multiplier`

Dans l'univers de Pokémon, la notion de type est très importante pour prédire l'issue d'un combat. Chaque type de Pokémon a des forces et des faiblesses contre d'autres types de Pokémon. Par exemple, un Pokémon de type **FEU** aura un avantage contre un Pokémon de type **PLANTE**. On peut donc dire que, contrairement au langage Python, le monde des Pokémon est fortement typé (sans mauvais jeu de mot 😉).

Vous devez implémenter la méthode abstraite `get_attack_multiplier` dans les trois classes. Cette méthode retourne le multiplicateur d'attaque (double) du Pokémon en fonction du type du Pokémon attaqué (passé en paramètre).

Voici les multiplicateurs d'attaque pour chaque type de Pokémon:

- **Pour les pokémons de type FIRE**:

  - GRASS: 1.25
  - WATER: 0.75
  - Autre: 1.0

- **Pour les pokémons de type WATER**:

  - FIRE: 1.25
  - GRASS: 0.75
  - Autre: 1.0

- **Pour les pokémons de type GRASS**:
  - WATER: 1.25
  - FIRE: 0.75
  - Autre: 1.0

**Exemple d'utilisation:**

```python
squirtle = Squirtle(...)
charmander = Charmander(...)
print(squirtle.get_attack_multiplier(charmander.type)) # Retourne: 1.25
print(charmander.get_attack_multiplier(squirtle.type)) # Retourne: 0.75
```

## 1.3 Le Triptyque: `Squirtle`, `Charmander` et `Bulbasaur`

Les classes `Squirtle`, `Charmander` et `Bulbasaur` représentent les trois Pokémon de départ les plus emblématiques de cet univers. Chacun de ces Pokémon incarne un élément fondamental - Eau, Feu et Plante - et possède la capacité fascinante d'évoluer, de gagner en puissance, et d'exprimer leur individualité à travers un son unique.

### 1.3.1 Héritage

Les trois classes doivent hériter de la classe abstraite correspondant à leur type de Pokémon (`PokemonWaterType`, `PokemonFireType` et `PokemonGrassType`). Cet héritage permet une implémentation cohérente et propre des comportements spécifiques à chaque type.

### 1.3.2 Constructeur

Le constructeur des trois classes ne prend aucun paramètre. Vous devez utiliser le constructeur de la classe parent en lui donnant les caractéristiques spécifiques du Pokémon en question. Chaque constructeur ne doit donc pas dépasser une ligne de code.

Voici les caractéristiques de base de chaque Pokémon:

- **Squirtle**:

  - Nom: Squirtle
  - Attaque: 48
  - Défense: 65

- **Charmander**:

  - Nom: Charmander
  - Attaque: 52
  - Défense: 43

- **Bulbasaur**:
  - Nom: Bulbasaur
  - Attaque: 49
  - Défense: 49

### 1.3.3 Implémentation de `evolve`

Ce qui rend ces Pokémon particulièrement captivants, c'est leur capacité à évoluer et à monter en puissance. La méthode `evolve` assure cette transformation en modifiant les attributs d'attaque et de défense ainsi que le nom du Pokémon, reflétant ainsi son nouvel état évolutif. Elle ne prend aucun paramètre et ne retourne rien.

Voici les caractéristiques de chaque Pokémon après son évolution:

- **Squirtle**:

  - Nom: Wartortle
  - Attaque: 63
  - Défense: 80

- **Charmander**:

  - Nom: Charmeleon
  - Attaque: 64
  - Défense: 58

- **Bulbasaur**:
  - Nom: Ivysaur
  - Attaque: 62
  - Défense: 63

**Exemple d'utilisation:**

```python
bulbasaur = Bulbasaur(...)
print(bulbasaur.name) # Retourne: Bulbasaur
print(bulbasaur.attack) # Retourne: 49
print(bulbasaur.defense) # Retourne: 49
bulbasaur.evolve()
print(bulbasaur.name) # Retourne: Ivysaur
print(bulbasaur.attack) # Retourne: 62
print(bulbasaur.defense) # Retourne: 63
```

### 1.3.4 Implémentation de `get_signature_sound` 🎶

Chaque Pokémon exprime sa singularité à travers un son distinct. La méthode `get_signature_sound` nous gratifie de ces sonorités emblématiques. Elle ne prend aucun paramètre et retourne le son de signature du Pokémon (string).

Voici les sons de signature de chaque Pokémon:

- **Squirtle**: "Squirtle-squirtle"
- **Charmander**: "Char-char"
- **Bulbasaur**: "Bulba-bulba"

**Exemple d'utilisation:**

```python
charmander = Charmander(...)
print(charmander.get_signature_sound()) # Retourne: Char-char
```

### 1.4 Complétion de la classe `PokemonArena`

La construction de l'arène de combat est presque achevée. La dernière brique à poser est l'implémentation de la méthode `attack` de la classe `PokemonArena`. Cette méthode prend deux paramètres: un Pokémon attaquant et un Pokémon défenseur. Elle calcule les dégâts infligés par l'attaquant au défenseur en fonction du multiplicateur de dégâts de l'attaquant et soustrait les dégâts aux points de vie du défenseur. La méthode doit retourner les dégâts infligés.

**Exemple d'utilisation:**

```python
squirtle = Squirtle(...)
charmander = Charmander(...)
print(charmander.health) # Retourne: 1000
PokemonArena.attack(squirtle, charmander) # Retourne: 60 (car 48 * 1.25 = 60)
print(charmander.health) # Retourne: 940
```

**Important**: Il est nécessaire d'utiliser la méthode `get_attack_multiplier` de la classe `Pokemon` pour calculer le multiplicateur de dégâts de l'attaquant et d'utiliser la surcharge de l'opérateur "-" pour soustraire les dégâts aux points de vie du défenseur.

### 1.5 Création du script principal

Vous êtes maintenant prêt à entrer dans l'arène et à vivre l'expérience ultime de la vie de dresseur/dresseuse de Pokémon! Dans ce script principal, nous allons tester tous les aspects de la dynamique entre les Pokémon, de leur tout premier combat jusqu'à leur forme évoluée.

Il est donc temps de vous diriger vers le fichier [main.py](part2/main.py) et suivre les instructions TODO pour compléter votre aventure. Le combat final vous attend! ⭐️

## Remise

Pour soumettre votre travail, assurez-vous d'abord que tous les tests de votre code passent avec succès. Ensuite, faites un dernier commit de vos changements si nécessaire et faites un `push` sur votre dépôt **GitHub** Classroom.

Il est important de vérifier sur GitHub que vos dernières modifications ont bien été mises en ligne. Aucune étape supplémentaire comme la création d'un fichier zip n'est nécessaire ; votre travail sera évalué directement à partir de votre dépôt GitHub Classroom. Veillez simplement à ce que tout soit à jour avant la date limite de remise.

## Barème

| Question  | Points  |
| --------- | ------- |
| 1.1.1     | 2       |
| 1.1.2     | 4       |
| 1.1.3     | 6       |
| 1.1.4     | 12      |
| 1.1.5     | 4       |
| 1.1.6     | 8       |
| 1.1.7     | 12      |
| 1.2.1     | 2       |
| 1.2.2     | 4       |
| 1.2.3     | 8       |
| 1.3.1     | 2       |
| 1.3.2     | 6       |
| 1.3.3     | 6       |
| 1.3.4     | 8       |
| 1.4       | 6       |
| 1.5       | 10      |
| **Total** | **100** |

## Annexe: Guide et normes de codage

- [Le guide maison](https://github.com/INF1007-Gabarits/Guide-codage-python) de normes supplémentaires à respecter
- [Le plugin Pycharm Pylint](https://plugins.jetbrains.com/plugin/11084-pylint) qui analyse votre code et indique certaines erreurs. Vous avertis aussi si vous ne respectez pas certaines de normes de PEP8.
- [Quelques indications en français sur PEP8](https://openclassrooms.com/fr/courses/4425111-perfectionnez-vous-en-python/4464230-assimilez-les-bonnes-pratiques-de-la-pep-8)
- [La documentation PEP8 Officielle](https://www.python.org/dev/peps/pep-0008/)

## Bon succès à tou(te)s! 🚀
