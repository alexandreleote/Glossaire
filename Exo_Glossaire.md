# GLOSSAIRE

- [Général](#général)
- [Front-end](#front-end)
- [UX / UI](#ux-ui)
- [Architecture](#architecture)
- [Modélisation / Base de données](#modélisation---base-de-données)
- [Symfony](#symfony)
- [Sécurité](#sécurité)
- [RGPD](#rgpd)
- [SEO](#seo)
- [Gestion de projets / DevOps](#gestion-de-projets---devops)
- [English](#english)

## Général
1.	Quel est l’environnement à installer pour exécuter un script PHP ? Citer 2 exemples de logiciels permettant ce contexte

L'environnement à installer pour exécuter un script PHP est Apache qui permet d'interpréter ce langage. On peut installer Laragon, WAMP, XAMP pour ce contexte.
Il ne faut pas faire cohabiter deux versions de logiciels, cela créerait des conflits.
    
2.	Qu’est-ce qu’un algorithme ?

Un algorithme est une suite d'instructions données afin de résoudre un problème que l'on a posé initialement.
  
3.	Qu’est-ce qu’une variable ? Par quel symbole est préfixée une variable en PHP ?

Une variable est un espace de stockage que l'on crée afin de pouvoir y stocker une valeur numérique, une chaîne de caractères, un tableau, etc... 
Elle est symbolisée par le signe "$" que l'on écrit avant de nommer la variable.

4.	Qu’est-ce que la portée d’une variable ?

La portée d'une variable est la zone d'effet de la variable dès qu'elle est déclarée. C'est-à-dire en d'autres termes, l'impact dans la portion de code où elle est utilisée.
Elle peut être locale ou globale (cette dernière s'applique à tous les blocs de code, dont les classes).
  
5.	Qu’est-ce qu’une constante ? Quelle est la différence avec une variable ?

Une constante est un espace de mémoire dont la valeur est définie et qui ne sera pas modifiée par la suite. <br>
A l'inverse la variable est un élément de données dont la valeur évolue au cours de l'exécution d'un programme.

6.	Qu’est-ce qu’une superglobale, combien en existent-ils et donner un exemple d’utilisation

Il s'agit d'une variable prédéfinie permettant d'accéder à des données stockées à l'extérieur du programme dans lequelle la superglobale est appelée. Elle permet de récupérer des données provenant de formulaires, de cookies, de sesssions ou encore d'environnement d'exécution.<br>
Il existe neuf superglobales en PHP :<br>
<ul>
    <li><code>$GLOBALS</code> : permet de parcourir rapidement l’ensemble des variables globales définies dans un script.</li>
    function test() {<br>
    $foo = "local variable";<br>
    echo '$foo in global scope: ' . $GLOBALS["foo"] . "\n";<br>
    echo '$foo in current scope: ' . $foo . "\n"; }
    $foo = "Example content";<br>
    test();<br><br>
    <li><code>$_SERVER</code> : contient des variables définies par le serveur utilisé ainsi que des informations relatives au script.</li>
    echo $_SERVER['SERVER_NAME'];<br><br>
    <li><code>$_GET</code> : stocke les valeurs lorsque le formulaire sera envoyé via la méthode GET.</li>
    echo 'Hello ' . htmlspecialchars($_GET["name"]) . '!';<br><br>
    <li><code>$_POST</code> : stocke les valeurs lorsque le formulaire sera envoyé via la méthode POST.</li>
    echo 'Bonjour, tu t\'appelles ' .$_POST['prenom'];<br><br>
    <li><code>$_FILES</code> : contient les informations relatives aux fichiers téléchargés via un formulaire.</li>
    move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], "uploads/" . basename($_FILES["fileToUpload"]["name"]));<br><br>
    <li><code>$_COOKIE</code> : est un tableau associatif contenant les variables passées via des cookies HTTP.</li>
    setcookie("utilisateur", "Jean", time() + (86400 * 30), "/");<br>
    echo isset($_COOKIE["utilisateur"]) ? $_COOKIE["utilisateur"] : "Le cookie n'est pas défini.";<br><br>
    <li><code>$_SESSION</code> : est un tableau associatif contenant les variables de session.</li>
    session_start(); $_SESSION["utilisateur"] = "Jean";<br>
    session_start(); echo isset($_SESSION["utilisateur"]) ? $_SESSION["utilisateur"] : "Aucun utilisateur.";<br><br>
    <li><code>$_REQUEST</code> : est un tableau associatif contenant les variables de <code>$_GET</code>, <code>$_POST</code>, et <code>$_COOKIE</code>.</li>
    echo isset($_REQUEST["nom"]) ? $_REQUEST["nom"] : "Paramètre non défini.";<br><br>
    <li><code>$_ENV</code> : contient des informations liées à l'envrionnement dans lequel s'exécute le script.</li>
    $_ENV["APP_ENV"] = "production";<br>
    echo isset($_ENV["APP_ENV"]) ? $_ENV["APP_ENV"] : "Variable non définie.";<br><br>
</ul>

7.	Quels sont les différents types (primitifs) que l’on peut associer à une variable en PHP ? Les citer et en donner des exemples (ne pas oublier le type d’une variable sans valeur)

Il existe 8 types (primitifs) que l'on peut associer à une variable :
- int : entier
  
  | $age = 42;  // Type : entier<br>
  
- float : nombre décimal
  
  | $price = 19.99;  // Type : flottant<br>
  
- string : chaîne de caractères
  
  | $name = "Alexandre";  // Type : chaîne de caractères<br>
  
- bool : booléen (vrai/faux)
  
  | $isCoding = true;  // Type : booléen<br>
  
- array : tableau
  
  | $manga = array("DemonSlayer", "Shangri-La Frontier", "Solo Leveling");  // Type : tableau indexé<br>
    $personne = [
      "nom" => "Alexandre",
      "age" => 29
      ];  // Type : tableau associatif<br>
  
- object : objet
  
  | class Personne { public $nom; public $age; }<br>
    $personne = new Personne();  // Type : objet<br>
    $personne->nom = "Alice";<br>
    $personne->age = 25;<br>
  
- NULL : absence de valeur
  
  | $despair = null;  // Type : NULL<br>
  
- resource : ressource (externe)
  
  | $folder = fopen("exemple.txt", "r");  // Type : resource<br>

8.	Existe-t-il plusieurs types de tableaux en PHP, si oui lesquels ?

Il existe les tableaux associatifs et les tableaux à index numériques. <br>
Dans le premier cas, il s'agit d'un tableau dont les indices sont des chaînes de caractères.<br>
Dans le deuxième cas, il s'agit d'un tableau dont les indices sont des valeurs numériques.

9.	Quelles sont les différentes structures de contrôles qu’il existe en algorithmie ? Donner un exemple pour chacune d’entre elles

Il existe trois grandes structures de contrôles en algorithmie : les structures séquentielles, les structures conditionnelles et les structures itératives.<br><br>
Par exemple pour les *structures séquentielles*, il  s'agit d'exécuter les instructions dans l'ordre où elles apparaissent :<br>
a = 5<br>
b = 10<br>
c = a + b<br>
print(c)<br>
<br>
Pour les *structures conditionnelles*, on désire vérifier une information et retourner un résultat de manière à ce que l'information vérifiée corresponde au résultat attendu ou non:<br><br>
a = 5;<br>
if (a > 0) {<br>
    echo "a est positif";<br>
} else if (a < 0) {<br>
    echo "a est négatif"<br>
} else {<br>
    echo "a est nul" }<br>
<br>
Enfin pour les *structures itératives*, on souhaite répéter une séquence d'instructions un nombre de fois non défini jusqu'à remplir la condition.<br>
Il exsite trois types de boucles : la boucle <code>for</code>, la boucle <code>while</code> et la boucle <code>foreach</code>.<br>
<br>
Méthode <code>for</code> :<br>
for($i = 1; $i <= 10; $i++) {<br>
    echo $i." ";}<br>
<br>
Méthode <code>while</code> :<br>
$i = 1;<br>
while($i <= 10) {<br>
    echo $i." ";<br>
    $i++;}<br>
<br>
Méthode <code>foreach</code> :<br>
$range = range(1,10);<br>
var_dump($range);<br>
<br>
foreach(range(1,10) as $v) {<br>
    echo $v." ";}<br>


10.	Quelle est la fonction PHP permettant de demander la longueur d’une chaîne de caractères ?

La fonction PHP strlen() permet de demander la longueur de d'une chaîne de caractères.

11.	Qu’est-ce qu’une session ? Quelle fonction permet de démarrer une session en PHP ? Donner un exemple d’utilisation en PHP

Une session correspond à la façon de stocker des données de chaque utilisateur par l'intermédiaire d'un identifiant de session unique. De sorte à ce que les données soient envoyées à l'utilisateur correspondant et non une personne tierce.<br>
L'utilisateur n'a accès à ses informations que si sa « session » est démarrée.<br>
<br>
Pour démarrer une session en PHP, la fonction <code>session_start()</code> est appelée. La sessions est alors en cours tout le temps où l'utilisateur reste sur la ou les pages en relation. Habituellement, elle se ferme dès lors que l'utilisateur ferme son navigateur (sauf si l'utilisateur se déconnecte via la fonction prévue à cet effet ou s'il prolonge la session via un cookie).

12.	Qu’est-ce qu’un cookie ? Donner un exemple d’utilisation en PHP

Un cookie est un fichier stocké côté client au sein de son navigateur. Ces cookies servent à garder en mémoire les préférences d'utilisation de l'utilisateur entre les visites d'une page ou d'un site web.<br>
Ces fichiers contiennent des données pouvant être des informations de session, des identifiants, des paramètres de navigation, etc. Leur durée de vie est généralement définie de sorte qu'ils soient utiles et par la suite supprimés automatiquement si nécessaire.<br>
<br>
Lorsque l'on navigue sur un site web, ce dernier peut enregistrer nos idenfiants de connexion afin de ne pas perdre de temps à rentrer à nouveau les informations. Cela facilite l'expérience utilisateur et permet également de garder en mémoire le nom de celui-ci, si l'on associe son idenfiant au nom renseigné.

13.	Quelle est la différence entre les instructions « require » et « include » en PHP

Les deux instructions vont permettre de charger des fichiers PHP. La différence réside dans le comportement de chacune des instructions si le fichier demandé n'existe pas.<br>
En effet, « include » va relever l'erreur sans compromettre la suite du code et ainsi laisser le programmer s'exécuter. A l'inverse, « require » va relever l'erreur et stoppera le script.<br>

14.	Comment effectuer une redirection en PHP ?

Pour effectuer une redirection en PHP, on utilise la fonction <code>header()</code> en indiquant la page où sera redirigé l'utilisateur.
Exemple : 

<code>header('Location: http://www.votresite.com/pageprotegee.php');<br>
exit();</code>

15.	Définir la partie « front-end » et « back-end » d’une application

La partie « front-end » correspond à l'ensemble des productions qu'un utilisateur pourra voir et aura la possibilité d'intéragir avec. Il s'agirait par exemple de l'espace d'un magasin dans lequel le client peut sa balader (zones prévues à cet effet).<br>
Pour la partie « back-end », il s'agit des données dont l'utilisateur n'est pas censé avoir accès. Il s'agit de l'ensemble du code permettant le fonctionnement du site et de récupérer les données stockées en base de données. Par exemple, il s'agit de ce qu'il se passe derrière le comptoir d'une boutique ou ce que l'on appelle l'arrière-boutique.<br>

16.	Définir le contrôle de version ? Qu’est-ce que Git ?

Le contrôle de version est la pratique qui consiste à suivre et gérer les changements apportés au code d'un logiciel. Ainsi, cela permet aux différents intervenants de l'équipe de développement de gérer les changements au fil du temps.
De plus, le contrôle de version permet un suivi intelligent et clair dans les modifications apportées au code.

Git est un système permettant le contrôle de version permettant de gérer les versions localement (chaque utilisateur a une copie de l'historique du projet). Il permet également de créer des branches afin de ne pas altérer le code source mais de vérifier une fonctionnalité avant da la fusionner (merge) à la branche principale (main/master).
De plus, il propose un suivi des moficiations de façon à ce que les développeurs voient les différences apportées entre les commits (qui, quoi, quand). On peut collaborer via des dépôts à distance (remote repositroies)

17.	Qu’est-ce qu’un CMS ? Citer au moins 2 exemples

Un CMS est un acronyme désignant un système de gestion de contenu : Content Management System. Ce logiciel en ligne permet à ses utilisateurs de créer, gérer et modifier facilment un site web sans nécessairement avoir besoin de connaissances techniques dans les langages utilisés (HTML, CSS, JS, PHP). WordPress est un CMS reconnu, OpenSource, disposant d'un grand choix de template pour créer son site. Au départ créé pour repondre à l'engouement des blogs, aujourd'hui il s'agit d'un pilier de la création de site web pour les personnes souhaitant avoir une vitrine sans pour autant suivre une formation de développeur web. D'autres CMS connus sont : Drupal, PrestaShop pour les e-commerces, Magento, etc...

## Front-end
18.	Définir HTML

HTML est l'acronyme pour «HyperText Markup language», que nous pouvons traduire en français par «langage de balises pour l'hypertexte».
Ce langage est utilisé pour concevoir et représenter le contenu d'une page web ainsi que son squelette (structure).

19.	Définir CSS

CSS est l'acronyme pour « Cascading Style Sheet s» ou en français « feuilles de style en cascade ». Ce langage est utilisé pour décrire la présenationt d'un document écrit en HTML ou XML. <br>
Ce langage de programmation décrit la façon dont les éléments doivent être affichés à l'écran, sur papier, à l'oral ou sur d'autres médias.
Autrement dit, le CSS est le langage qui habille le site web codé en HTML.

20.	Définir Javascript

Le JavaScript, à ne pas confondre avec le Java qui est un autre langage, est un langage de script léger, orienté objet, principalement connu comme le langage de script des pages web.
Si on devait définir l'importance du JavaScript (abrégé en « JS »), on pourrait dire que l'HTML est la carrosserie d'une voiture, le CSS la couleur de celle-ci et le JS le moteur qui fait avancer la voiture.

21.	Définir JSON. Dans quel contexte ce format est-il utilisé ? 

JSON est l'acronyme pour JavaScript Object Notation, qui est un format de fichier permettant d'échanger des données entre plusieurs pages.<br>
On s'en sert stocker des données de manière hiérarchique. On peut alors créer des collection de paires "nom" : "valeur" pouvant alors donner lieu à des objet, enregistrement, dictionnaire, liste à clé ou tableau associatif.<br>
On peut utiliser le JSON dans plusieurs cas, dans les APIs REST ou web plus globalement, dans les fichiers de configuration ou encore dans les 'bundles' que l'on trouve dans Symfony par exemple.

22.	Peut-on interpréter du Javascript côté serveur ? Si oui, comment ?

On peut interpréter du Javascript coté serveur notamment grâce à un environnement d'exécution : Node.JS.
La manière dont cela s'opère est de manière asynchrone, c'est-à-dire que les requêtes seront envoyées mais n'interrompent pas le programme. La réponse sera alors traitée lorsqu'elle sera retournée.
Ainsi, on rend notre code non bloquant dans son usage en évitant de bloquer notre application monothread durant l'exécution de la requête.

23.	Qu’est-ce qu’un sélecteur CSS ?

Un sélecteur CSS est un élément qui cible une balise HTML pour en modifier les propriétés. On peut cibler une balise <body> qui altèrera le corps du site.
Si l'on attribue à cette balise un ID ou une CLASS, alors on peut modifier certains aspects de façon individuelles ou multiples.

24.	Quelle balise HTML permet de créer un lien hypertexte ?

La balise <a> avec l'attribut href permet de créer un lien hypertexte. Par exemple un lien pour revenir à la page index : *a href="index.html"* entre <> pour qu'elle soit effective.

25.	Qu’est-ce qu’une requête AJAX ?

L'AJAX est une technique de développement web permettant d'actualiser une partie d'une page sans devoir en recharger tout le contenu.
Acronyme d'Asynchronous Javascript And Xml : l'AJAX est apparu en 1998 mais dont l'usage a été démocratisé que bien plus tard grâce en partie à la bibliothèque open source jQuery ayant intégré cette fonctionnalité.
Ainsi on peut soumettre des formaulaires sans recharger la page, afficher des propositions dans un champ de recherche lorsqu'on tape les premiers caractères, effectuer une requête en base de données pour mettre à jour un bloc d'une page, consommer une API externe de façon asynchrone au chargement de la page sur une action utilisateur.

26.	Quel sélecteur CSS permet de sélectionner tous les éléments d’une classe spécifique ? D’un identifiant spécifique ?

Le sélecteur CSS qui permet de sélectionner tous les éléments est *. <br>
Pour une classe cela donne : .class{ } <br>
Pour un identifiant spécifique : #id{ } 

27.	Définir le responsive design

Il s'agit de rendre un site web adapté et accessible à tous les supports (devices) possibles : ordinateurs, smartphones, tablettes, etc.
Cela s'effectue à la fois avec la programmation HTML et le style CSS 

28.	Qu’est-ce que le templating ?

Le templating est un moyen d'insérer une structure HTML au travers d'un id. Ceci est ignoré du DOM, il ne sera pas interprété et le CSS ne serait pas appliqué.

29.	Qu’est-ce qu’une fonction anonyme en Javascript ?
30.	Quelle méthode JavaScript est utilisée pour ajouter un élément à la fin d'un tableau ?

Pour ajouter un élément à la fin d'un tableau, on utilise la méthode <code>push()</code> en ciblant le tableau correctement.
Exemple :

const animals = ['pigs', 'goats', 'sheep'];

const count = animals.push('cows');
console.log(count);
// Expected output: 4
console.log(animals);
// Expected output: Array ["pigs", "goats", "sheep", "cows"]

animals.push('chickens', 'cats', 'dogs');
console.log(animals);
// Expected output: Array ["pigs", "goats", "sheep", "cows", "chickens", "cats", "dogs"]

31.	Qu’est-ce qu’un « media query » ?

Un « media query » est une fonction en CSS permettant de définir le comportement de certains éléments, classes ou ids en fonction de paramètres définis par le concepteur. <br>
Par exemple, on peut définir la taille minimale d'un écran et la taille maximale dans lesquelles le comportement de ces éléments agissent d'une manière définie, on peut penser au responsive design sur mobile et tablettes qui diffère du format desktop.<br>
Ainsi, on peut favoriser les performances d'affichage de ces éléments et l'adapter au format pour rendre l'expérience utilisateur optimale.

32.	Qu’est-ce qu’un pseudo élément en CSS ?

Un pseudo élément en CSS est une fonction permettant de styliser des parties définies d'un élément HTML. Par exemple, pour modifier le surlignage de son texte sur son site web pour ne pas garder celui de base (de couleur bleue), il faut alors écrire dans son CSS ceci : <br>
<code>::selection {
    background-color: black;<br>
    color: white; }</code><br>
Ainsi on remplace la couleur bleue initiale de la fonction de surlignage en une couleur noire et en changement également la couleur du texte pour s'assurer de la lisibilité. Il faut ajouter -moz- pour définir cela sur les navigateurs mozilla également sinon on perd notre effet et altère l'expérience utilisateur.

33.	Qu’est-ce que Bootstrap ? Donner d’autres exemples équivalent

Bootstrap est un framework frontend OpenSource permettant de faciliter les modifications de style CSS de sites web responsives en utilisant des classes prédéfinies à intégrer à son code HTML. D'autres framework tels que Tailwind CSS ou Semantic UI, et d'autres encore, sont capables d'en faire autant avec chacun leurs avantages. Tailwind CSS va se concentrer sur des classes précises plutôt que des composants prédéfinis afin de créer des interfaces détaillées sur mesure.

34.	Quand un formulaire HTML est créé, quelles sont les 2 méthodes qui peuvent lui être associées ? Donner la différence entre ces 2 méthodes

Les deux méthodes qui peuvent lui être associées sont la méthode "POST" et la méthode "GET".
La première envoie les informations renseignées dans le formulaire à l'URL définie dans l'action du formulaire. Les données ne seront pas visibles directement dans l'URL.
Avec la méthode "GET", les données seront visibles dans l'URL en tant que paramètres après le point d'interrogation.

## UX UI
35.	Quelle est la différence entre UX Design et UI Design ?

L'UX Design désigne l'expérience utilisateur (User eXperience), il s'agit de ce qui est permis de faire à l'utilisateur sur un site, une application mobile ou un logiciel. <br>
L'UI Design désigne quant à lui l'interface utilisateur (User Interface), cela implique les fenêtres, boutons, liens et tous les éléments visuels et textuels.

36.	Qu’est-ce qu’un wireframe ? 

Le wireframe est une maquette fonctionnelle, un schéma permettant de définir les éléments et composants essentiels que la maquette doit contenir. IL s'agit d'un squelette pour la conception de l'application, le site ou logiciel. 

37.	Qu’est-ce qu’un prototype ? 

On entend par prototype, une première version d'un site ou une application simulant son interface et ses fonctionnalités. On peut alors tester si les fonctions pensées et crées sont validées ou à revoir. Un prototype peut être plus ou moins fonctionnel à savoir s'il s'agit d'une maquette papier, interactive ou d'une application déjà construite.

38.	Qu’est-ce que la hiérarchie visuelle en UI Design ?

La hiérarchie visuelle permet de valoriser les éléments graphiques importants tels que la taille, la couleur et la forme qui sont utilisés pour regrouper de manière logique les informations et guider l'oeil de l'utilisateur sur le site / l'application.

39.	Qu’est-ce que l’accessibilité en UX Design ? 

Il s'agit de permettre à tout un chacun, quelque ce soit son handicap ou non handicap, de profiter pleinement de l'application ou site web. Il est important de permettre aux personnes en situation de handicap d'accéder aux informations au travers du numérique dans une démarche adaptée et facilité leur expérience utilisateur.

40.	Qu’est-ce qu’une grille de mise en page ?

Il s'agit d'un calque qui permet d'agencer les éléments pour qu'ils soient affichés de manière harmonieuse à l'écran.
De sorte qu'il puisse voir lors du maquettage le comportement des différents éléments (image, bloc texte, bouton) et anticiper des modifications suivant la taille de certains écrans ou pour permettre un affichage spécifique qui sied à l'information affichée.<br>
Ainsi on rexpecte la cohérence visuelle, la lisibilité dans la navigation, l'efficacité et la rapidité ainsi que l'adaptabilité. Il s'agit d'un outil important lors de la conception des interfaces afin qu'elles soient esthétiques, organisées et intuitives.

41.	Qu’est-ce que la notion d’affordance en UX Design ?

L'affordance en UX Design est le principe dans lequel l'utilisateur évolue de manière intuitive sur une page web. Cette manière est dictée subtilement par les éléments auxquels l'utilisateur fait face : les boutons, les images, les liens...<br>
Dans le développement d'une site web, nous allons respecter certaines règles de bienséance du développement afin de ne pas perturber l'utilisateur dans sa découverte et lui permettre de naviguer sur le site la première fois comme s'il l'avait déjà fait auparavant.<br>
Le tout est de fluidifier son expérience de sorte à ce qu'il revienne ou reste sur le site un maximum de temps et de fois.

42.	Qu’est-ce qu’un « mobile first design » ?

Le "mobile first design" consiste à partir de l'affichage mobile en le rendant pertinent et fonctionnel pour ensuite développer les tailles d'écrans plus grandes en modifiant les différents éléments.<br>
Le but étant de ne pas supprimer d'éléments mais d'en ajouter ou de les déplacer de sorte que le site soit performant et adapté au format mobile.

## Programmation orientée objet (POO)
43.	Donner une définition de la programmation orientée objet 

La programmation orientée objet est la manière de concevoir son code en bloc contenant des variables, fonctions et contantes permettant la création d'objets. Ceci dans le but de construire et organiser son code autrement que de manière procédurale.

44.	Qu’est-ce qu’une classe ? Comment la déclare-t-on ?

Une classe permet d'instancier un objet. Autrement il s'agit du paramétrage de ce dernier avant de le concevoir. La classe est constituée d'attributs qui définissent l'objet qui sera instancié.<br>
On déclare la classe comme suit : <code>Class NomDeLaClasse {}</code>

45.	Qu’est-ce qu’un objet ?

Un objet est un élément possédant des caractéristiques qui lui sont propres et définies en amont. Il s'agit de caractéristiques physiques le rendant tangible. (On ne parle pas de son usage)

46.	Définir la notion de propriété / attribut / méthode

En POO, une propriété consiste en une variable définie au sein d'une classe lors de la création d'un objet. Cette variable n'aura pas de valeur qui lui sera donnée mais elle possédera un mot-clé en préfixe :
 public $user_name;
De sorte en ajoutant le mot-clé public, on définit son accessibilité depuis l'extérieur de la classe. Donc on pourra récupérer les informations qu'elle contiendra même si on ne se trouve pas dans l'élément qui la gère directement.

Un attribut est une caractéristique de la classe, synonyme de propriété elle désigne les informations stockées. Par exemple, pour un ordinateur, il s'agira de la carte mère, la RAM, etc.

Une méthode consiste en ne action applicable à l'objet. Une action entraine un résultat à la fin de la programmation qui peut être séquentielle, itérative ou conditionnelle.


47.	Qu’est-ce que la visibilité d’une propriété ou d’une méthode ? Citer les différents types de visibilité
48.	Quelle est la méthode spécifique utilisée pour créer un nouvel objet à partir d’une classe ?
49.	Qu’est-ce que l’encapsulation ?

L'encapsulation consiste à regrouper des données au sein d'une même unité. Ceci de manière à protéger les données contre l'extérieur. On définit les niveaux d'accès aux données suivant des mots-clés <code>public</code>, <code>private</code> et <code>protected</code>.<br> 

50.	Que signifie « étendre une classe » ? Quelle est le concept clé mis en œuvre ? Donner un exemple
51.	Définir l’opérateur de résolution de portée
52.	Définir une méthode / propriété statique
53.	Définir le polymorphisme en POO
54.	Définir une méthode / classe abstraite ?
55.	Définir le chaînage de méthodes

Le chaînage de méthodes consiste à agir sur plusieurs classes d'un objet en une instruction.

Exemple :

<code>$objet->methode1()->methode2()</code>

56.	Qu’est-ce que la méthode __toString() ? Existe-t-il d’autres méthodes « magiques »
57.	Qu’est-ce qu’un « autoload » ?
58.	Comment appelle-t-on en français les « getters » et les « setters » ?

On appelle en français les accesseurs pour les "getters" et les mutateurs pour les "setters". Le but pour les accesseurs est de récupérer les informations et pour les mutateurs de les modifier selon l'instruction programmée.

59.	Qu’est-ce que la sérialisation en PHP ? 

## Architecture 
60.	Qu’est-ce que l’architecture client / serveur ? Grâce à quel type de requête peut-on interroger le serveur. Définir l’acronyme de ce type de requête. Si on ajoute un « S » à cet acronyme, expliquer la différence
61.	Donner la définition d’un design pattern. Citer au moins 3 exemples de design pattern

Le design pattern (patron de conception) est un élément important en POO : il a pour but de répondre à un problème technique avec une infrastructure logicielle faite de quelques classes.
- Le modèle composite, qui sert à mettre en œuvre une structure arborescente. Il peut s’agir de la représentation d’un dossier avec ses sous-dossiers et les fichiers qu’on y trouve. Les feuilles et les composites suivent un modèle qui fait appel à la même interface logicielle. La manipulation est la même à chaque utilisation.
- Un autre modèle important est le singleton. Il limite l’instanciation d’une classe à un seul objet. Il est utilisé pour qu’un seul objet coordonne les opérations à l’intérieur d’un système donné. Il est surtout utilisé pour un système plus rapide ou qui occupe moins de mémoire. Il s’agit aussi d’un système avec peu d’objets. Les itérateurs et les adaptateurs comptent aussi parmi les principaux modèles de design pattern.
- Fabrique est un patron de conception de création qui définit une interface pour créer des objets dans une classe mère, mais délègue le choix des types d’objets à créer aux sous-classes.

62.	Qu’est-ce que l’architecture MVC ?

L'architecture MVC est un design pattern utilisé lors de la conception d'un site internet. Il est constitué de trois modules constituant l'acronyme : Modèle-Vue-Contrôleur. Le but est de séparer les modules dans leur fonctionnement et qu'ils remplissent des rôles spécifiques tout en communicant entre eux.

<ul>
    <li>modèle : données (accès et mise à jour)</li>
    <li>vue : interface utilisateur (entrées et sorties)</li>
    <li>contrôleur : gestion des événements et synchronisation</li>
</ul>

63.	Quel est le rôle de chaque couche du design pattern MVC : Model, View, Controller ?

Afin d'être plus précis, le Modèle est la couche traitant directement avec la base de données en préparant les requêtes SQL qui lui seront envoyées.
Le Controller se charge quant à lui de répondre aux actions de l'utilisateur sur la couche View. Ainsi, il transmet l'information au Modèle avant de remonter l'information à la View. Le Controller sert à gérer les demandes et contrôler ce qui est renvoyé également avant que les informations ne soient affichées sur la View.

64.	Quels sont les avantages de l’architecture MVC ?
65.	Existe-t-il des variantes à l’architecture MVC ?
66.	Qu’est-ce qu’une API ? Définir l’architecture REST

Une API vient de l'acronyme Application Programming Interface et permet à une application de récupérer des données d'un service tiers.
Par exemple : une API web peut être utilisée pour interagir avec une base de données ou un service distant via des requêtes HTTP (GET, POST, etc.).

## Modélisation - Base de données
67.	Qu’est-ce que la modélisation de données ? Définir la méthode Merise
68.	Quelles sont les 3 étapes principales de la méthode Merise ? 
a.	Analyse, conception et réalisation
b.	Planification, exécution et contrôle
c.	Création, modification et suppression
69.	Qu’est-ce qu’un modèle conceptuel de données (MCD) en Merise ?
70.	Qu’est-ce qu’un modèle logique de données (MLD) en Merise ?
71.	Donner la définition des mots suivants :
a.	Entité
b.	Relation
c.	Cardinalité
d.	Clé primaire / clé étrangère
72.	Que devient une relation de type « Many To Many » dans le modèle logique de données ?
73.	Qu’est-ce qu’une base de données ?
74.	Définir les notions suivantes : 
a.	SQL
b.	MySQL
c.	SGBD (donner 2 exemples de SGBD)
75.	Dans une base de données, les données sont stockées dans des ___. Celles-ci sont constituées de lignes appelées ___ et de colonnes appelées ___
76.	Quelle est la différence entre une base de données relationnelle et non relationnelle ?
77.	Qu’est-ce qu’une jointure dans une base de données ? En existe-t-il plusieurs ? Si oui lesquelles ?
78.	A quoi sert une vue dans une base de données ?
79.	Qu’est-ce que l’intégrité référentielle dans une base de données ?
80.	Quelles sont les fonctions d’agrégation en SQL ?
81.	Qu’est-ce qu’un CRUD dans le contexte d’une base de données ?
82.	Quelles sont les clauses qui permettent de :
a.	Insérer un nouvel enregistrement dans une table
b.	Modifier un enregistrement dans une table
c.	Supprimer un enregistrement dans une table
d.	Supprimer la base de données
e.	Filtrer les résultats d’une requête SQL
f.	Trier les résultats d’une requête SELECT
g.	Regrouper les résultats d'une requête SELECT en fonction d'une colonne spécifique
h.	Concaténer 2 chaînes de caractères 
83.	Comment se connecter à une base de données en PHP ? Quelle est la classe native utilisée ?

## Symfony
84.	Qu’est-ce que Symfony ?
85.	Sur quel langage de programmation et design pattern repose Symfony ? 
86.	Quelle est la dernière version en date de Symfony ?
87.	Qu’est-ce qu’un bundle ? 
88.	Quel est le moteur de template utilisé par défaut dans Symfony ?
89.	Qu’est-ce qu’un ORM ? Quel est son utilité et comment s’appelle-t-il au sein de Symfony ?
90.	Qu’est-ce que l’injection de dépendances ? Quel est l’outil utilisé dans ce contexte et quel fichier contient l’intégralité des dépendances du projet ?
91.	Que permet le bundle Maker au sein de Symfony ? 
92.	Quel est le langage de requêtage exploité au sein d’un projet Symfony ?
93.	Quel est le composant qui garantit l’authentification et l’autorisation des utilisateurs ?

## Sécurité
94.	Qu’est-ce que l’injection SQL ? Comment s’en prémunir ?
95.	Qu’est-ce que la faille XSS ? Comment s’en prémunir ?
96.	Qu’est-ce que la faille CSRF ? Comment s’en prémunir ?
97.	Définir l’attaque par force brute et l’attaque par dictionnaire
98.	Existe-t-il d’autres failles de sécurité ? Citer celles-ci et expliquer simplement leur comportement
99.	A quoi servent l’authentification et l’autorisation dans un contexte d’application web ?
100.	Définir la notion de hachage d’un mot de passe et citer des algorithmes de hachage
101.	Qu’est-ce qu’une politique de mots de passe forts ?
102.	Qu’est-ce que l’hameçonnage ?
103.	Définir la « validation des entrées »


## RGPD
104.	Qu’est-ce que le RGPD ?
      
Le RGPD est l'acronyme de «Règlement Général de Protection des Données» en français. En anglais, cet acronyme sera écrit GDPR "General Data Protection Regulation".

105.	Quel est son objectif principal ?
106.	Quelle est la date d’entrée en vigueur du RGPD ?

Le RGPD est entré en vigueur le 24 mai 2016 et s'applique depuis le 25 mai 2018.

107.	Quelles sont les sanctions possibles en cas de non-respect du RGPD ?
108.	En France, quel est l’autorité administrative qui s’occupe de faire appliquer le RGPD ?
109.	Quel est le consentement valide selon le RPGD ?
110.	Qu’est-ce qu’une politique de confidentialité ?
111.	Quelle est la durée de conservation maximale des données personnelles selon le RGPD ?
112.	Quels sont les droits des utilisateurs selon le RGPD ?
113.	Qu’est-ce que le principe de minimisation des données selon le RGPD ?

## SEO
114.	Qu’est-ce que le SEO ? 
115.	Quel est l’objectif principal du SEO ?
116.	Existe-t-il plusieurs types de référencement ? Lesquels ?
117.	Qu’est-ce que la densité de mots-clés en SEO ?
118.	Qu’est-ce qu’un attribut « alt » ?

Un attribut « alt » en HTML permet de donner une description textuelle à une image. Le terme désiné texte alternatif, alternatif dans le cas où l'utilisateur ne pourrait pas accéder à l'image visuellement ou serait dans l'incapacité de voir l'image.
De ce fait, en donnant une description dans une chaine de caractères à l'attribut alt d'une image, on rend possible la retranscripption vocale du texte permettant à l'utilisateur de comprendre l'élément que l'on a intégré dans notre site internet.

119.	Qu’est-ce que la balise « meta description » ?
120.	Qu’est-ce que le « nofollow » en SEO ?
121.	Quelle est l'importance du contenu de qualité pour le référencement d'un site web ?
122.	Pourquoi est-il important d'utiliser des balises de titre (h1, h2, h3, etc.) de manière structurée ?
123.	Quelle est la recommandation pour les URL d'un site web bien référencé ?
124.	Qu'est-ce que le maillage interne et pourquoi est-il important pour le référencement ?
125.	Qu'est-ce que l'optimisation des images pour le référencement ?
126.	Qu'est-ce qu'un plan de site (sitemap) et pourquoi est-il important pour le référencement ?

## Gestion de projets - DevOps
127.	Qu’est-ce que la gestion de projet ?	
128.	Qu’est-ce qu’une méthode Agile de gestion de projet ? 
129.	Expliquer la méthode MoSCoW en quelques lignes et citer ses avantages
130.	A quoi sert la méthodologie MVP ? Citer les caractéristiques clés
131.	Qu’est-ce que la planification itérative ?
132.	Citer 3 méthodes Agiles dans le cadre d’un projet informatique
133.	Qu’est-ce qu’une réunion de revue de projet ?
134.	Qu’est-ce qu’un livrable dans un projet ? 
135.	Quels sont les 3 piliers SCRUM ? Définir chacun d’entre eux
136.	Qu’est-ce que le DevOps et quel est son objectif principal ?
137.	Qu’est-ce que l’intégration continue ? 
138.	Qu’est-ce que Docker ? Et en quoi est-il utile dans le cadre du DevOps ?
139.	Qu’est-ce qu’un test unitaire ? 
140.	Quelle est l'unité de code testée lors d'un test unitaire ?
141.	Quelles sont les caractéristiques d'un bon test unitaire ?
142.	Qu'est-ce qu'une assertion dans un test unitaire ?
 
## English
1)	What does JavaScript enable you to do on a website ?
a.	Add interactive behavior and dynamic content
b.	Define the layout and design of web pages
c.	Handle server-side operations
2)	Which programming language is primarily used for server-side web development ?
a.	PHP
b.	JavaScript
c.	HTML
3)	What is the purpose of a web browser ?
a.	To render and display web pages
b.	To execute serve-side code
c.	To manage databases
4)	What is the difference between GET and POST methods in HTTP ?
a.	GET retrieves data from a server, while POST submits data to a server
b.	GET submits data to a server, while POST retrieves data from a server
c.	GET and POST methods are interchangeable
5)	What is the purpose of version control systems (e.g., Git) in web development ?
a.	To track changes and manage collaborative development
b.	To optimize website loading speed
c.	To handle server-side scripting
6)	What is the purpose of a framework in web development ?
a.	To provide a structured environment for building web applications
b.	To handle network protocols and data transfer
c.	To create visual designs and layouts for websites
7)	What does NoSQL stand for ?
a.	Not Only SQL
b.	Non-Structured Query Language
c.	New Object-Oriented Language
8)	Which of the following is a characteristic of NoSQL databases ?
a.	Strict schema enforcement
b.	Support for complex transactions
c.	Scalability and flexible data models
