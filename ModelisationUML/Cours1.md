Modélisation UML
================

## L'histoire de l'UML

1è standardisation UML : novembre 1997 -> 20 ans ! Happy Birthday !
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
  - Cas d'utilisation : décrit les services fournis par le système à ses acteurs (premier diagramme à faire)
  - Activités : décrit des processus (plutôt processus informatiques, limite algorithmes)
  - États-transitions : modes de marche d'un système (en panne, pas en panne, commande saisie, validée, payée, archivée, facturée...)
  - Séquences : échanges de messages entre des éléments de mon système, et leur dimension temporelle
  - Communications : structure des échanges de messages, qui dialogue avec qui (de moins en moins utilisé)
  - Chronométrage : c'est comme les chronogrammes (diagramme temps-signaux)
  - Vue d'ensemble d'interactions : *euuuuh* on s'en servira pas
