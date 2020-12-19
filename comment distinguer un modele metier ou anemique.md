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

Le problème étant: comment faire vivre des objets à coté d'une base de données. Et comment y accèder depuis différentes Interface Homme Machines; ces dernière se multipliant à la faveur du déploiement des internets et de clients (programme client) de plus en plus universels et versatiles (ordis, tablettes, mobiles, interface vocale, objets connectés).

Cela a donné ce genre de modélisation, on frait émerger les classes parce qu'il y a des tables dans une base de données et on les affubles de toutes les opérations possibles et imaginables:
![ugly design](uml%20model.png)

On avait envie, par principe DRY (Don't Repeat Yourself) d'avoir des objets omnipotents, qui encapsulent tout, le savoir être(l'état) et le savoir faire (les opérations), uniquement distribué par une vision purment d'objet au sens programatique du terme. Des objets avec des tonnes de méthodes. Et des objets qui se baladeraient (les mêmes) de couche en couche du sytème,  de l'interface graphique à la base de données. 
Des initiatives ultra-monolithiques telles ques des bases de données orientées objets (je pense à un vieux système français aujourd'hui disparu: O2) ou des frameworks tout en un, type WinDev (encore hélas en vie) ou FoxPro ou Delphi. Ca pouvait fonctionner sur des applis Client Lourd. Mais au prix d'un couplage immense.

Heureusement les interfaces Web et la multiplicité des solutions de stockage (sans parler des services et de la virtualisation extrême de tout cela) rend impossible de trimbaler des objets aussi lourds et chargés de tant de responsabilité.

Et tant mieux, il nous fallait un code plus simple.


# Epurer, jusqu'à l'anémie


C'est comme cela qu'on en est arrivé à des modèles d'objets anémiques.
Des classes qui représentent des entités mais qui ne contiennent aucune logique métier, car elles étaient bien souvent une émanation des DAO (Data Access Objets).

![anemic model](anemic%20model.png)

C'était pour "simplifier".
Mais on n'a fait que mettre la poussière sous le tapis. 
La logique métier remontant dans d'énormes classes de "service" ou "business layers" qui devenaient énorme parce que le métier n'était pas plus découpé. 

D'une part, ca n'a rien simplifié car on s'est retrouvé toujours pieds et points liés à la couche d'accès aux données (1).

Avec derrière tout cela, l'idée qu'une bonne couche de liaison à une base de données allait une fois de plus nous donner tout ce qu'il fallait: fais ton MCD (ou plutôt obéit à celui que le DBA a fait pour toi) et adapte ton code à cela. 

![and in the darkness bind them](one-database-to-rule-them-all.jpg)

Les ORM (Object-relational Mappers) continuaient de nous laisser croire que la méthode Merise était la bonne et que jamais nous ne nous serions capable de nous délivrer de ce fichu MCD.

Ces objets orientés "données", non contents d'être anémiques en eux même, cachaient des règles métiers dans la couche DAO: il fallait que le l'éxecution du code traverse la partie DAO pour voir apparaitre les contraintes sur les relations, les formats de données, et une partie des règles métiers que l'on savait traduire en ordre SQL: clés uniques, ou pire: triggers.

Et d'un autre coté, on codait dans la business layer (et parfois même coté client avec de beaux validateurs 🤢) bien souvent les même règles.

Puis on s'est mis à créer des services. Puisqu'il fallait bien compenser ces objets anémiques sans véritable comportement.
Et dès qu'on multipliait les services, on multipliait les règles, même si plusieurs services pouvaient finalement modifier la même entité (ou aggregat tant qu'on y est) avec chacun ses propres règles pour ses propres besoins, laissant la persistance finale se débrouiller plus ou moins bien avec des injonctions paradoxales. Bugs en pagaille assurés.

Une fois de plus, la base de données avait le dernier mot. Et les DBA jouaient le rôle d'arbitres entre équipes de devs qui se déchiraient sur la compréhension du besoin du client.

C'est du vécu!

# Puis vint DDD

Comment éviter un domaine objet anémique sans retourner aux erreurs du modèle objet old school ?
C'est à la lecture de [cet article](https://blog.pragmatists.com/domain-driven-design-vs-anemic-model-how-do-they-differ-ffdee9371a86) que j'ai eu envie d'écrire ces lignes.

La motivation d'Eric Evans, avec son livre Domain Driven Design, n'était pas tant de parler architecture logiciellle mais de représentation.
Plutôt que le mot objet, il choisit le mot entité. 
Et le plus important des concepts est celui du langage choisi, pas le langage de développement mais le vocabulaire partagé, la discussion, le nommage des choses, la sémantique commune, la conversation que les ingénieurs ont avec les experts métiers.

Cette approche orientée "Ubiquitous Language" nous oblige à poser plusieurs choses. D'abord séparer les Domaines métiers, car plusieurs se cachent forcément dans un système d'information (mot valise que je vais utiliser pour parler d'une App, d'un SaaS, d'un site, d'un prog, bref.... du code en production).
Ensuite établir des Entités regroupées en Aggrégats afin d'obtenir un Modele à l'intérieur d'une Domaine Délimité (Bounded Context).

Un atelier tel que l'Event Storming ou l'Event Modeling, nous aide à mieux savoir quoi modélier (et comment).
Il y a plusieurs choses qui émergent de ces ateliers: les évenements en premier, les commandes (ou actions en second) et très vite derrière les aggregats.
Cette séparation entre évènements et aggregats n'est pas anodine. Bien que les évènements ont des effets sur les aggrégats, les aggrégats existent pour eux même. Ils décrivent ce qui reste une fois les évènements passés. 
Les évènements sont transients. Parfois contingents. Mais ils passent. On ne peut les arrêter.
L'Event Sourcing tente de capturer ces évènements, comme on tente de capture le temps.
Ce n'est pas sans danger. On peut avec un certains nombres d'outils, remonter le temps et le cours des évènements; c'est la force de l'Event Sourcing. Avec un certain prix à payer.

Le Domain Model survit après les évènements; c'est lui que l'on montre à l'utilisateur final qui se moque pas mal des journaux de logs. Il montre l'état du monde et sa cohésion .


La question est "quelle part du business" doit se retrouver implémentée dans la face concrète du Domain Model ?

---------------------

(1)
On peut encore trouver du code assez horible comme celui ci (projet Jigsaw), où on vous impose des trucs du genre:
        
        "As you can see, the Java Beans are strictly equivalent to the table they represents. The name of the bean properties MUST be strictly equals to the column names in the SQL table."

Je tire sur l'ambulance mais il y a encore de vilains restes de cette époque, rien qu'à voir les horribles [ADO.Net datasets](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/ado-net-datasets) encore supportés.