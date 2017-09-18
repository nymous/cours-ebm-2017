Dans la peau d'un moteur de recherche
=====================================

<!-- MarkdownTOC uri_encoding="false" -->

- [Le PageRank](#le-pagerank)
- [Un secret bien gardé](#un-secret-bien-gardé)
- [Quelques uns des 200 paramètres de ranking](#quelques-uns-des-200-paramètres-de-ranking)
- [Le PageRank, c'est fini ?](#le-pagerank-cest-fini-)
- [Le TrustRank](#le-trustrank)
- [Le SERP Rank](#le-serp-rank)
- [La Google Dance](#la-google-dance)

<!-- /MarkdownTOC -->

## Le PageRank

Les "pages" votent pour d'autres pages  
L'échelle est logarithmique, de 0 à 10 (3-4 c'est déjà beaucoup)  
Le processus de calcul est récursif -> facteur d'amortissement (*damping factor factor*, généralement 85%) pour éviter que ça ne monte à l'infini

## Un secret bien gardé

Les facteurs qui comptent et leur pondération sont secrets, mais RB va nous en donner le secret !

"Les moteurs de recherche le détestent"

## Quelques uns des 200 paramètres de ranking

Sur la page (*onpage*)
* Ancienneté de la page
* Fréquence d'actualisation
* Texte
    - visible sur la page
    - meta tags

Sur le site (*onsite*)
* Liens internes, arborescence, fil d'ariane (*breadcrumbs*)
* Paramétrage sur Google Webmaster Tools

Hors du site (*offsite*)
* Liens entrants (visibles en partie avec une recherche `link:http://fr.wikipedia.org`)
    - Leur PageRank, âge, TrustRank de la page
* Social bookmarking, tweets

-> Débat : Google utilise-t-il les données qu'il stocke sur le comportement des internautes pour le PageRank ?
* Temps passé sur le site
* Stats renvoyées par la barre d'outils Google (ça existe encore ce truc ?)
* Citations d'URL dans Gmail
* Marque-pages Google
* Âge, sexe, localisation de l'utilisateur
* Précédentes recherches

## Le PageRank, c'est fini ?

L'algo actuel s'appelle *Hummingbird*, un colibri qui s'alimente sur diverses sources :
* RankBrain (machine learning)
* Panda : qualité globale d'un site (temps de réponse...)
* Penguin : anti black-hat
* Pigeon : recherches locales
* Top heavy : pages lentes, lourdes, avec trop de pub
* Mobile friendly : "Mobilegeddon", les pages "responsive" sont mieux classées ?
* Pirate : pas de contenu copyrighté
* ... et toujours le PageRank !

## Le TrustRank

Méthode pour détecter les sites de spam : une page propre ne fait pas de lien vers un site de spam

1. Amorçage : on établit une liste de pages "propres" de références -> analyse humaine
2. Suivi récursif des liens de la liste d'amorçage
3. Plus les liens sont forts avec les pages de référence, plus leur degré de confiance est élevé

Le TrustRank est entre 0 (page de spam) et 1 (page de référence)

## Le SERP Rank

Ordre de présentation des liens quand on entre certains mots clés, à partir du PageRank

La page de résultats affiche une liste ordonnée de liens vers des pages/image/vidéos, avec un snippet en provenance de la page

-> Une page a un PageRank en fonction d'un mot clé ou d'un ensemble de mots clés

## La Google Dance

Avant, c'était la période pendant laquelle Google mettait à jour le classement des pages.  
Aujourd'hui, il n'existe plus, l'actualisation est continue.
