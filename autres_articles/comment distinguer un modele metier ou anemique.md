# Constat
J'ai la chance de pratiquer de la modélisation d'objets dans le cadre d'applications variées, utilisant pour la peine un mix entre diagrammes UML et du Design Emergeant en codant directement les classes d'objets au fur et à mesure.

Et toujours se pose la question de : "comment organiser les classes" et surtout "quelles sont leur responsabilités". Et toujours de grands débats animent les séances de coding.

Donnant actuellement des cours UML et conception objet, c'est toujours difficille d'expliquer comment poser les bases d'un "bon" design objet.

L'apprentissage classique et nombre de tutos sur les internets qui ont emboité le pas dans la catégorie "auto formation" se délecte des exemples simplistes et absolument pas en phase avec le quotidien du développeur: le cercle, le carré, le réctangle, la forme géométrique sont les exemples donnés pour un modèles objet. Et on y colle les opérations habituelles: calculer aire ou je ne sais quoi de basique.

Avec cela, beaucoup de développeurs se font une très mauvaise idée de ce que peut être un vrai modèle objet dans une application d'entreprise qui se verra mise en production avec des milliers d'utilisateurs (ou plus j'espère) et des années de durée de vie entrainant une nécessaire maintenance et évolution.
Sans parler des corrections de bugs.

# L'héritage lancinant de Merise

Je trouve que la méthode Merise a causé énormément de tort et de retard à l'ingénierie logicielle en France (pour ce que j'en connais).
Très en vogue dans les années 80, elle est extrêment rigide et s'accorde bien du cycle de développement en V. Elle impose tout un tas de diagrammes que je qualifie sans peur de Big Design Upfront, qui ont tendance à rassurer les chefs de projets et les développeurs quand il faut s'attaquer à développer un système sans trop savoir où cela va nous mener.

La méthode de modélisation Merise ne prône pas l'agilité, et pour moi elle mène a des architectures d'application trop rigides et fortement couplées, avec une qualité de design très pauvre.

Cela aboutit bien souvent à des vues d'ingénieurs complètement déconnectés des utilisateurs finaux.

Elle se base aussi sur un postulat bien encombrant: tout est piloté par une base de données, relationnelle qui plus est!



Cette ommiprésence de la base de données (et des gens qui en sont les gardiens, à savoir les concepteurs et les administrateurs, les fameux DBA longtemps très recherchés et considérés comme des demi-dieux) nous avait amené à ériger en modèle de programmtion parfait l'architecture N-tiers, dans laquelle la couche de persistance (l'accès à la base de données) était la fondation de tout et surtout dictait son  modèle aux autres couches. D'horribles dépendances se créaient. Mais après tout c'était du Merise à la lettre.

Evidemment cette dépendance au choix d'un SGBDR et un tel couplage était rapidement source d'un coût de maintenance insuportable. Chaque changement de SGBDR demandait la ré écriture du tout.

Et aussi ce posait le problème de la responsabilité attribuée à la base de données, qui allait même jusqu'à gérer les règles métiers complexes, avec l'échouage ultime qu'était l'utilisation de triggers, ou le comportment était mélé de manière inextricable au simple stockage.

# Poussée du design objet

Heureusement les librairies et les frameworks (ouille) nous ont poussé vers d'autres design d'architecture.

Le problème étant: comment faire vivre des objets à coté d'une base de données. Et comment y accéder depuis différentes Interface Homme Machines; ces dernière se multipliant à la faveur du déploiement des internets et de clients (programme client) de plus en plus universels et versatiles (ordis, tablettes, mobiles, interface vocale, objets connectés).

Cela a donné ce genre de modélisation, on fait émerger les classes parce qu'il y a des tables dans une base de données et on les affubles de toutes les opérations possibles et imaginables:
![ugly design](uml%20model.png)

