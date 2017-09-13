Modélisation UML
================

## L'histoire de l'UML

1è standardisation UML : novembre 1997 -> 20 ans ! Happy Birthday ! ✨🎆🎂
  - Booh
  - Rumbaugh
  - Jacobson

L'UML est une notation, *PAS une méthode*
L'UML est un langage de modélisation
  - objet dans sa construction
  - généraliste : il n'est pas limité au logiciel/informatique
L'UML est (presque) dans le domaine public
L'UML est riche, ouvert (extensible)
L'UML évolue

## 14 diagrammes

Diagrammes de structure
  - Classes : définit des concepts, les données métier importantes et les relations entre ces données -> structure des données
  - Objets : exemples correspondant au diagramme de classes -> pour expliquer au client
  - Paquetages : ensemble d'éléments de modélisation (permet d'organiser un modèle)
  - Composants : cartographie des composants qu'on a pu modéliser, et qu'on va écrire (c'est la fin du cycle de modélisation, presque le développement)
  - Déploiement : mise en place d'un logiciel sur des machines (qu'est-ce qui tourne où...)
  - Structures composites : diagramme de classes à très grosse mailles (pour des systèmes énormes), décrit des systèmes de systèmes
  - Profils : adaptation de l'UML (cf [www.omg.org](http://www.omg.org/spec/#Profile))
Diagrammes de comportement
  - Cas d'utilisation : décrit les services fournis par le système à ses acteurs **(très souvent le premier diagramme à faire)**
  - Activités : décrit des processus (plutôt processus informatiques, limite algorithmes)
  - États-transitions : modes de marche d'un système (en panne, pas en panne, commande saisie, validée, payée, archivée, facturée...)
  - Séquences : échanges de messages entre des éléments de mon système, et leur dimension temporelle
  - Communications : structure des échanges de messages, qui dialogue avec qui (de moins en moins utilisé)
  - Chronométrage : c'est comme les chronogrammes (diagramme temps-signaux)
  - Vue d'ensemble d'interactions : *euuuuh* on s'en servira pas

## En vrac...

3 aspects dans un système :
  - la structure du système
  - les fonctions qu'il remplit
  - la dynamique du système

**⚠ Attention aux associations et aux associations-classes**
Deux classes liées par une association créent un ensemble où chaque couple doit être unique ! Donc `Personne 0..* <-réserve-> 1..* Table` permet à une personne de ne réserver qu'une seule fois une table. Il faut créer une classe intermédiaire (qui est en plus ce qu'on essaie de gérer), ie. `Personne 1..1 <-effectue-> 0..* Réservation 0..* <-concerne-> 1..* Table`

## Outils

  - MagicDraw
  - IBM Rational Software Architect (c'est lourd)
  - Papyrus (open source)

**⚠ Attention à la couverture et au respect du standard UML**

## Rappels UML de base

Association : 2 classes au même niveau
Agrégation : `composant` fait partie de `composite` (représenté par un **losange blanc** du côté du composite)
Composition : agrégation avec dépendance des cycles de vie (si le composite est détruit, les composants sont détruits aussi), et la cardinalité max vers un composite est 1 (`Composite 0..1 ou 1..1 <-> Composite`, un composant n'appartient qu'à un composite max) (représenté par un **losange noir**) -> `ON DELETE CASCADE` dans une BDD

## Comment choisir un type de relation entre 2 classes

Loi de Liskov : pour savoir si on a une généralisation/spécialisation, on prend une instance d'une classe et on se demande si c'est aussi une instance de l'autre classe.

Sinon, on essaie avec une association (ça marche très souvent). ⚠ Vérifier qu'on n'aura pas de doublons, si oui on doit créer une classe intermédiaire.

Si on peut dire qu'une classe est composée d'une autre classe, ou fait partie, on rajoute un losange blanc car c'est une *agrégation*.

Si en plus la cardinalité max du composite est 1 et qu'on détruit le composant avec le composite, on noircit le losange car c'est une *composition*.

## Rappels formes normales

  - 0 : Une relation où on met tout dedans `R0(a1, a2, a3, ...)`
  - 1FN : Relation où tous les attributs sont de type simple (date, entier... pas de tableau) et pas calculés (date de naissance plutôt que l'âge)
  - 2FN : On définit un identifiant (grâce à un ou plusieurs attributs) et on regarde si les autres attributs dépendent de l'identifiant et de **tout** l'identifiant (ex : code postal, un bout permet de déterminer la région)(dépendance fonctionnelle élémentaire)
  - 3FN : La dépendance fonctionnelle élémentaire est en plus directe, les attributs dépendent exclusivement de l'identifiant (si `a3` dépend de `a2` en plus de `a1`, il faut découper la relation)

## Transformer un diagramme de classe en base relationnelle

Classes
  - Chaque classe devient une table
  - Chaque attribut de classe devient une colonne de la table
  - On rajoute une colonne `ID` qui sera la clé primaire (implicite en UML)
  - Chaque instance de classe devient une ligne de la table

Associations
  - `?..*` : on crée une table avec le nom de l'association, qui contient 2 colonnes avec l'id des lignes dans les tables correspondantes (en clé étrangère). Le couple d'id devient la clé primaire (ainsi pas de doublon dans ma relation). Si l'association contient des attributs, ils deviennent des colonnes dans la table.
  - `?..1` : on peut créer une table avec le nom de l'association, 2 colonnes et une clé primaire sur la colonne qui doit être unique. L'autre possibilité est de rajouter une colonne dans la table du "possédé" comme clé étrangère vers l'autre table.
