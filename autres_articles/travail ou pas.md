Que vaut le travail que l'on ne fait pas?


Je pose cette question dans le prolongement de l’excellent article de mon confrère Nicolas Brondin  (https://blog.nicolas.brondin-bernard.com/lettre-ouverte-pourquoi-le-travail-d-un-developpeur-vaut-cher/) où il explique bien que le travail de développeur ne se résume pas qu’à produire du code.

Étonnant d’en venir à justifier que l’on travaille quand on ne travaille pas. Je pense même que cela peut choquer hors du cercle des informaticiens.

Cela révèle que développer (coder) est un métier vraiment pas comme les autres. 
C’est le mien, j’en suis très fier et il ne s’agit ni d’une passade ou d’une erreur de trajectoire. Ni je pense d’un hasard.
En tout cas, ce n’est pas une honte de rester développeur jusqu’au bout et de ne pas vouloir être super chef ou commercial comme aboutissement d’une carrière. 
Savoir coder n’est pas (forcément) une transition vers quelque chose de soit disant plus honorable [^1].

Ce n’est qu’au fur et à mesure de ma progression dans ce métier que je m’aperçu que ce n'était pas un simple travail d’ingénieur au sens commun du terme. Ni de scientifique d’ailleurs. 
Nous (les développeurs) utilisons des outils de la science, mais nos productions ne sont pas des découvertes. Nous ne démontrons pas de théorèmes. Nous ne découvrons rien que nous ne sachions déjà (sur les théories de l’informatique et le travail de nos pairs avant nous).
Nous explorons simplement. 
Et surtout nous créons des choses qui n'existaient pas dans leur tout (le nouveau logiciel, la nouvelle fonctionnalité) sous une forme auparavant donnée. 
Nous créons. Nous ne découvrons pas.
Et chaque logiciel est unique.
En découle qu’il n’y a pas d'usine logicielle, au sens où notre travail n’est pas industriel.
Ce qui sort d’une industrie, d’une chaîne de montage, ce sont des séries, des copies.
Exactement ce que le logiciel n’est pas.

# On ne peut pas changer 1000 personnes 1000 fois ...

Pour preuve: donnez le même problème à résoudre à 1000 informaticiens différents, et vous aurez 1000 code sources différents.
Ne serait-ce que par l’existence de plus de 800 (parmi ceux recensés) langages de développement connus à ce jour (http://www.rosettacode.org/wiki/Rosetta_Code).
Combinez cela au fait que, dans un même langage de programmation X [^2], 10 développeurs vous produiront 10 codes sources différents, du fait même qu’émergent des styles d’écritures différents, propre à l’expérience de chacun, mais aussi à leur vécu, leur formation, et quelque chose d’impalpable qui est de l’ordre de l’intuition et la sensibilité, c’est à dire bien en dehors des domaines de la rationalité et de la science.

Oui, le travail de produire un logiciel est complexe et échappe à la science au bout d’un moment.
Alors, comment voulez-vous que nous puissions prédire “combien de temps cela va prendre à développer ???”.
Impossible avec certitude. Ne cherchez pas et passez plutôt du temps à coder!



Mais il y a autre chose, sur les “styles” de programmation.

Regardez 2 réponses (sous forme de code) au même problème (le très célèbre [kata](https://codingdojo.org/kata/RomanNumerals/) qui consiste à transformer en chiffres romains un nombre entier positif inférieur à 4000):

2e code, qui fait exactement la même chose:




Les 2 versions du code donnent le même résultat au moment de l’exécution.
Alors, pouvez-vous encore honnêtement penser que le travail de développeur se résume à la ligne de code que l’on a écrit?

> Les lignes de code n’ont aucune valeur juste par leur nombre. Au contraire.

# Montre moi ton code, je te dirai combien tu vaux

Si l’on me demandait de payer le développeur à la ligne, je n'hésiterai pas à attribuer à 80% des lignes de code une valeur négative.
Pourquoi?  
Une raison parmi tant d’autres est la lisibilité du code. Il est plus facile de lire quelque chose de concis; à condition que cela soit explicite évidemment. 
Par contre, comment mesure-t-on l’expressivité du code?

L’autre valeur négative qui se cache derrière une ligne de code en trop est le bug qu’elle va induire. Moins de code = moins de bug. Là pour le coup, c’est juste mathématique.

Autre valeur négative: la complexité du code rend difficile voir impossible sa maintenance et son évolution. Quand un nouveau cas (use case) se présente; ou bien un comportement non prévu (bug) vous devez fouiller dans beaucoup de lignes de code pour corriger. Perte de temps et d’argent.

Viens le point littéraire de l’article, merci Saint Exupéry, mais il est toujours pertinent:

> Il semble que la perfection soit atteinte non quand il n'y a plus rien à ajouter, mais quand il n'y a plus rien à retrancher.

Au passage, vous avez noté qu’il était romancier, non pas informaticien.

# De la mesure du code

Pour revenir à la valeur d’une ligne de code, nous avons des heuristiques, des guidelines, qui nous permettent de juger des qualités ou des défauts (selon un certain nombre de conventions, adaptables) du code, et qui nous poussent à l’améliorer (refactoring).
Pour moi, ce sont avant tout les principes DRY, YAGNI et SOLID, mais aussi la Connascence ou couplage (https://connascence.io/) .

Ce travail autour de la qualité du code est plutôt abstrait.
Qui sait réellement la mesurer sans équivoque? 
Ce n’est pas Sonarqube qui va vous dire si vous avez fait du copier coller, ou si vous ne respectez pas les principes SOLID. Encore plus pour du [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) ou une [Feature Envy](https://refactoring.guru/smells/feature-envy).
Rien ne remplacera une expérience/expertise humaine. 

Je vois quand même 2 bonnes mesures de qualité du code à commencer à appliquer:  la complexité cyclomatique (https://en.wikipedia.org/wiki/Cyclomatic_complexity)  et les graphes de dépendance (je pense à NDepend pour .Net).
Ceux-là devraient être intégrés comme règle dans Sonar (ou équivalent). 
On attriburait des valeurs négatives aux lignes de code qui augmentent la complexité cyclomatique et les dépendances. 
Tout comme il faut pénaliser celles qui ne sont pas couvertes par les tests.
Mais là encore, c’est une mesure qui peut être déformée (https://blogs.infosupport.com/thinking-about-test-coverage/). Voir contournée (https://medium.com/better-programming/is-code-coverage-a-useless-metric-bc76e0fde9e)

# Quantité vs Qualité

C’est donc un travail intellectuel  *énorme* que de se retenir d’écrire une ligne de code.
 Toute ligne en trop, ou de mauvaise qualité, rentre dans la catégorie de la fameuse “dette technique”.
Et d’ailleurs, qui pourrait évaluer la valeur (négative) de la dette technique que l’on s’efforce de supprimer? Comment la chiffrer?

En tout cas, le travail de frugalité intelligente, de parcimonie éclairée, ne se joue pas qu’au niveau du développeur mais aussi sur celui des architectes.
Combien de choix d’architecture logicielle, de frameworks, de librairies à la mode, qui ont conduit des projets au désastre.
Combien de frameworks (je pense aux affreux JavaBeans et autres horreurs type Corba à l’époque) qui vous impose d’écrire des tonnes de lignes de code overkill ? Imbitables ...
Ou bien si un framework n’est pas si mal pensé, combien de fois est-il vraiment bien utilisé?

Il est si facile de transformer un bon pattern en un anti pattern, juste par un mauvais usage.

Un mot pour conclure:

> Uncle Bob (Robert C. Martin): "A good architect maximizes the number of decisions not made."

Difficile là aussi de donner une valeur à l’absence. Et pourtant.

# Pour conclure, peut-on définir le travail du codeur?

Ce n’est ni science, ni industrie. Peut-être une forme d’art. Et comme dans tout art, il cache une grande part d’intangible.
N’en déplaise à ceux qui veulent tout monnayer et tout transformer en chiffres.



--------
[^1]: Pour moi, il y a d’abord eu la fascination pour les machines, et surtout la possibilité -rendue simple- de prendre le contrôle de la machine. De parler à l’oreille des machines pourrait-on dire. Pourtant, je n’ai eu que relativement tardivement (par rapport aux 1ères lignes de code que j’ai écrites) accès aux travaux d’Alan Turing , Alonzo Church et Noam Chomsky, 3 des pères de la programmation (et je dois humblement admettre que, n’ayant pas poursuivi dans le domaine de la recherche, je n’ai acquis que des bouts de leur savoir). Je n’avais pas une vraie vision de mon métier alors.

[^2]: j’aurais bien aimé dire Z, mais Zed est déjà le nom d’un langage de programmation ^^

 [^3]: Et quand bien même, qui peut dire qu’il comprend parfaitement tout ce que ces génies ont voulu nous transmettre?