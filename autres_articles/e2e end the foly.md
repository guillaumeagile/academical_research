C'est un peu mon dada depuis des lustres cette affaire; et la source de discussions très animées avec mes pairs.
Et pourtant, je ne peux cesser de l'affirmer pour l'avoir vécu de l'intérieur.
Les [tests End 2 End](https://levelup.gitconnected.com/the-problem-with-end-to-end-tests-65509df4bc7a), E2E pour les intimes, sont [un véritable enfer](https://www.stevesmith.tech/blog/end-to-end-testing-considered-harmful/).
Un enfer pavé de bonnes intentions.
Une facilité qui se transforme de suite en [handicap](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html).

Une solution vers laquelle on plonge d'autant plus facilement quand on fait du quick & dirty, pour ce rassurer.

Une solution trompeuse, pour ceux qui ne veulent pas ..............

C'est finalement la même chose que le sucre dans l'alimentation. C'est bon, c'est pas cher, ca se trouve partout, ca fait consenus.
Mais ca rend obèse et diabétique.
Et quand vous y avez goûté, le piège se referme sur vous.

# Pourquoi?

D'abord, pourquoi en faire?
Plusieurs arguments pour:

##Parce que je veux vérifier pour pas cher
Les tests End 2 End délivrent 2 mensonges: 
1) que l'on va tout vérifier en une passe
2) que c'est pas cher
3) que c'est fiable

##Parce que je ne sais pas faire autrement

