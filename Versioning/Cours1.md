Versioning
==========

Par Éric Sigoillot, Sopra Stéria

<!-- MarkdownTOC -->

- [Le versioning, c'est quoi ?](#le-versioning-cest-quoi-)
    - [Définitions](#d%C3%A9finitions)
    - [Des versions ou des révisions ?](#des-versions-ou-des-r%C3%A9visions-)
    - [Centralisé VS distribué](#centralis%C3%A9-vs-distribu%C3%A9)
    - [Le workspace personnel](#le-workspace-personnel)
    - [Des fusions \(merge\) aux conflits](#des-fusions-merge-aux-conflits)
    - [Cycle de vie simplifié](#cycle-de-vie-simplifi%C3%A9)
    - [Dans la vraie vie...](#dans-la-vraie-vie)
    - [Fonctionnement concurrent ou exclusif ?](#fonctionnement-concurrent-ou-exclusif-)
- [Solutions existantes](#solutions-existantes)
    - [Les grands du monde libre](#les-grands-du-monde-libre)
    - [Les propriétaires \(beurk\)](#les-propri%C3%A9taires-beurk)
- [Gérer des versions, un peu de pratique](#g%C3%A9rer-des-versions-un-peu-de-pratique)
    - [Un référentiel, comment ça marche ?](#un-r%C3%A9f%C3%A9rentiel-comment-%C3%A7a-marche-)
    - [Les attributions du référentiel](#les-attributions-du-r%C3%A9f%C3%A9rentiel)
    - [Comparaison entre révisions](#comparaison-entre-r%C3%A9visions)
- [SVN et Git par l'exemple](#svn-et-git-par-lexemple)
    - [Subversion](#subversion)
    - [Git](#git)
- [L'information au cœur du projet](#linformation-au-c%C5%93ur-du-projet)
- [Le branching](#le-branching)
    - [Stratégies de branching](#strat%C3%A9gies-de-branching)

<!-- /MarkdownTOC -->

## Le versioning, c'est quoi ?

> Sauvegarde  
> Revenir en arrière  
> S'assurer que tout le monde est à jour  
> Chronologie des changements  
> Identifier qui a fait quoi et pourquoi  
> Travail en groupe

Exemple de gestionnaires de version : git, Subversion, Google Drive, la corbeille, le <kbd>Ctrl</kbd>+<kbd>z</kbd>

### Définitions

Wikipédia :
> La gestion de versions consiste à maintenir l'ensemble des version d'un ou plusieurs fichiers (généralement en texte).

Définition bof, et très orientée code

> Processus permettant de **conserver une trace** des modifications successives apportées à un fichier numérique (documentation, code source, base de données), à travers un logiciel spécialisé.
> Il est ainsi possible de retrouver des données effacées, mais aussi d'effectuer de nombreuses manipulations comme *j'ai raté la fin*.

Notions importantes :
* Contrôle
* Traçabilité
* Archivage
* Suivi des évolutions

### Des versions ou des révisions ?

En réalité, on gère des révisions plutôt que des versions.

**Révision** :
* Modification opérée sur un ou plusieurs éléments gérés par l'outil (généralement des fichiers)
* Associée à un compte utilisateur unique -> traçabilité
* Possède un marqueur unique (un ID)
* Créé à une date précise
* Permettant de retrouver le contenu exact des éléments concernés à la date de création de la révision

Un CVS possède systématiquement une base de référence des révisions : le **référentiel** (ou *dépôt*). Elle sert de base pour comparer.

### Centralisé VS distribué

Centralisé : la référence est stockée sur un seul serveur  
Distribué : la référence est stockée chez tout le monde

### Le workspace personnel

Le travail fait par un utilisateur se fait sur une copie locale du référentiel !  
Chacun possède son propre **espace de travail* (ou *workspace*, *working copy*, *sandbox*).

L'espace de travail est vivant (modifié en permanence), et doit être considéré **volatile** : il faut sécuriser son espace de travail dès que possible ! (en respectant certaines règles)

-> On doit récupérer les mises à jour des autres utilisateurs, et pousser ses propres modifications pour que tout le monde reste à la page.  
-> Il faut le faire **régulièrement**, sinon ça devient vite compliqué...

### Des fusions (merge) aux conflits

Quand on travaille à plusieurs, chacun peut modifier les mêmes fichiers. Les outils peuvent faire une **fusion** automatique (ou **merge**), mais parfois il y a CONFLIT ! Et il faut un cerveau pour résoudre et choisir quelles modifications sont importantes...  
-> Opération à haut risque, car sans assistance de la part de l'outil -> Merge souvent raté car mal analysé ou précipité -> La révision est corrompue, des données sont perdues

### Cycle de vie simplifié

1. Référentiel : révision stable
2. Checkout/Update : extraction d'une révision
3. Espace de travail : modification de la révision
4. Commit : proposition d'une nouvelle révision
5. Merge/Resolve : résolution des problèmes éventuels et validation

### Dans la vraie vie...

Le cycle de vie est plus complexe : il faut initialiser le référentiel, définir d'une stratégie de gestion des versions et des éléments à contrôler, définir les autorisations d'accès...  
Les éléments doivent être ajoutés avant d'être modifiés.  
Les comparaisons entre les versions d'un même élément sont parfois limitées : comment comparer des images ?

### Fonctionnement concurrent ou exclusif ?

**Exclusif** : approche simple dans la gestion des versions  
Quand A veut travailler sur un fichier, le CVS verrouille le fichier. Si B veut travailler sur le même fichier, il doit attendre que A ait commit son travail.
* Avantages : Cohérence maximale des données, pas de problème de fusion puisqu'une seule personne travaille sur un fichier au même moment
* Inconvénients : C'est cher puisqu'on ne peut pas mener 2 tâches en parallèle, si la personne a ouvert un fichier mais ne travaille pas dessus (ou ne peux pas libérer le verrou parce qu'elle a perdu son ordinateur) on est bloqué

MAIS c'est parfois nécessaire : comment gérer les fusions entre 2 versions d'une image ?

**Colaboratif** : chacun peut travailler sur une révision quand il veut
* Avantages : Travail beaucoup plus souple, chacun avance à son rythme, pratique pour des équipes distribuées
* Inconvénients : Certaines fusions doivent être faites à la main, seront complexes à gérer et peuvent entraîner des erreurs

Il faut **former**.

## Solutions existantes

La gestion de version c'est vieeeeeeux (années 1970).  
Les outils actuellement sur le marché sont très concentrés sur du code source (c'est difficile de comparer autre chose que du texte).  
Les autres types d'éléments (un peu plus spécialisés) possèdent des outils dédiés souvent fournis par l'éditeur (Word et les révisions, MagicDraw et TeamWork...)

### Les grands du monde libre

* **Revision Control System** (RCS), années 1980, disparu aujourd'hui
* **Concurrent Versions System** (CVS), années 1990, quasiment disparu
* **Subversion** (SVN), années 2000 et toujours actif, référentiel *centralisé*
* **Git**, né en 2005, grosse *grosse* progression ces dernières années, référentiel *distribué*, utilisé par Linux, Android, et le reste
* **Mercurial** (Hg), né en 2005, moins connu que git

### Les propriétaires (beurk)

* **IBM Rational ClearCase**, années 1990, intégrée dans une suite d'outils (CleauQuest, suite Rational)
* **Microsoft Team Foundation Server** (TFS), années 2000, compatible avec git depuis quelques années
* **Atlassian Bitbucket**, centré sur git et ajoute une suite complète d'outils (JIRA, Confluence)
* **Perforce**, années 1990, bien implanté et compatible avec des systèmes libres comme git
* **Serena PVCS**, années 1980, mode d'accès exclusif

Pourquoi payer ? Le support, des engagements de performance, une intégration avec les outils des éditeurs.

## Gérer des versions, un peu de pratique

### Un référentiel, comment ça marche ?

Le référentiel peut être géré de 2 manières
* Arborescence de fichiers
* Base de données

La plupart des outils utilise un système hybride

Le stockage des révisions se fait par delta : les différences entre rev-1 et rev-2 -> gain de place  
⚠ Attention : si on perd des fichiers sur le référentiel, on ne peut pas reconstruire tout l'historique (c'est faux sur git, qui prend des images complètes des fichiers à chaque fois, mais bien optimisées)

### Les attributions du référentiel

Un référentiel ne fait pas que stocker les révisions, mais aussi :
* des métadonnées, date, numéro de révision et commentaires
* authentification et autorisations
* gestion de workflow
* garantir l'intégrité des données (il peut refuser des opérations)

### Comparaison entre révisions

On utilise un outil dédié pour mettre en valeur les ajouts, suppressions ou modifications.

* Pour des fichiers texte, la comparaison peut être précise
* Pour des fichiers binaires, ce sera probablement juste "identique" ou "différent"

## SVN et Git par l'exemple

### Subversion

Le référentiel est **centralisé**. IPQ les barbus qui tapent les commandes en CLI sont rares 😢

Fonctions de base :
* `checkout` pour récupérer une révision auprès du référentiel (quand on n'a pas déjà de version du référentiel)
* `commit` pour créer une nouvelle révision d'un fichier
* `update` pour mettre à jour l'espace de travail avec une nouvelle révision
* `resolve` pour résoudre un conflit, apparu lors d'un `update`
* `add` pour ajouter un nouveau fichier
* `delete` pour supprimer un fichier
* `move` pour renommer un fichier
* `copy` pour copier un fichier

Dans SVN, on commit assez peu (une fois par jour, 2 fois par semaine) donc les commits sont gros et peuvent entraîner des conflits

### Git

Le référentiel est **distribué**, chacun peut travailler en local et déconnecté. Pour simplifier l'utilisation de l'outil (et ne pas avoir besoin de push sur chacun des remote de chaque utilisateur), on utilise un référentiel central qui sert de source de vérité.  
Toutes les infos du référentiel sont stockées dans le dossier `.git` dans le projet.

Dans git, on commit beaucoup plus souvent, on peut annuler un commit, ils sont donc beaucoup plus petits.

Fonctions de base :
* `init` pour initialiser un référentiel
* `clone` pour récupérer une copie *complète* du référentiel (avec toutes les révisions)
* `fetch` pour obtenir les dernières mises à jour
* `merge` pour fusionner les conflits
* `pull` correspond à `fetch` et `merge` en même temps
* `push` pour envoyer ses modifications validées sur les autres référentiels
* `commit` pour valider localement ses modifications
* `add` pour ajouter un élément au commit (*pas* ajouter un fichier)
* `remote` pour déclarer un nouveau référentiel distant avec lequel échanger

## L'information au cœur du projet

Il n'y a pas que des sources dans un projet, il y a aussi la documentation.  
Un projet évolue, a un début et une fin, il faut pouvoir tracer qui a fait quelle modification, quand, pourquoi...  
L'information nécessite une traçabilité !

## Le branching

Au cours d'un projet, on a plusieurs versions qui tournent en parallèle. Par exemple, une V2 est en développement, mais la V1 est encore en fonctionnement et doit être supportée. -> On crée des branches

La conf de base est généralement appelée "tronc" (ou *trunk*), qui fait foi -> branche de prod  
Les conf parallèles seront appelées des "branches" (*branch*)  
Une fois le travail sur une branche terminé, on peut la merge sur la branche parente (ou une autre si l'outil le supporte).

### Stratégies de branching

* [Git flow](http://nvie.com/posts/a-successful-git-branching-model/)
    - une branche principale (`master`) qui est en prod
    - une branche `develop` principale pour les dev (pas forcément de commit directement dessus, mais c'est possible)
    - des branches `feature/nomdefeature`, qui partent de `develop`
    - des branches `release`, pour préparer la nouvelle version (test, bugfix, bump de version...), et mergée sur `master` quand fini
    - des branches de `hotfix` pour les bugs urgents, qui partent de master et sont reportées sur `master` et `develop`