On avait envie, par principe DRY (Don't Repeat Yourself) d'avoir des objets omnipotents, qui encapsulent tout, le savoir être(l'état) et le savoir faire (les opérations), uniquement distribué par une vision purement d'objet au sens programatique du terme. Des objets avec des tonnes de méthodes. Et des objets qui se baladeraient (les mêmes) de couche en couche du système,  de l'interface graphique à la base de données. 
Des initiatives ultra-monolithiques telles que des bases de données orientées objets (je pense à un vieux système français aujourd'hui disparu: O2) ou des frameworks tout en un, type WinDev (encore hélas en vie) ou FoxPro ou Delphi. Ca pouvait fonctionner sur des applis Client Lourd. Mais au prix d'un couplage immense.

Heureusement les interfaces Web et la multiplicité des solutions de stockage (sans parler des services et de la virtualisation extrême de tout cela) rend impossible de trimbaler des objets aussi lourds et chargés de tant de responsabilité.

Et tant mieux, il nous fallait un code plus simple.


# Epurer, jusqu'à l'anémie


C'est comme cela qu'on en est arrivé à des modèles d'objets anémiques.
Des classes qui représentent des entités mais qui ne contiennent aucune logique métier, car elles étaient bien souvent une émanation des DAO (Data Access Objets).

![anemic model](anemic%20model.png)

C'était pour "simplifier".
Mais on n'a fait que mettre la poussière sous le tapis. 
La logique métier remontant dans d'énormes classes de "service" ou "business layers" qui devenaient énorme parce que le métier n'était pas plus découpé. 

D'une part, ca n'a rien simplifié car on s'est retrouvé toujours pieds et points liés à la couche d'accès aux données [^1].

Avec derrière tout cela, l'idée qu'une bonne couche de liaison à une base de données allait une fois de plus nous donner tout ce qu'il fallait: fais ton MCD (ou plutôt obéit à celui que le DBA a fait pour toi) et adapte ton code à cela. 

![and in the darkness bind them](one-database-to-rule-them-all.jpg)

Les ORM (Object-relational Mappers) continuaient de nous laisser croire que la méthode Merise était la bonne et que jamais nous ne nous serions capable de nous délivrer de ce fichu MCD.

Ces objets orientés "données", non contents d'être anémiques en eux même, cachaient des règles métiers dans la couche DAO: il fallait que le l'exécution du code traverse la partie DAO pour voir apparaitre les contraintes sur les relations, les formats de données, et une partie des règles métiers que l'on savait traduire en ordre SQL: clés uniques, ou pire: triggers.

Et d'un autre coté, on codait dans la business layer (et parfois même coté client avec de beaux validateurs 🤢) bien souvent les même règles.

Puis on s'est mis à créer des services. Puisqu'il fallait bien compenser ces objets anémiques sans véritable comportement.
Et dès qu'on multipliait les services, on multipliait les règles, même si plusieurs services pouvaient finalement modifier la même entité (ou agrégat tant qu'on y est) avec chacun ses propres règles pour ses propres besoins, laissant la persistance finale se débrouiller plus ou moins bien avec des injonctions paradoxales. Bugs en pagaille assurés.

Une fois de plus, la base de données avait le dernier mot. Et les DBA jouaient le rôle d'arbitres entre équipes de devs qui se déchiraient sur la compréhension du besoin du client.

C'est du vécu!

## Un peu de code...

Un petit Kata exemple:  Tell Don't Ask avec le TyrePressure Monitor ou le CpuMonitor
la règle remonte non pas dans le service mais dans la classe moniteur qui est utilisée par le service, afin que cette dernière 'affirme' (tell) la règle au lieu que ce soit le service qui demande (ask) des valeurs internes au moniteur. La logique (fonction) qui a besoin d'une donnée doit se trouver dans la même classe que cette donnée.

Le résultat est [ici](https://github.com/guillaumeagile/seed-TS-promises/tree/7059a8d93a249a1260fa06da25429828413de994).

> Things that change together should be together. (Fowler)

# Puis vint DDD

Comment éviter un domaine objet anémique sans retourner aux erreurs du modèle objet old school ?
C'est à la lecture de [cet article](https://blog.pragmatists.com/domain-driven-design-vs-anemic-model-how-do-they-differ-ffdee9371a86) que j'ai eu envie d'écrire ces lignes.

![DDD model](domain%20model.png)

L'idée étant de pouvoir décrire un modèle affranchi des contraintes qui ne sont pas les siennes.
Se sauvegarder dans une base de données untel ou s'afficher à l'utilisateur sur un interface Z (il y a des milliers de frameworks pour faire le beau sur le Web[^2])) ne concerne en rien, absolument en rien le Modèle du Domaine d'une App ou d'un SI.


# DDD à la rescousse 

La motivation d'Eric Evans, avec son livre [Domain Driven Design](https://www.dddcommunity.org/books/), n'était pas tant de parler architecture logiciellle mais de représentation.
Plutôt que le mot objet/classe, il choisit le mot entité.
Et le plus important des principes qu'il a voulu mettre en avant est celui du langage parlé.
Pas le langage de développement mais le vocabulaire partagé, le nommage des choses, la sémantique commune, la conversation que les développeurs doivent avoir avec les experts métiers.

Cette approche appelée "Ubiquitous Language" nous oblige à poser plusieurs choses.
D'abord séparer les Domaines métiers, car plusieurs se cachent forcément dans tout système d'informations (mot valise que je vais utiliser pour parler d'une App, d'un SaaS, d'un site, d'un prog, bref.... du code en production).
Ensuite établir des Entités regroupées en Agrégats afin d'obtenir un Modèle à l'intérieur d'un Domaine Délimité (Bounded Context).

Un atelier tel que l'[Event Storming](https://www.eventstorming.com/) ou l'[Event Modeling](https://eventmodeling.org/), nous aide à mieux savoir quoi modéliser (et comment) en partant de zéro et sans connaissance technique particulière (des posts its , des stylos et de grands murs suffisent).

Il y a plusieurs choses qui émergent de ces ateliers: les évènements en premier, les commandes (ou actions en second) et très vite derrière les agrégats et leur "policies".
Cette distinction entre évènements et agrégats n'est pas anodine. Bien que les évènements aient des effets sur les agrégats, les agrégats existent pour eux même. Ils décrivent ce qui reste une fois les évènements passés. Et leur "policies" est leur profession de foi, ce qui est toujours vrai pour eux (et leur entourage proche).

> Voila pourquoi la modélisation du Domaine en Agrégats (Entités + Value Objects) va nous enrichir en "règles métiers", tout en traitant par ailleurs les évènements.

(Pour en savoir plus sur l'Event Storming il y a foule d'articles et bien sûr de publications à ce sujet, mais peu en [français](https://cleandojo.com/2019/06/event-storming-modelisez-votre-domaine-metier-en-equipe/).)

Les évènements sont transients. Parfois contingents. Mais ils passent. On ne peut les arrêter.
L'Event Sourcing tente de capturer ces évènements, comme on tenterait de capture le temps.
Ce n'est pas sans risque. On peut avec un certains nombres d'outils, remonter le temps et le cours des évènements; c'est la force de l'Event Sourcing. Avec un certain prix à payer.

Le Domain Model survit après les évènements; c'est lui que l'on présente (sous une forme adaptée, dite View Model ou [Read Model](http://gorodinski.com/blog/2012/04/25/read-models-as-a-tactical-pattern-in-domain-driven-design-ddd/) à l'utilisateur final, lequel se moque pas mal des journaux de logs. Les éléments du modèle montrent l'état (partiel) du monde (tel que manipulé dans un contexte donné) et sa cohésion.

Mais, j'aurai le plaisir de vous parler des évènements dans une autre article.

Et d'aller plus loin dans la modélisation objet d'un domaine dans la suite de cet article.





------------------------




# Previously (TL;DR)

Ne pas vouloir faire des objets anémiques, et respecter le Tell Don't Ask, c'est bien.
Remettre toutes les logiques dans des classes obèses, c'est mal.

![tell dont ask schema](https://martinfowler.com/bliki/images/tellDontAsk/sketch.png)

J'ai d'ailleurs trouvé (après avoir écrit mon billet précdent) un [article en anglais qui dit à peu près la même chose](https://blog.codecentric.de/en/2019/10/ddd-vs-anemic-domain-models/).

Toute la logique dans les objets? Non. Martin Fowler en parle un peu dans son article d'ailleurs.
Il existe une approche qui nous invite à y réflechir en détail, elle se nomme: Domain Driven Design.

# Modéliser un Domaine avec sa cohérence

Pour assurer la cohésion du modèle, on va donc parler de règles. Règles métier. Mais se cachent beaucoup de choses derrière ce terme.
Pourtant, la règle c'est quelque chose qui doit pouvoir se vérifier. C'est ce qui doit toujours être vrai; sinon ce n'est plus une règle.

Comment placer ces règles dans le Modèle de Domaine, sans surcharger les objets de méthodes, car en réalité un modèle s'explore bien par ses attributs, rarement par ses opérations.

C'est là que DDD nous offre quelque chose de plus puissant que des méthodes calées sur des objets:  les [Value Objects](https://medium.com/swlh/value-objects-to-the-rescue-28c563ad97c6).

Je ne vais pas vous expliquer ici toutes les subtilités des Value Objects, mais sachez deux choses;
les Values Objects sont un élément clé d'un bon design objet (appliquant les principes DDD) car:
1. ils se basent sur un typage fort (ils remplacent des types primitifs, trop agnostiques)
2. ils encapsulent des règles métier (de par leur typage) car ils se valident eux-mêmes.

Ainsi, avec le temps, les opérations qui prenaient des termes désuets comme "Validation", disparaissent au profit d'une cohésion qui réside dans les propriétés des Entités, au mieux sous forme de Value Objetcs, mais pas que.

C'est un point de vue qui choque pas mal de développeurs et concepteurs objets.
Ils pensent que des classes d'objets sans opérations sont anémiques.
C'est faux.


> Another good warning sign of trouble is (...) a class that has only fields and accessors. That's almost always a sign of trouble because it's devoid of behavior.  [M. Fowler](https://martinfowler.com/bliki/GetterEradicator.html)
 
Ce n'est pas vrai. Enfin pas tout à fait. Il faut être plus malin que ca.

>Look for who uses the data and try to see if some of this behavior can be moved into the object.  [M. Fowler](https://martinfowler.com/bliki/GetterEradicator.html)

Une classe qui n'a que des Settes et Getters, n'est peut être pas dépourvue de logique; il faut aller regarder le code des propriétés, c'est aussi un bon endroit pour ranger de la logique métier propre aux Entités.

Si vous poussez au bout la logique de chasser les "Primitive Obsessions", vous allez créer des types non primitifs, qui en plus d'avoir un sens métier, révèlent un comportement métier de par leur existence (et donc à leur construction).

Etant donné qu'un Value Object se doit d'être immutable (si une valeur est modifiée, cela devient une nouvelle valeur), la logique (vérification de règles) va donc se loger dans son constructeur, aucune méthode supplémentaire n'est utile.
A lire: [to mutate or not](https://www.schibsted.pl/blog/immutability-entities-and-value-objects/) .

De l'extérieur cela pourrait ressembler à un objet anémique. A l'intérieur, c'est bien lui qui tient toutes les règles métiers de l'entité désignée.

>A good rule of thumb is that things that change together should be together.


## Un peu de code...

Je reprends mon petit Kata de m'article précédent: [implémenter Tell Don't Ask en TDD avec un TyrePressure Monitor ou un CpuMonitor](https://github.com/guillaumeagile/seed-TS-promises/tree/7059a8d93a249a1260fa06da25429828413de994).
Dans mon code, j'ai réussi une premier refacto : la règle de vérification de surchauffe remonte non pas dans le service mais dans le moniteur, mais on doit appeler  une méthode 'hasAlert' pour savoir ce qu'il se passe.

Il est facile de refactorer cette méthode en propriété, pour désigner un état.
Un état qui serait partie intégrante du Modèle, plutôt qu'une méthode.

Mais pour ajouter la  règle suivante, comment faire?
> une température ne devrait pas être en dessous du minimum absolu (-273.15°C) et l'on pourrait choisir l'unité de temperature (Celcius ou Kelvin) et la conversion devrait se faire.

Il suffit pour cela de chercher les Primitives Obsessions.
Une valeur de temperature n'est pas un entier ou un number, mais un type à part entière. C'est une Temperature.
Les règles métiers sont dans son constructeur mais aussi dans la surcharges des opérateurs : equalTo, greaterThan, lowerThan, hashCode et + (add).
J'ai voulu le coder en typeScript mais je me suis fais avoir par la limitation de ce langage: je ne peux pas surcharger les operateurs standards, à part 'valueOf'.
Tant pis, j'ai quand même pu capturer l'idée dans des méthodes. Un langage propre m'aurait permis de masquer ces méthodes en surchargeant les opérateurs courants ( == , < , > , + ).

[Vous pouvez voir mon repo ici](https://github.com/guillaumeagile/seed-TS-promises/tree/cpuMonitorKata) .

Bon, heureusement il y a d'autres langages de programmation plus sympatoches, et je ne citerai ici que C# (oui c'est orienté 😅) qui dans ses dernières versions nous offre encore plus de facilités avec ses "Records" immutable par nature (rattrapant un retard qui avait été pris sur les "mordernes" langages fonctionnels à la mode aujourd'hui)
[Les Records de C# pour vos Objets Valeurs](https://enterprisecraftsmanship.com/posts/csharp-records-value-objects/)


## Et pour les entités alors?

Une partie logique va aussi venir se loger tout naturellement dans les "Setters", pour les entités mutables.
Après tout, accéder à une information via un "Set", permet de déclencher toutes les règles métiers au meilleur moment.
Avec l'avantage que c'est le compilateur qui va venir brancher sur le code de vérification quand une modification (set) de la propriété est demandée. Systématique, propre, net.

Mais attention.

Quand il s'agit de manipuler des attributs portant sur autre chose que des Values Objects appartenant à une entité (donc une autre entité), on peut dire que l'on a 2 cas:
- la propriété n'a pas de multiplicité; dans son Setter peuvent se jouer les règles à vérifier lorsqu'on fait changer l'état de l'objet à travers cette propriété.
- la propriété a une multiplicité (n..m), ce qui va nous obliger à exporer un type d'objet qui finalement n'a rien avoir avec notre domaine: Array, HashMap, Collection, List, Dictionnaire...  you name it!

Même si ces types sont génériques, qui vont nous permettre de finalement accèder à la sous entité qui a du sens pour notre domaine, ils exposent un certain fonctionnement (table, queue, collection, liste chainée, associations) qui n'est peut être pas exactement ce que le métier nous dicte.

Par exemple: ces types vont juste exprimer la collection (pour employer un terme vague) de l'information dont votre entité à réellement besoin. Mais comment gérer le fait qu'il y en a une multiplicité particulière (et parfois contrainte)? Ou une condition de non répétition d'un élément dans la liste (unicité)? ou autre?

Et après tout, pourquoi une collection, une liste, un tableau, une hasmap? Pourquoi exposer dans une Modelé Domaine ce qui n'est qu'un choix d'implémentation qui convient au développeur à ce moment, et qui surement posera problème au moment de sérialiser (vers une persistance ou un couche graphique)?

https://deviq.com/exposing-collection-properties/


## Moving towards intention-revealing interfaces

> keeping the aggregates and entities pure and Occam-esque. 

Ne serait il pas judicieux d'exposer juste des capacités?
L'important est de savoir ce que l'on peut faire (et ne pas faire) avec les propriétés d'une entité.
Si cette propriété est unique, parfait, son type nous dit ce qu'elle doit être.
Si elle affiche une multiplicité, il est important de savoir ce que on peut en faire:
l'énumérer, la parcourir de façon indexée peut être, la modifier? Mais comment? Sous quelles conditions?

Peut-être que le métier veut que l'on ne peut qu'ajouter des éléments, pas les supprimer?
Ou au contraire, peut être que tous les éléments ont été déjà crées initialement, qu'on ne peut pas y toucher, juste tout effacer d'un coup?
Peut être encore que la liste n'est qu'en lecture seule, ce qui ne veut pas dire qu'il est simplement interdit de la remplacer par une autre liste, mais qu'on ne peut modifier aucun des éléments qui la contient.

Tant de possibilités!
C'est là que les interfaces de classes nous seront utiles.

> [Cook]  definition is clearly based on established object-oriented principles: “maintain encapsulation” and “code to an interface, not an implementation” . 
Joseph Junkler on [Abstract Data Types and Objects](https://medium.com/@jnkrtech/abstract-data-types-and-objects-17828bd4abdc), quoting [Willian Cook](https://www.cs.utexas.edu/~wcook/Drafts/2009/essay.pdf).

(I)Enumerable/Iterable par exemple, nous informe que nous pouvons parcourir la collection d'une manière indépendante de la façon dont elle est représentée en mémoire (la capacité d'énumération est commune à toutes les structures qui accumulent des objets).

Alors qu'avec une interface de style (I)List nous indique que nous pouvons faire varier la taille de la liste.

La beauté des interfaces est qu'on peut en hériter d'autant que nécessaire, mais seulement du nombre suffisant pour satisfaire nos exigences métier.
C'est là que le principe [Interface Segration](https://blog.ndepend.com/solid-design-the-interface-segregation-principle-isp/) rentre en jeu.
La séparation entre IList et IEnumerable (en .Net) résulte bien de ISP

La frugalité étant d'exposer le strict nécessaire; pas la peine de dire: j'utilise telle structure de données en interne. Pas la peine non plus d'infliger au monde entier des exceptions si quelque chose se passe mal avec cette structure.

Le fait de gérer des listes avec des règles métiers contient plus d'intelligence qu'une quelconque implémentation de liste fournie par n'importe quel language et son framework associé. Il nous faudra améliorer ce que font les listes standards.
 En particulier lors de toute tentative de modifier la liste, puisque c'est à ce moment là que rentre en jeu des règles métiers, il faudra que le résultat de cet ajout puisse refléter que une règle métier ait été violée.

C'est pourquoi j'encourage dans le cadre d'un modèle DDD à développer des Interfaces génériques explicites, du style (I)ListeSansDoublonsNonModifiable  ou (I)ListBornée.
Oui, j'utilise la langue française quand mon appli est developpée par des francophones uniquement 😊.

Le meilleur design pour obtenir un "feedback" de la part d'une méthode n'est certainement pas de renvoyer des exceptions. Les exceptions cassent la logique du code, et ne sont pas vues par le compilateur. Certains n'hésitent pas à les comparer à des "goto"  (*TODO ref here*).
Une fonction devrait toujours retourner une valeur en sortie à celui qui l'a appelé.
La fonction Add() d'une collection de T (T type des élements contenus par cette collection)  pourrait vous retourner l'objet de type T effectivement ajouté.
Mais au cas où cet ajout est infaisable (car il casse une règle métier), une monade MayBe&lt;T&gt; (ou Perhaps) sera un type de retour très expressif.
Peut être que l'objet T sera ajouté à la collection, ou peut être pas. Il est très facile de jouer avec ce type de retour pour ensuite prendre les dispositions qu'il convient.


Cette manipulation des entités est à orchester (ou coordonner) dans la partie Service.

Ainsi, il sera bon de se poser la question: pour ajouter un objet  objT de type T avec la fonction Add(objT: T) de l'entité E, qui doit instancier l'objet objT?  Qui fait le new?

Il n'est pas bon de laisser n'importe qui faire les instanciations des objets du domaine.

En général ces objets n'émergent pas de n'importe où.

Soient ils étaient déjà connu par le système (dans une persistance ou dans un service tiers), soient ils sont nouveaux mais vont servier par la suite (et pourront être éventuellement persisté, mais on ne sait pas à priori sous quelle forme)
Moins on en sait, mieux on se porte.





Prenons l'exemple de ce code:
https://github.com/zkavtaskin/Domain-Driven-Design-Example/blob/master/eCommerce/DomainModelLayer/Carts/Cart.cs

L'on voit 2 méthodes s'ajouter au constructeur; l'une pour ajouter un CartProduct à un collection qui fait partie l'objet Cart en cours.
L'autre pour supprimer un CartProduct à la collection dans Cart. Et une dernière pour effacer toutes les CartProduct de Cart.

Mais ces fonctions ne font que modifier l'état interne de l'objet Cart.





> aggregates should reference other aggregates using only the identity instead of direct association


# 2 grosses questions en suspens

>"Alors, quoi, toutes les règles de validation dans le domaine, ca ne pose pas problème?"

A moi non, et je ne suis pas le seul. Je vous renvoie à un tout récent article que j'ai lu alors que j'étais en train de finir le présent article (je vous jure!)...(ne jurez pas Marie Thérèse!)...(référence cinématographique 😄)
[Always-Valid Domain Model](https://enterprisecraftsmanship.com/posts/always-valid-domain-model/?__s=pe49kel8e59wl0x323nu) or not?

>Deuxio "quelle part du business" doit se retrouver implémentée dans la face concrète du Domain Model ?
Qui répond un peu à la première: ce qui n'est pas invariant dans le modèle de domaine n'a bien sûr rien à faire dans celui ci.
C'est alors que les vérifications dépendantes du contexte peuvent aller dans la partie "Thin Service/Application Logic" ou peut être dans une partie de votre architecture totalement orientée "Feature" et non Modèle.

Mais j'ai eu aussi à coder des dérivations d'un modèle, des dérivées locales (au sens, par pays, par culture, par localisation du contexte) et pour cela il m'a fallu "étendre" ou "encapsuler" les entités de domaines dans d'autres classes et laisser un astucieux mécanisme choisir de charger l'extension locale d'un modèle à la run-time.
Bien sûr chaque extension à son jeu de règles, qui est écrit en TDD et donc testé entièrement.
Comme ce modèle dérivé est compatible en type avec le modèle de base, alors il est persistable ou utilisable par tout port/adapter qui s'adosse au modèle général.


## Validation ou Invariants?


## Que faire des stacks front end
et de leur validation facile à coder?

## Two-step validation
Also consider two-step validation. Use field-level validation on your command Data Transfer Objects (DTOs) and domain-level validation inside your entities. You can do this by returning a result object instead of exceptions in order to make it easier to deal with the validation errors.

Using field validation with data annotations, for example, you do not duplicate the validation definition. The execution, though, can be both server-side and client-side in the case of DTOs (commands and ViewModels, for instance). 


# Un mot sur la persistance et les ORM
Si les ORM sont la solution la plus efficace pour les "zones" de votre système où le CRUD fait loi, il n'en est pas de même pour les View Model de DDD.
Déjà, comme vous pouvez le lire un peut partout, CQRS est une approche quia un coût de développement non négligeable.
Là où le CRUD se suffit, n'allez pas faire du CQRS/ES.

Pour les View Model, attention à ne pas faire du mapping Objet Relationnel sauvage.
Le problème reste toujours le N+1 Select.
"no ORM, no mapping magic, no problem! " si on veut être extrême.

Simplement, j'aime bien le terme View Model, car en effet, ce que l'on veut faire apparaitre sous forme objet (pour ensuite le présenter à une couche graphique) est bien une Vue (au sens SQL du terme; HQL ca passe aussi) plutôt qu'un assemblage de tables/classes.

Il est donc inutile, voire contre performant, d'exposer les entités telles que le mapper ORM vous les montre par défaut, pour un affichage à l'utilisateur.

---------------------

[^1]: On peut encore trouver du code assez horible comme celui ci (projet Jigsaw), où on vous impose des trucs du genre:
        
        "As you can see, the Java Beans are strictly equivalent to the table they represents. The name of the bean properties MUST be strictly equals to the column names in the SQL table."

Je tire sur l'ambulance mais il y a encore de vilains restes de cette époque, rien qu'à voir les horribles [ADO.Net datasets](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/ado-net-datasets) encore supportés.

[^2]: Si un framework de présentation (je pense à tous ceux basés sur les patterns MMVM ou MVP ou MVC) vous demande de placer dans sa couche à lui (son environnement si vous préférez) un modèle, je pense que vous pouvez le jeter par la fenêtre et lui cracher dessus.
Le modèle métier n'appartient pas à la couche de présentation. La couche de présentation manipule un View Model