##Parce que tout le monde fait ca
C'est un peu comme de dire que puisqu'il y a tant de gens qui croient que la terre est plate, alors forcément, elle l'est. (Ca marche aussi pour l'existence de Dieu, mais je ne critique pas la foi, j'essaie juste d'être rationnel et je vous renvoie à cette [excellente vidéo sur le sujet](https://youtu.be/0wAy0Kptq3c). 


# Que dit la littérature sur le sujet?

Il y a plusieurs pistes, dont une fait référence absolue.
[La fameuse pyamide des tests](https://martinfowler.com/articles/practical-test-pyramid.html).
Tout le monde la connait mais en pratique très peu la respectent.
Pourquoi? J'en ai déjà parlé ci-dessus et j'avoue que les bras m'en tombent au final.
On sait, mais on ne veut pas voir.
Parce qu'il y a un manque de courage certains.
Et parce qu'on veut s'arranger avec la réalité.

Pourtant il suffit de savoir lire: la pyramide est inversée. La base représente la partie la plus large. Là où tout repose. Donc quelque chose de solide. Et c'est là que les tests unitaires se trouvent.
Et par tests unitaires, on parle bien de ceux écrit dans une démarche TDD. Red, green, refactor.


Le haut, c'est un peu la cerise sur le gateau, et là où beaucoup trop de gens ont écrit E2E, il aurait mieux fallu marquer: Exploratory ou Smoke tests.

Mais le "très peu" est vite transformé en beaucoup, comme ca, presque sans s'en rendre compte.
Egalement, on se dit que les tests unitaires c'est compliqué, et que le TDD, bah, ca prend du temps. Et surtout ca demande des compétences et qu'"on verra plus tard".

Et le "plus tard", c'est justement le test E2E. Celui qui vient à la fin.

Si Uncle Bob, Martin Fowler, Kent Beck ne manquent pas d'avoir proféré toutes les injonctions à l'endroit du TDD et à l'encore du E2E; d'autres auteurs n'ont pas toujours été aussi clair.

Dans un livre pourtant bien écrit ( [Unit Testing Principles, Practices, and Patterns ](https://www.manning.com/books/unit-testing) ), Vladimir Khorikov est revenu tout récement sur la mésinterpretation croissante de son propos sur les tests E2E; il en a fait plusieurs sujet de sa [newsletter](https://enterprisecraftsmanship.com/?), et je reprends quelques de ses arguments plus loin.

Et il y a les ultra convaincus, qui n'y vont pas par quatre chemins: les tests E2E sont une arnaque! (et ca, c'est pour rester poli)

[J'ai cité TDD cinq fois à ce stade, laissez moi vous recommander un peu de lecture sur le sujet](https://www.softwaretestingnews.co.uk/adopting-the-test-pyramid-model-approach/).

# Combien ca coûte?

Très cher! Trop cher!
Un test E2E parait facile quand on regarde les 2 tutos et les 3 bouts d'exemples qui trainent partout.
Tous les gens qui font du E2E de manière intensive ne se rendent pas compte qu'ils ont misé sur un cheval boiteux.
Mais comme c'est leur cheval (de battaille même, pourtant moi j'appelle cela un mulet), ils ne descendront jamais du canasson pour voir à quelle vitesse il se déplace réellement.

Trop cher, car long à faire tourner. Donc boucle de feedback beaucoup trop longue.
J'ai travaillé avec des éditeurs logiciels chez qui il fallait lancer les testes E2E (tout piloté par Selenium) le vendredi et prier le weekend pour avoir un résultat viable le lundi matin. 
Parce que le test pouvait échouer, non pas à cause d'un vrai bug dans le code, mais parce que toute la machinerie mise en branle par cette suite incommansurable de tests était fragile et cassait toute seule d'elle même. Un naufrage.
D'ailleurs ce sont des sociétés qui ont plié boutique depuis.

Donc je parle en terme purement économique. Financier. Money!!!


# Sont-ils fiables ?

NON!
 Les tests E2E ont comme principales caractéristiques de vouloir tout tester, donc de tirer toutes les dépendances du monde; cela peut être (liste non exhaustive):
 * des APIs tierces
 * des bases de données / système de fichier
 * des fichiers externes
 * des systèmes de communication (vulgairement des Entrées/Sorties) 
 * des librairies tierces
 * le temps! (indéterminisme)
 * la génération de nombres aléatoires, et tout ce qui se base dessus: numéros de séquence unique (Guid), Cryptographie...
 
Et pour ajouter de la difficulté dont on se passerait bien, certains de ces dépendances peuvent présenter des comportements asynchrones et/ou indeterministes.

Beaucoup se risquent à régler les 2 derniers problèmes avec des exceptions, ce qui ne règle rien, alourdit votre code (en temps d'execution et pire en lisibilité) et rend l'ensemble encore plus sujets aux bugs. Bref, rien ne va!

Deux symptômes apparaissent:

## Les faux négatifs
Quand un test E2E plante c'est souvent parce qu'une de ses dépendances à planté. 
Base de données ne répond plus ou n'a pas les bonnes données par exemple.
Hors ce n'est pas le comportement du système tiers que vous voulez tester, car celui-ci est déjà testé par ailleurs (ou devrait l'être par son fournisseur si celui est un minimum sérieux).
Vous voulez savoir comment un seul de vos composants, celui qui fait l'interface (ou mieux l'adaptation) avec le dit module externe, se comporte en cas de problème. C'est tout.
Comment ensuite le problème se "transporte" à l'intérieur de votre ensemble de composants devrait être réglé par une programmtion sérieuse (principes SOLIDES, ne pas utiliser les exceptions, utiliser des monades de type Result ou MayBe ou Optional) et finalement ne sera qu'un problème de typage et donc de compilation, pas de tests à proprement parler.  Tellement plus simple!

Un faux négatif reflète un test coûteux à maintenir, car il vous faudra pas mal de temps (surtout pour chercher d'où vient le problèlme puisque vous faites jouer toutes les dépendances en même temps avec des effets de bord de partout) pour le debugger et lui redonner un comportement normal. Ou bien il aura tendance à revenir instable assez souvent.

## Les faux positifs

Toutes ces dépendances traversées par les tests E2E vous amènent à écrire des tests qui ne testent pas vraiment votre code, in fine.

Il arrive que supprimer des lignes de notre code n'impacte aucun test E2E, car c'est hors des radars des dépendances, et je le redis, les tests E2E ne font que ca.

Du coup, vous livrez un bug mais vous ne voyez rien passer.
Par contre, vos utilisateurs ne manqueront pas de tomber dessus très rapidement.

De même si des tests E2E échouent alors qu'un refactoring est correct (C'est la resistance au refactoring) c'est qu'il y a trop de dépendances mal branchées, et que vous ne vous êtes par préoccupé des contrats entre votre code et les dites dépendances.  


# Alors, c'est quoi un bon test?

Il doit avoir 4 grandes propriétés:

##Proteger contre les  regressions 
Un modification de code entrainant un retour en arrière sur un resultat attendus devrait faire passer un test au rouge.
Pour éviter cela, vous pouvez vous doter d'un outil pour faire du test de mutation (mutation testing).
Donc absence de faux positifs (des tests qui resteraient verts alors qu'ils devraient être rouges).
Donc détection de bugs efficace.

##Resistant au refactoring 
Le refactoring de code (donc sans changement de comportement) ne doit pas faire passer vos tests existants au rouge.
Donc absence de fausses erreurs (faux test rouge)


##Donner un feedback très rapide
un test ne devrait pas prendre plus de quelques dixième de secondes pour donner son résultat.
Donc pas d'attente, pas de boucles, pas de sleep ou wait (sérieusement? vous pensiez tester comme ça du code asynchrone??? 🤯). Personne ne devrait accepter attendre plus d'une demi-heure pour avoir les résultats d'une campagne de tests.

##Maintenable
Des journées à écrire un test, à le faire passer au vert puis à le modifier ou le consolider?
Allons, allons. Il est temps de faire table rase de tout cela.

Il faut qu'il soit [facile à écrire](https://martinfowler.com/testing/), et facine à lire bien entendu.
Plus il y a de lignes de code dans un test, moins solide il est.
Et attention au code caché (par exemple derrière de la configuration et donc des dépendances).
Toujours utiliser des abstractions, puis de l'inversion de dépendances.
Ne pas mocker ce qui ne nous appartient pas (je reviendrai là dessus)
How hard it is to understand the test — The fewer lines of code in the test, the more readable the test is.

How hard it is to run the test — If the test works with out-of-process dependencies, you have to spend time keeping those dependencies operational: reboot the database server, resolve network connectivity issues, and so on.


>“Push tests as _low_ as they can go for the highest return in investment and quickest feedback” Janet Gregory and Lisa Crispin

# Payez vous une cure de désintox des tests E2E

Les tests End To End sont une facilité, pas une fatalité.
Avec de la pratique et de la rigueur, on peut les limiter à un très très petit nombre et les remplacer avec une meilleure efficacité (couverture technique ET fonctionnelle améliorée) à condition de bien s'y prendre.

Il vous faut procéder par petit pas:

 ## 1er pas: vers des Tests hermétiques

Ou tests en isolation. Il y a des milliers de lectures à ce sujet, je m'y étendrais pas cette fois ci;
[Voici ce qu'en pensait un ingénieur de chez Google en 2014](
https://docs.google.com/presentation/d/15gNk21rjer3xo-b1ZqyQVGebOp_aPvHU3YH7YnOMxtE/edit?usp=sharing) .

On peut dire qu'un bon test devrait pouvoir tourner sur n'importe quelle machine sans connexion réseau. 
Oui, oui. Vous avez bien lu.

Et surtout, surtout, faites tout pour éviter le "mais ca marche sur ma machine, je comprends pas!".
Et les DevOps ne vous sauverons pas ! ^^ 
![it works on...](img/1_DPS45Tufsih-zED3To4k6g.jpeg)


 ## 2e pas: un conception objet "test oriented"

 >Si vous faites du TDD, et respectez les principes [SOLID](https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898) à la lettre, alors vous devriez automatiquement vous sentir légitimes pour dire: "le test E2E est une complète aberration, car il met à mal toutes les règles que je tente d'appliquer":
 - Single Responsibility
 - Open Close principle
- Liskov Substitution 
- Interface Segregration 
- Dependency Injection 

Pensez à ces règles dans vos tests, et effectivement, les tests E2E sont à coté de la plaque! 

> Le code de VOS tests est aussi VOTRE code. Il obéit aux même lois.

 ## 3e pas: vers une architecture "test oriented"

Et pour cela, l'architecture hexagonale a fait ces preuves. J'y reviendrai sûrement dans un prochain article.
Cet architecture préconise de mettre en place des Ports et des Adapteurs, qui permettent justement de ne pas tout tester en même temps, d'éviter les tests E2E.

## 4e pas: le métier est vérifié et codé dans des bounded contexts
Je reprends ici les termes du Domain Driven Design, car même sans faire d'Event Sourcing, DDD nous propose de découper, délimiter, responsabiliser le domaine métier et ses règles; et évidement de le découpler de tout ce qui est autour (UI, persistence, services externes, sous domaines, domaines génériques, domaines support).

# Mais comment je saurai que ca marche si je ne le vois pas de mes yeux?

Au mieux, c'est du St Thomas.
Au pire c'est un débat du même niveau que de penser que [la terre est plate](https://youtu.be/j90zyS8xvOM), parce qu'à l'oeil nu elle apparait plate. Ou remettre en question l'existence des virus.

Les tests E2E ne sont qu'une illusion, nous avons vu le problème des faux positifs et négatifs.

Pour autant les gens plongent dans l'obscurantisme quand on leur parle d'enlever les tests E2E (parce que c'est là qu'on voit) et les remplacer par des tests d'intégration (des vrais!).

Il y a toujours eu des gens pour me dire: "mais tu ne peux pas avoir de certitude à 100%". Les même ont des doutes quand on leur dit que la terre est une sphère. C'est -hélas- le même schéma de pensée.

Je ne dit pas pour autant que un test E2E est inutile. Parce que la vraie question est "que teste-t-on".
Ou plutôt :
> "Que peut-on tester?"

Si on a aucun outillage de tests efficace, alors oui il ne reste que le test E2E.
Mais vouloir tout tester avec un E2E est une perte d'argent et de temps comme je ne cesse de le répeter.

Il y a d'autres moyens de tester les choses une par une.

C'est là où [tout le monde s'embrouille sur la pyramide de tests](https://martinfowler.com/articles/practical-test-pyramid.html#TheConfusionAboutTestingTerminology) quand on lit: "_integration tests_".
Pour beaucoup, tester en intégration c'est tester tout ce qui peut s'intégrer, ensemble, en même temps. Et bim!
On revient sur du E2E.

Tout comme ceux qui ont confondu les tests E2E avec les tests de l'Interface Graphique.
Parce que c'est tellement facile (en apparence) à coder avec des outils comme Selenium ou Cypress.
Parce que justement leur architecture spaghetti, ou N-tiers ( = plat de lasagne), ou maitenant Micro Services ( = plat de raviolis) ne permet plus de séparer la UI (User Interface) d'un monstre monolythique où tout est collé bout à bout.

Pourtant, le but est de tester si les composants qui ont, par ailleurs, été testés de manière isolée, s'intègrent bien entre elles.
Une fois cela vérifié, pourquoi l'ensemble ne serait-il pas stable?
Si il reste des bugs, c'est qu'il manque des tests, tout simplement.




##  Integration ou Contrat ?

Attention, quand on parle test d'intégration, beaucoup reviennent sur l'idée de End to End; on intègre tout de bout en bout. [Il ne s'agit pas de cela!](https://blog.thecodewhisperer.com/permalink/integrated-tests-are-a-scam)
Une intégration fiable se joue autour d'un contrat fiable.
S'assurer que le contrat est respecté, DES DEUX COTES, c'est faire de l'intégration.
Il faut s'assurer de l'équivalence du contrat des 2 cotés d'un composant: fournisseur (provider) ET consommateur (consumer).

Quand on fake (ou mocke, désolé pour l'anglicisme), le test n'est valide que si le fake est valide. 
Ce qu'il faut c'est s'assurer constamment (à chaque build, à chaque intégration continue) que le contrat n'est pas rompu.
Une doublure oui, mais une doublure valide.
La bonne idée pour éviter des vérifications superflues, c'est de laisser le compilateur les faire par le typage. Un typage très fort et un respect à 300% des règles SOLID. Et ne pas utiliser les exceptions. Et suivre toute la démarche DDD.
Ce n'est qu'avec cet affort là que vos doublures seront fiables.

L'autre arme c'est le Contract Based Programming/Testing.

Il faut utiliser les deux.

Oui c'est un travail supplémentaire. Mais je ne vois pas comment l'éviter pour ne pas retomber dans le piège du E2E qui finalement est un pis-aller pour ceux qui ne prennent pas le temps de faire soit du typage fort, soit du Contract Testing ([Consumer-driven contract testing (CDC) expliqué ici](https://medium.com/typeforms-engineering-blog/contract-testing-i-e2e-testing-is-so-last-season-1142fa63c740) )




# Les bénéfices de l'abstinence

Les gens qui mettent (pardon, ils perdent) tout leur argent dans le E2E testing, sont nhélàs souvent des gens qui n'ont pas pris soin d'explorer d'autres pistes.

Et pourtant, il y a des choses bien plus profitables (rentables, messieurs les financiers) comme [le Smoke Testing, le Sanity Testing et le Regression Testing](https://www.softwaretestinghelp.com/smoke-testing-and-sanity-testing-difference/). Et ce n'est pas du tout ce que vous offrent les tests E2E pour pas cher. Cela n'a rien à voir et ce serait une fausse promesse (mais qui a la vie dure).


# Et s'il ne devait en rester qu'un (ou deux)

Et bien, un test "End to End" , bout en bout, pourrait bien s'avérer utile pour tester ce qu'on ne sait pas tester autrement, et c'est peut être justement l'intégration de l'intégration.
L'articulation ultime.
Mais je suis sûr qu'on peut le remplacer par un autre test d'intégration.

Le problème vient le plus souvent des configurations de mise en prod. Les valeurs effectives d'un système dans sa phase que tout le monde aime bien appeler "RUN". Le temps du RUN. Le Run Time (Je ne dis pas LA runtime pour de bonnes raisons).

Et là, que dois je vérifier?
Que mon système démarre bien.
C'est tout.  Derrière cela veut dire que ma config est juste et que mes systèmes sont opérationnels. Mais cela aussi je peux le surveiller ("monitorer") par d'autres tests plus unitaires.

Juste un test, un happy path. Un seul. Pour convaincre le dernier des incrédules.
Cela n'a même aucun intérêt pour l'ingénierie.
Même pas une liste "High Value Paths" comme on peut le lire [par ci](https://www.testim.io/blog/e2e-testing/), par là; parce que si vous entrez dans cette logique, vous allez en écrire autant que de Use Cases de votre métier (c'est à dire: pléthore); et je n'ai vu personne qui sache poser une limite à cela.
Alors que toute la logique devrait être dans le Domaine Métier tel que nous l'apprends DDD (voir mes articles à ce sujet).

Par contre, savoir différencier ["Smoke Tests"](https://www.softwaretestinghelp.com/smoke-testing-and-sanity-testing-difference/) des tests E2E, là oui.
Ces tests manuels ont toute leur place, et l'économie de moyens à faire en supprimant les tests E2E doit être ré-investie dans ces tests Exploratoires.

Mais cela est une autre histoire...



-----------

Références

https://www.stevesmith.tech/blog/end-to-end-testing-considered-harmful/

