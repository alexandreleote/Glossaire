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
1. Quel est l'environnement à installer pour exécuter un script PHP ? Citer 2 exemples de logiciels permettant ce contexte

L'environnement à installer pour exécuter un script PHP est Apache qui permet d'interpréter ce langage. On peut installer Laragon, WAMP, XAMPP pour ce contexte.
Il ne faut pas faire cohabiter deux versions de logiciels, cela créerait des conflits.
    
2. Qu'est-ce qu'un algorithme ?

Un algorithme est une suite d'instructions données afin de résoudre un problème que l'on a posé initialement.
  
3. Qu'est-ce qu'une variable ? Par quel symbole est préfixée une variable en PHP ?

Une variable est un espace de stockage que l'on crée afin de pouvoir y stocker une valeur numérique, une chaîne de caractères, un tableau, etc. 
Elle est symbolisée par le signe `$` que l'on écrit avant de nommer la variable.

4. Qu'est-ce que la portée d'une variable ?

La portée d'une variable est la zone d'effet de la variable dès qu'elle est déclarée. C'est-à-dire en d'autres termes, l'impact dans la portion de code où elle est utilisée.
Elle peut être locale ou globale (cette dernière s'applique à tous les blocs de code, dont les classes).
  
5. Qu'est-ce qu'une constante ? Quelle est la différence avec une variable ?

Une constante est un espace de mémoire dont la valeur est définie et qui ne sera pas modifiée par la suite.  
À l'inverse, la variable est un élément de données dont la valeur évolue au cours de l'exécution d'un programme.

6. Qu'est-ce qu'une superglobale, combien en existent-ils et donner un exemple d'utilisation

Il s'agit d'une variable prédéfinie permettant d'accéder à des données stockées à l'extérieur du programme dans lequel la superglobale est appelée. Elle permet de récupérer des données provenant de formulaires, de cookies, de sessions ou encore d'environnement d'exécution.

Il existe neuf superglobales en PHP :

- `$GLOBALS` : permet de parcourir rapidement l'ensemble des variables globales définies dans un script.
```php
function test() {
    $foo = "local variable";
    echo '$foo in global scope: ' . $GLOBALS["foo"] . "\n";
    echo '$foo in current scope: ' . $foo . "\n";
}
$foo = "Example content";
test();
```

- `$_SERVER` : contient des variables définies par le serveur utilisé ainsi que des informations relatives au script.
```php
echo $_SERVER['SERVER_NAME'];
```

- `$_GET` : stocke les valeurs lorsque le formulaire sera envoyé via la méthode GET.
```php
echo 'Hello ' . htmlspecialchars($_GET["name"]) . '!';
```

- `$_POST` : stocke les valeurs lorsque le formulaire sera envoyé via la méthode POST.
```php
echo 'Bonjour, tu t\'appelles ' . $_POST['prenom'];
```

- `$_FILES` : contient les informations relatives aux fichiers téléchargés via un formulaire.
```php
move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], "uploads/" . basename($_FILES["fileToUpload"]["name"]));
```

- `$_COOKIE` : est un tableau associatif contenant les variables passées via des cookies HTTP.
```php
setcookie("utilisateur", "Jean", time() + (86400 * 30), "/");
echo isset($_COOKIE["utilisateur"]) ? $_COOKIE["utilisateur"] : "Le cookie n'est pas défini.";
```

- `$_SESSION` : est un tableau associatif contenant les variables de session.
```php
session_start();
$_SESSION["utilisateur"] = "Jean";
echo isset($_SESSION["utilisateur"]) ? $_SESSION["utilisateur"] : "Aucun utilisateur.";
```

- `$_REQUEST` : est un tableau associatif contenant les variables de `$_GET`, `$_POST`, et `$_COOKIE`.
```php
echo isset($_REQUEST["nom"]) ? $_REQUEST["nom"] : "Paramètre non défini.";
```

- `$_ENV` : contient des informations liées à l'environnement dans lequel s'exécute le script.
```php
$_ENV["APP_ENV"] = "production";
echo isset($_ENV["APP_ENV"]) ? $_ENV["APP_ENV"] : "Variable non définie.";
```

7. Quels sont les différents types (primitifs) que l'on peut associer à une variable en PHP ? Les citer et en donner des exemples (ne pas oublier le type d'une variable sans valeur)

Il existe 8 types (primitifs) que l'on peut associer à une variable :

- `int` : entier
```php
$age = 42;  // Type : entier
```

- `float` : nombre décimal
```php
$price = 19.99;  // Type : flottant
```

- `string` : chaîne de caractères
```php
$name = "Alexandre";  // Type : chaîne de caractères
```

- `bool` : booléen (vrai/faux)
```php
$isCoding = true;  // Type : booléen
```

- `array` : tableau
```php
$manga = array("DemonSlayer", "Shangri-La Frontier", "Solo Leveling");  // Type : tableau indexé
$personne = [
    "nom" => "Alexandre",
    "age" => 29
];  // Type : tableau associatif
```

- `object` : objet
```php
class Personne {
    public $nom;
    public $age;
}
$personne = new Personne();  // Type : objet
$personne->nom = "Alice";
$personne->age = 25;
```

- `NULL` : absence de valeur
```php
$despair = null;  // Type : NULL
```

- `resource` : ressource (externe)
```php
$folder = fopen("exemple.txt", "r");  // Type : resource
```

8. Existe-t-il plusieurs types de tableaux en PHP, si oui lesquels ?

Il existe les tableaux associatifs et les tableaux à index numériques.  
Dans le premier cas, il s'agit d'un tableau dont les indices sont des chaînes de caractères.  
Dans le deuxième cas, il s'agit d'un tableau dont les indices sont des valeurs numériques.

9.	Quelles sont les différentes structures de contrôles qu’il existe en algorithmie ? Donner un exemple pour chacune d’entre elles

Il existe trois grandes structures de contrôles en algorithmie : les structures séquentielles, les structures conditionnelles et les structures itératives.


**1. Programmation séquentielle**
- Les instructions sont exécutées les unes après les autres, dans un ordre prédéfini
- Chaque instruction est traitée séquentiellement, de haut en bas
- Exemple en JavaScript :
```javascript
// Instructions exécutées dans l'ordre
console.log("Première étape");
let x = 5;
let y = x * 2;
console.log("Deuxième étape");
```

**2. Programmation conditionnelle**
- Utilise des structures de contrôle pour prendre des décisions
- Les instructions sont exécutées uniquement si certaines conditions sont remplies
- Mots-clés principaux : `if`, `else`, `elseif`
- Exemple en PHP :
```php
$age = 18;
if ($age < 18) {
    echo "Mineur";
} elseif ($age == 18) {
    echo "Tout juste majeur";
} else {
    echo "Majeur";
}
```

**3. Programmation itérative**
- Permet de répéter un bloc de code plusieurs fois
- Utilise des boucles (`for`, `while`)
- Idéal pour traiter des collections ou répéter des actions
- Exemples en JavaScript et PHP :
```javascript
// Boucle for en JavaScript
for (let i = 0; i < 5; i++) {
    console.log(`Itération ${i}`);
}

// Boucle while en JavaScript
let compteur = 0;
while (compteur < 3) {
    console.log(`Compteur : ${compteur}`);
    compteur++;
}
```

```php
// Boucle for en PHP
for ($i = 1; $i <= 5; $i++) {
    echo "Itération $i ";
}

// Boucle while en PHP
$compteur = 0;
while ($compteur < 3) {
    echo "Compteur : $compteur ";
    $compteur++;
}
```

**Caractéristiques principales :**
- Séquentielle : ordre strict, pas de saut
- Conditionnelle : décisions basées sur des conditions
- Itérative : répétition de blocs de code

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
Si l'on attribue à cette balise un ID ou une CLASS, alors on peut modifier certains aspects de forme individuelles ou multiples.

24.	Quelle balise HTML permet de créer un lien hypertexte ?

La balise `<a>` avec l'attribut href permet de créer un lien hypertexte. Par exemple un lien pour revenir à la page index : `<a href="index.html">Accueil</a>`.

25.	Qu’est-ce qu’une requête AJAX ?

L'AJAX est une technique de développement web permettant d'actualiser une partie d'une page sans devoir en recharger tout le contenu.
Acronyme d'Asynchronous Javascript And Xml : l'AJAX est apparu en 1998 mais dont l'usage a été démocratisé que bien plus tard grâce en partie à la bibliothèque open source jQuery ayant intégré cette fonctionnalité.
Ainsi on peut soumettre des formulaires sans recharger la page, afficher des propositions dans un champ de recherche lorsqu'on tape les premiers caractères, effectuer une requête en base de données pour mettre à jour un bloc d'une page, consommer une API externe de forme asynchrone au chargement de la page sur une action utilisateur.

26.	Quel sélecteur CSS permet de sélectionner tous les éléments d’une classe spécifique ? D’un identifiant spécifique ?

Le sélecteur CSS qui permet de sélectionner tous les éléments est `*`.  
Pour une classe : `.class { }`  
Pour un identifiant spécifique : `#id { }`

27.	Définir le responsive design

Il s'agit de rendre un site web adapté et accessible à tous les supports (devices) possibles : ordinateurs, smartphones, tablettes, etc.
Cela s'effectue à la fois avec la programmation HTML et le style CSS 

28.	Qu’est-ce que le templating ?

Le templating est un moyen de générer du code HTML en incluant des variables, des boucles, des conditionnelles... dans un fichier HTML.  
Il s'agit de définir un modèle HTML qui sera remplacé ultérieurement par des données que l'on souhaite afficher.  
Cela permet d'ajouter des éléments HTML sans avoir à modifier le code source de la page.  

Exemple :

On a un fichier template.html :

29.	Qu’est-ce qu’une fonction anonyme en Javascript ?

Une fonction anonyme en JavaScript est une fonction qui est définie sans nom et est utilisée une seule fois. 

Elle est souvent utilisée comme une fonction de rappel ou comme une fonction qui est passée en tant qu'argument à une autre fonction.

Exemple :
```javascript
const sayHello = function() {
    console.log('Bonjour');
};

sayHello();
```

30.	Quelle méthode JavaScript est utilisée pour ajouter un élément à la fin d'un tableau ?

Pour ajouter un élément à la fin d'un tableau, on utilise la méthode `push()` en ciblant le tableau correctement.
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

Un « media query » est une fonction en CSS permettant de définir le comportement de certains éléments, classes ou ids en fonction de paramètres définis par le concepteur.  
Par exemple, on peut définir la taille minimale d'un écran et la taille maximale dans lesquelles le comportement de ces éléments agissent d'une manière définie, on peut penser au responsive design sur mobile et tablettes qui diffère du format desktop.  
Ainsi, on peut favoriser les performances d'affichage de ces éléments et l'adapter au format pour rendre l'expérience utilisateur optimale.

32.	Qu’est-ce qu’un pseudo élément en CSS ?

Un pseudo élément en CSS est une fonction permettant de styliser des parties définies d'un élément HTML. Par exemple, pour modifier le surlignage de son texte sur son site web pour ne pas garder celui de base (de couleur bleue), il faut alors écrire dans son CSS :

```css
::selection {
    background-color: black;
    color: white;
}
```

Ainsi on remplace la couleur bleue initiale de la fonction de surlignage en une couleur noire et en changeant également la couleur du texte pour s'assurer de la lisibilité. Il faut ajouter `-moz-` pour définir cela sur les navigateurs Mozilla également sinon on perd notre effet et altère l'expérience utilisateur.

33.	Qu’est-ce que Bootstrap ? Donner d’autres exemples équivalent

Bootstrap est un framework frontend OpenSource qui permet de faciliter la mise en forme de sites web responsives. Il fournit des classes prédéfinies qui peuvent être utilisées pour modifier le style CSS de son code HTML. 

D'autres framework tels que Tailwind CSS, Semantic UI, Bulma, Foundation, et d'autres encore, sont capables de proposer des fonctionnalités similaires. 

Tailwind CSS, par exemple, propose des classes plus précises pour créer des interfaces détaillées sur mesure, tandis que Bulma propose des composants prédéfinis pour créer des interfaces plus rapides.

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

En POO, une propriété est une variable qui est définie au sein d'une classe lors de la création d'un objet. 
Exemple : dans la classe Voiture, la propriété "marque" aura pour valeur "Peugeot" pour l'objet "maVoiture".<br>

Un attribut est une caractéristique de la classe, synonyme de propriété. 
Exemple : pour un ordinateur, il s'agira de la carte mère, la RAM, etc.<br>

Une méthode consiste en une action applicable à l'objet. 
Exemple : dans la classe Voiture, la méthode "demarrer()" permettra d'allumer le moteur de l'objet "maVoiture".


47.	Qu’est-ce que la visibilité d’une propriété ou d’une méthode ? Citer les différents types de visibilité

La visibilité d'une propriété ou d'une méthode est la définition de l'accès qui y est possible. 

Les différents types de visibilité sont : 
- public : la propriété ou la méthode est accessible de l'extérieur de la classe et de ses classes filles.
- private : la propriété ou la méthode est accessible uniquement de l'intérieur de la classe et non des classes filles.
- protected : la propriété ou la méthode est accessible de l'intérieur de la classe et de ses classes filles.


48.	Quelle est la méthode spécifique utilisée pour créer un nouvel objet à partir d’une classe ?

La méthode spécifique utilisée pour créer un nouvel objet à partir d’une classe est la méthode `new`. 

Exemple : `$monObjet = new MaClasse();`


49.	Qu’est-ce que l’encapsulation ?

L'encapsulation consiste à regrouper des données et des comportements au sein d'une même unité, pour en contrôler l'accès et la modification. 
Cela permet de protéger les données contre l'extérieur, en définissant les niveaux d'accès suivant des mots-clés <code>public</code>, <code>private</code> et <code>protected</code>.<br>

50.	Que signifie « étendre une classe » ? Quelle est le concept clé mis en œuvre ? Donner un exemple

Ici on parle d'héritage d'une classe, c'est-à-dire que l'on étend les attributs et méthodes d'une classe à une autre qui en bénéficie. <br>
Ainsi on crée une hiérarchie des classes et réutilise du code existant. En partant d'une classe générale, on peut créer des classes spécifiques qui héritent de la même base.

51.	Définir l’opérateur de résolution de portée

Il est essentiel dans le principe d'héritage d'une classe, l'utilisation des membres statiques et constantes d'une classe parente ou de sa propre classe.

52.	Définir une méthode / propriété statique

Une méthode statique est une méthode qui est liée à une classe et non à un objet.<br>
Elle est donc accessible sans avoir à instancier la classe.<br> 
Les propriétés statiques sont quant à elles des propriétés liées à une classe et non à un objet. <br>
Les propriétés statiques sont en lecture seule, c'est-à-dire qu'elles ne peuvent pas être modifiées une fois la classe instanciée.

53.	Définir le polymorphisme en POO

Cela permet à différentes classes d'implémenter les mêmes méthodes de manières différentes (définies par une interface ou une classe parente).<br>
En pratique, cela signifie qu'un même nom de méthode peut avoir différents comportements selon la classe qui l'implémente, permettant ainsi de traiter de manière uniforme des objets de types différents.

54.	Définir une méthode / classe abstraite ?

Une méthode ou classe abstraite consiste à déclarer une classe ou une méthode sans la définir. <br>
Cela signifie que la classe abstraite ne peut pas être instanciée directement et qu'elle ne peut contenir que des méthodes abstraites. <br>
Les classes abstraites sont utilisées pour établir des liens entre les classes et pour organiser l'héritage. <br>
Les méthodes abstraites sont des méthodes qui ne sont pas définies mais qui doivent être définies dans les classes qui héritent de la classe abstraite.

55.	Définir le chaînage de méthodes

Le chaînage de méthodes consiste à agir sur plusieurs classes d'un objet en une instruction.

Exemple :
```php
$objet->methode1()->methode2();
```

56.	Qu’est-ce que la méthode __toString() ? Existe-t-il d’autres méthodes « magiques »

La méthode __toString() est une méthode qui permet de définir comment un objet doit être converti en string.<br>
Il existe d'autres méthodes magiques qui sont appelées automatiquement par PHP en fonction de l'usage de l'objet. <br>

Les méthodes magiques sont :
- __construct() : La méthode **__construct()** est lancée lors de la création d'un objet. Elle permet de configurer l'objet en lui attribuant des valeurs par défaut.
- __destruct() : La méthode **__destruct()** est exécutée lorsque l'objet est détruit. Elle permet de libérer les ressources utilisées par l'objet.
- __set() : La méthode **__set()** est déclenchée lorsqu'une propriété inexistante est assignée. Elle permet de gérer l'assignation de valeurs à des propriétés inconnues.
- __get() : La méthode **__get()** est exécutée lorsque l'on accède à une propriété inexistante. Elle permet de gérer l'accès à des propriétés inconnues.
- __isset() : La méthode **__isset()** est appelée lorsque l'on teste l'existence d'une propriété avec l'opérateur isset(). Elle permet de définir le comportement de isset() pour les propriétés de l'objet.
- __unset() : La méthode **__unset()** est exécutée lorsque l'on supprime une propriété avec l'opérateur unset(). Elle permet de définir le comportement de unset() pour les propriétés de l'objet.
- __sleep() : La méthode **__sleep()** est exécutée lorsque l'on sérialise un objet. Elle permet de définir les propriétés qui doivent être sauvegardées.
- __wakeup() : La méthode **__wakeup()** est exécutée lorsque l'on désérialise un objet. Elle permet de définir les actions à réaliser lors de la désérialisation.
- __invoke() : La méthode **__invoke()** est lancée lorsque l'on utilise un objet comme fonction. Elle permet de définir le comportement de l'objet lorsqu'il est utilisé comme fonction.
- __set_state() : La méthode **__set_state()** est exécutée lorsque l'on instancie un objet à partir d'un tableau. Elle permet de définir comment l'objet doit être instancié.
- __clone() : La méthode **__clone()** est exécutée lorsque l'on clone un objet. Elle permet de définir le comportement de l'objet lorsqu'il est cloné.
- __debugInfo() : La méthode **__debugInfo()** est exécutée lorsque l'on passe un objet en paramètre d'une fonction var_dump(). Elle permet de définir les informations qui doivent être affichées lors de la mise à jour de l'objet.


57.	Qu’est-ce qu’un « autoload » ?

Un « autoload » consiste à charger des classes et des fichiers en fonction de leur nom.<br>
Cela permet de ne pas avoir à inclure des fichiers et des classes manuellement.

58.	Comment appelle-t-on en français les « getters » et les « setters » ?

On appelle en français les accesseurs pour les "getters" et les mutateurs pour les "setters".<br>
Le but pour les accesseurs est de récupérer les informations et pour les mutateurs de les modifier selon l'instruction programmée.

59.	Qu’est-ce que la sérialisation en PHP ?

Il s'agit d'une méthode de conversion des données (sous forme de tableau, d'objets ou autre) en une chaîne de caractères pour ensuite les manipuler plus aisément.

## Architecture 
60.	Qu’est-ce que l’architecture client / serveur ? Grâce à quel type de requête peut-on interroger le serveur. Définir l’acronyme de ce type de requête. Si on ajoute un « S » à cet acronyme, expliquer la différence

L'architecture client/serveur est une forme d'architecture applicative qui permet d'interconnecter des ordinateurs entre eux. 
Un client est un ordinateur qui envoie des requêtes à un serveur qui les exécute. Les clients envoient des requêtes au serveur qui les traite et leur envoie des réponses. 
Les clients n'ont pas accès directement aux ressources du serveur, mais peuvent y accéder via des requêtes.<br>
On peut interroger le serveur en envoyant des requêtes HTTP (HyperText Transfer Protocol). L'acronyme de ce type de requête est HTTP.<br>
Si on ajoute un "S" à cet acronyme, on obtient HTTPS. HTTPS est un protocole de communication qui sécurise les échanges entre un client et un serveur en encryptant les données envoyées et reçues.

61.	Donner la définition d’un design pattern. Citer au moins 3 exemples de design pattern

Le design pattern (patron de conception) est un élément important en POO : il a pour but de répondre à un problème technique avec une infrastructure logicielle faite de quelques classes. Les design patterns sont des solutions éprouvées pour résoudre des problèmes couramment rencontrés lors de la conception d'un programme.

**Catégories de design patterns :**
- *Patterns de création* : gèrent l'instanciation des objets (Singleton, Fabrique)
- *Patterns structurels* : organisent les relations entre les objets (Composite, Adaptateur)
- *Patterns comportementaux* : définissent la communication entre objets (Observateur, Stratégie)

**Exemples de design patterns :**

1. **Modèle Composite** : 
   - Permet de traiter un groupe d'objets de la même manière qu'un objet unique
   - Exemple : Représenter une structure de fichiers avec dossiers et sous-dossiers
   - Les feuilles et les composites suivent un modèle qui fait appel à la même interface logicielle
   - La manipulation est la même à chaque utilisation

2. **Singleton** : 
   - Limite l'instanciation d'une classe à un seul objet
   - Utilisé pour coordonner les opérations à l'intérieur d'un système donné
   - Exemple : Gérer une connexion de base de données unique pour toute l'application

3. **Fabrique** : 
   - Patron de conception de création
   - Définit une interface pour créer des objets dans une classe mère
   - Délègue le choix des types d'objets à créer aux sous-classes
   - Exemple : Créer différents types de documents (PDF, Word) via une fabrique de documents

**Avantages des design patterns :**
- Réutilisation de solutions éprouvées
- Amélioration de la maintenabilité du code
- Standardisation des approches de conception
- Facilitation de la communication entre développeurs

62.	Qu’est-ce que l’architecture MVC ?

L'architecture MVC (Modèle-Vue-Contrôleur) est un design pattern qui structure les éléments d'un site web en trois parties distinctes : 
- le modèle, 
- la vue, 
- le contrôleur. 

Le modèle gère les données, la vue s'occupe de l'interface utilisateur et le contrôleur orchestre les interactions entre les deux. <br>
Cela permet de séparer les préoccupations de l'application en trois parties distinctes, ce qui facilite la maintenance et la mise à jour.

63.	Quel est le rôle de chaque couche du design pattern MVC : Model, View, Controller ?

Afin d'être plus précis, le Modèle est la couche qui gère les données de l'application : elle stocke, modifie et supprime les données en interagissant directement avec la base de données. Elle prépare les requêtes SQL qui lui sont envoyées.

Le Controller est la couche qui répond aux actions de l'utilisateur sur la couche View. Il reçoit les requêtes de l'utilisateur, les traite et les transmet au Modèle. Après cela, il prend en charge les résultats du Modèle et les transmet à la View.

Le Controller est donc le lien entre le Modèle et la View, servant à gérer les demandes et contrôler ce qui est renvoyé également avant que les informations ne soient affichées sur la View. Il est donc le maître d'oeuvre de l'application, coordonnant les interactions entre les différentes couches.

64.	Quels sont les avantages de l’architecture MVC ?

Les avantages de l'architecture MVC sont :
- Separation des responsabilités : chaque partie a un rôle qui lui est propre et n'interfère pas dans celui des autres.
- Facilitation de la maintenance et de la mise à jour : comme elles sont isolées les unes des autres, la mise à jour de chacune peut se faire individuellement au besoin.
- Facilitation de la testabilité : de cette façon, on peut plus facilement cibler les composantes de l'application et tester seulement celles qui ont besoin d'une modification.

65.	Existe-t-il des variantes à l’architecture MVC ?

Il existe plusieurs variantes qui sont nées de l'architecture MVC, notamment les architectures MVVM et MVP.

MVVM (Modèle-Vue-VueModèle) est une variante de l'architecture MVC qui se distingue par la division des responsabilités : 
- le Modèle gère les données, 
- la Vue gère l'affichage de l'interface utilisateur et 
- la VueModèle est un pont entre le Modèle et la Vue fournissant une interface que la vue peut utiliser pour accéder aux données du modèle de manière appropriée. <br>

MVP (Modèle-Vue-Présentateur) est une variante de l'architecture MVC qui se distingue par la division des responsabilités : 
- le Modèle gère les données, 
- la Vue gère l'affichage de l'interface utilisateur et 
- le Présentateur lie la Vue au Modèle de sorte à organiser et formater les données récupérées du Modèle. Cette couche regroupe les traitements concernant les actions de l'utilisateur, la couche Présentateur n'a pas accès à la Vue. <br>

Il n'y a pas un modèle meilleur qu'un autre, mais on choisit celui qui nous convient le mieux et ce en amont de tout.
On doit apporter un oeil attentif au choix de l'architecture qui correspond le mieux aux besoins du projet.

66.	Qu’est-ce qu’une API ? Définir l’architecture REST

Une API (Application Programming Interface) est une interface de programmation qui permet à une application de communiquer avec un service tiers, en échangeant des données, en exécutant des actions, ou en consommant des ressources. 
Les API Web sont couramment utilisées pour interagir avec des services distants, comme des bases de données, des systèmes de gestion de contenu, ou des services de paiement, en envoyant des requêtes HTTP (GET, POST, PUT, DELETE, etc.).

## Modélisation - Base de données
67.	Qu’est-ce que la modélisation de données ? Définir la méthode Merise

La modélisation de données consiste à prévoir le fonctionnement d'une application avec une base de données. <br>
De plus, elle permet de prévoir les différentes caractéristiques importantes au projet et au bon fonctionnement de l'application.<br>

La méthode Merise, ou Méthode d'Etude et de Réalisation Informatique par les Sous-Ensembles/des Systèmes d'Entreprise, est une méthode d'analyse, de conception et de gestion de projet. <br>
Le principe est d'articuler la démarche autour de 3 axes : conceptuel, logique et physique.

68.	Quelles sont les 3 étapes principales de la méthode Merise ? 
a.	Analyse, conception et réalisation

La phase initiale consiste à étudier et comprendre les bsoins du système : Analyse. <br>
On identifie les processus, les flux d'informations et l'objectif est de produire une vision claire des besoins. <br>

La phase de modélisation consiste à concevoir l'architecture du système : Conception. <br>
On crée des modèles conceptuels et logiques (MCD / MLD) afin d'organiser et structurer les données et traitements. <br>

La phase de développement consiste en une mise en oeuvre concrète du système : Réalisation. <br>
On transforme les modèles en solutions opérationnelles, développe les applications, bases de données et interfaces. <br>
S'ensuit alors une phase de tests et validaution du système.

b.	Planification, exécution et contrôle

On utilisera ces termes dans le cadre de la gestion de projet. <br>
Ils permettent de suivre, contrôler et vérifier le bon fonctionnement de l'application durant son développement. <br>
Il s'agit d'un point important quant aux livrables à remettre aux clients.

c.	Création, modification et suppression

Il s'agit de termes trop génériques ne décrivant pas spécifiquement les étapes propres à la méthode Merise.

69.	Qu’est-ce qu’un modèle conceptuel de données (MCD) en Merise ?

Un MCD (modèle conceptuel de données) sert à définir en une représentation abstraite et graphique la structure des données d'un système d'information : les entités, les relations et les attributs. <br>

Le MCD a pour caractéritiques d'être indépendant des considérations techniques, compréhensible par les utilisateurs et concepteurs en usant des termes simples et concrets.

Il se compose d'entités, d'associations et d'attributs afin de pouvoir modéliser le fonctionnement d'une application ou d'un système d'information.

70.	Qu’est-ce qu’un modèle logique de données (MLD) en Merise ?

Le MLD (modèle logique de données) permet de traduire techniquement le MCD. <br>
Il est adapté à un système de gestion de base de données en montrant les relations entre les entités par l'intégration de clé primaire et clé étrangère. <br>
Il représente les donnée ssous forme de tables et intègre les contraintes techniques.

On pourrait dire qu'il s'agit d'une conversion du MCD des entités directement en tables que l'on pourrait utiliser dans une base de données.
L'objectif est de préparer la création physique de la base de données en la structurant de manière opérationnelle afin d'en faciliter l'implémentation.


71.	Donner la définition des mots suivants :
a.	Entité

Une entité est un groupe de données qui est lié ensemble par des relations.

b.	Relation

Une relation est une liaison entre deux ou plusieurs entités.

c.	Cardinalité

Une cardinalité traduit une règle de gestion qui peut être One to One, One to Many, Many to One ou Many to Many.

d.	Clé primaire / clé étrangère

Une clé primaire permet d'identifier de façon unique chaque enregistrement d'une table. <br>
Une clé étrangère relie deux tables entre elles. C'est un point de référence qui garantit la cohérence et l'intégrité des données.

72.	Que devient une relation de type « Many To Many » dans le modèle logique de données ?

Dans le modèle logique une relation de type « Many to Many » devient une table composées des attributs des entités impliquées.

73.	Qu’est-ce qu’une base de données ?

Une base de données est un ensemble de tables regroupant des informations qui y sont stockées. Au moyen d'un logiciel et de requêtes, un utilisateur peut accéder aux différentes informations sauvegardées.

74.	Définir les notions suivantes : 
a.	SQL

SQL, ou Structured Query Language, est un langage de programmation permettant de stocker et traiter des informations stockées en base de données.

b.	MySQL

Il s'agit d'un système permettant d'administrer et gérer des données au moyen de requêtes SQL?

c.	SGBD (donner 2 exemples de SGBD)

L'acronyme SGBD vient de Système de Gestion de Base de Données. Vulgairement raccourci à « base de données », cela est plus complet que ne laisse transparaître le nom. Il s'agit en fait d'un logiciel définissant le modèle d'un système de base de données.
Ainsi on structure la base de données de sorte à faciliter les lectures et écritures en fonction des accès.

Exemples de SGBD : 
- MongoDB orienté documents (NoSQL)
- Firebird relationnel (SQL)

75.	Dans une base de données, les données sont stockées dans des ___. Celles-ci sont constituées de lignes appelées ___ et de colonnes appelées ___

Dans une base de données, les données sont stockées dans des __tables__. Celles-ci sont constituées de lignes appelées __enregistrements__ et de colonnes appelées __champs__.

76.	Quelle est la différence entre une base de données relationnelle et non relationnelle ?

Les bases de données relationnelles stockent des données selon un schéma strict avec des relations entre les différentes tables qui les composent. On garantit alors la cohérence de la base de données grâce aux propriétés ACID.<br>
Les bases de données non relationnelles stockent des données de manière flexible assurant une meilleure scalabilité des éléments enregistrés. On peut alors stocker différents documents, clé-valeur ou graphes.

77.	Qu’est-ce qu’une jointure dans une base de données ? En existe-t-il plusieurs ? Si oui lesquelles ?

Une jointure est une association entre deux tables au minimum afin de recouper des données ayant un intérêt. Il en existe quatre essentiellement :
 - INNER JOIN : Elle permet de récupérer les données recoupées des deux tables. On garde que ce qui est commun à la table A et B.
 - LEFT JOIN : Elle permet de récupérer l'ensemble des données de la table A et les données recoupées de la table B (qui sont les mêmes que la table A).
 - RIGHT JOIN : Elle permet de récupérer l'ensemble des données de la table B et les données recoupées de la table A (qui sont identiques à la table B).
 - FULL JOIN : Elle permet de récupérer la totalité des deux tables (ou plus) ciblées sans devoir définir de spécificités.

78.	A quoi sert une vue dans une base de données ?

![image](https://github.com/user-attachments/assets/feb4898d-609e-4f74-b12a-bedfdfcd1636)

Une vue permet de simplifier l'accès aux données, de sorte que l'on sauvegarde une requête complexe afin d'en extraire les éléments souhaités.

79.	Qu’est-ce que l’intégrité référentielle dans une base de données ?

Il s'agit de la cohérence entre les différentes tables liées par des clés étrangères dans une base de données dite relationnelle.

80.	Quelles sont les fonctions d’agrégation en SQL ?

Les fonctions d'agrégation permettent d'effectuer des opérations statistiques sur un ensemble d'enregistrement.
 - AVG() permet de calcluer la moyenne
 - COUNT() permet de compter le nombre d'enregistrement sur une colonne ou une table
 - MAX() renvoie la valeur maximale d'une colonne ou d'un ensemble de lignes (numérique et alphanumérique)
 - MIN() renvoie la valeur minimale d'une colonne ou d'un ensemble de lignes (numérique et alphanumérique)
 - SUM() permet de caluler la somme d'un ensemble d'enregistrement
 
81.	Qu’est-ce qu’un CRUD dans le contexte d’une base de données ?

CRUD est l'acronyme pour CREATE, READ, UPDATE & DELETE. 
Il s'agit des opérations principales d'une base de données pour la créer, la lire, la mettre à jour et supprimer des enregistrements de celle-ci.
On retrouve les fonctions suivantes pour réaliser ces actions :
 - INSERT INTO table pour créer
 - SELECT * FROM table pour lire les enregistrements d'une table
 - UPDATE table SET email = "example@test.fr" WHERE user_id = 1
 - DELETE FROM table WHERE user_id = 1

82.	Quelles sont les clauses qui permettent de :
a.	Insérer un nouvel enregistrement dans une table

INSERT INTO table (value1, value2) VALUES (valueA, valueB); On insère dans la table dans les champs value1 et value2, les valeurs définies valueA et valueB respectivement.

b.	Modifier un enregistrement dans une table

INSERT INTO table SET email ="example@test.fr" WHERE user_id = 1; On modifie dans la table l'email de l'utilisateur ayant pour ID le numéro 1.

c.	Supprimer un enregistrement dans une table

DELETE FROM table WHERE user_id = 1; On supprime l'enregistrement dans la table concernant l'utilisateur ayant pour ID le numéro 1.

d.	Supprimer la base de données

DROP DATABASE my_db; Nous sélectionnons la base de données ayant pour nom my_db afin de la supprimer dans son intégralité.

e.	Filtrer les résultats d’une requête SQL

SELECT * FROM user WHERE age > 30; On sélectionne les utilisateurs dont l'âge est supérieur à 30 ans.

f.	Trier les résultats d’une requête SELECT

SELECT * FROM user ORDER BY name ASC; On sélectionne les utilisateurs et les trie par ordre alphabétique ascendant, en partant de A jusqu'à Z.

g.	Regrouper les résultats d'une requête SELECT en fonction d'une colonne spécifique

SELECT is_verified, COUNT(*) FROM user GROUP BY is_verified; On sélectionne les utilisateurs de la table user et on compte le nombre d'utilisateurs vérifiés et non vérifiés, en les regroupant par catégorie (is_verified).

h.	Concaténer 2 chaînes de caractères 

SELECT CONCAT(u.first_name, ' ', u.name) AS identity FROM user u

83.	Comment se connecter à une base de données en PHP ? Quelle est la classe native utilisée ?

Pour se connecter à une base de données en PHP, on utilise la classe native PDO (PHP Data Objects).
Cela permet de créer une interface pour accéder à la base de données afin de paramétrer des requêtes préparées.

## Symfony
84.	Qu’est-ce que Symfony ?

Symfony est un framework en PHP qui permet de créer des applications web robustes et scalables.

85.	Sur quel langage de programmation et design pattern repose Symfony ? 

Il repose sur le langage de programmation PHP et le design pattern MVP : (Modèle-Vue-Présenteur).

86.	Quelle est la dernière version en date de Symfony ?

La dernière version en date stable de Symfony est la : 7.2.2 sortie en Novembre 2024.

87.	Qu’est-ce qu’un bundle ? 

Il s'agit d'un répertoire contenant tou ce qui peut être nécessaire pour une fonctionnalité tel que les classes PHP, des templates et des fichiers de configuration. Cela permet de créer des modules au sein des applications et de réutiliser ces modules au sein de différents projets.

88.	Quel est le moteur de template utilisé par défaut dans Symfony ?

Le moteur de template utilisé par Symfony est Twig.

89.	Qu’est-ce qu’un ORM ? Quel est son utilité et comment s’appelle-t-il au sein de Symfony ?

Un ORM (Object Relational Mapping) est une manière de gérer les interactions entre les données d'une base de données relationnelle et les objets utilisés par une application. 

On peut alors lier des objets en POO à des tables de bases de données, simplifiant ainsi la gestion des données.

Pour Symfony, l'ORM utilisé s'appelle Doctrine.

90.	Qu’est-ce que l’injection de dépendances ? Quel est l’outil utilisé dans ce contexte et quel fichier contient l’intégralité des dépendances du projet ? 

L'injection de dépendances est une pratique permettant à une classe d'utiliser des services ou obkets via un mécanisme externe.
Au lieu d'instancier directement les éléments nécessaires, les dépendancers permettant une modularité et faciliter les tests.
Ces dépendances sont gérées via l'outil Composer et listées dans le fichier `*composer.json*`.

91.	Que permet le bundle Maker au sein de Symfony ? 

Le bundle Maker permet de créder rapidmeent des entités, des contrôleurs, des formulaires, des commandes, des fonctionnalités diverses et variées dont on aurait besoin dans notre projet.
Pour ce faire, on emploie des commandes telles que `make:entity` ou `make:controller`. 

92.	Quel est le langage de requêtage exploité au sein d’un projet Symfony ?

Le langage de requêtage exploité au sein de Symfony est le DQL => __*Doctrine Query Language*__.
Il s'agit d'un langange orienté objet fourni avec Doctrine. Il ressemble au SQL mais abstrait les détails de la base de données.

93.	Quel est le composant qui garantit l’authentification et l’autorisation des utilisateurs ?

Le composant Security garantit l'authentification et l'autorisation des utilisateurs.
Il y arrive en vérifiant l'identité d'un utilisateur via des méthodes telles que le login/password ou OAuth par exemple.
Puis, il autorise les utilisateur grâce aux permissions en fonction des rôles : `ROLE_USER` ou `ROLE_ADMIN`.

On retrouve dans le fichier `config/packages/security.yaml` les configurations de firewalls pour l'authentification ;
Et pour l'autorisation, via des règles d'accès et annotation tel que @IsGranted.

## Sécurité
94.	Qu’est-ce que l’injection SQL ? Comment s’en prémunir ?

Il s'agit d'attaques contre les bases de données relationnelles (SQLi) et non relationnelles (injections NoSQL).
Un utilisateur communique depuis l'application web une entrée modifiant la requête SQL à la base de données.
Pour s'en prémunir, il faut utiliser des requêtes préparées et l'échapement des caractères spéciaux.

95.	Qu’est-ce que la faille XSS ? Comment s’en prémunir ?

La faille XSS (Cross-Site Scripting) permet aux attaquants d'injecter des scripts malveillants dans des pages web pour voler des données ou compromettre des sessions utilisateurs.<br> 
Pour s'en prémunir : encoder les sorties, valider et filtrer les entrées, utiliser des Content Security Policy (CSP), et échapper les caractères spéciaux.

96.	Qu’est-ce que la faille CSRF ? Comment s’en prémunir ?

La faille CSRF (Cross-Site Request Forgery) permet à un attaquant de faire exécuter des actions non désirées à un utilisateur connecté sur un site web. <br>
Pour s'en prémunir, il faut générer et vérifier des jetons uniques (tokens) pour chaque requête, utiliser des en-têtes HTTP personnalisées, et implémenter la politique SameSite pour les cookies.

97.	Définir l’attaque par force brute et l’attaque par dictionnaire

Attaque par force brute : méthode systématique testant exhaustivement toutes les combinaisons possibles de mots de passe/clés jusqu'à trouver la bonne. <br>
Attaque par dictionnaire : approche utilisant une liste prédéfinie de mots de passe probables (mots courants, noms, dates) pour tenter de craquer une authentification.

98.	Existe-t-il d’autres failles de sécurité ? Citer celles-ci et expliquer simplement leur comportement

Il existent plusieurs failles de sécurité, notamment :
- Faille XSS (Cros-Site Scripting) 
- Faille CSRF (Cross-Site Request Forgery)
- Faille SQL Injection 
- Les attaques par DdoS 
- Les attaques par force brute : on force avec des algorithmes puissants les mots de passes des utilisateurs pour les deviner.
- Les attaques par dictionnaire : se base sur un dictionnaire recessant les mots de passes les plus utilisés et leurs variantes.


99.	A quoi servent l’authentification et l’autorisation dans un contexte d’application web ?

L’authentification est la procédure qui permet de vérifier l’identité d’un utilisateur en s’assurant qu’il est bien qui il prétend être (par exemple en comparant un mot de passe à une entrée utilisateur).<br>
L’autorisation est la procédure qui permet de définir les accès autorisés pour un utilisateur une fois authentifié. Par exemple, un utilisateur peut avoir accès à certaines parties du site web mais pas d'autres.


100.	Définir la notion de hachage d’un mot de passe et citer des algorithmes de hachage

Le hachage génère une valeur unique et déterministe à partir de données d'entrée, rendant difficile la récupération de l'entrée d'origine. Les algorithmes Bcrypt et Argon2I sont dits "forts" car ils ajoutent du salage et un facteur de coût pour ralentir les attaques par force brute. Cela rend le processus de hachage plus sécurisé et résistant aux attaques de type dictionnaire ou force brute.

101.	Qu’est-ce qu’une politique de mots de passe forts ?

Une politique de mots de passe forts impose des critères pour garantir la sécurité des mots de passe, tels que la longueur minimale, la diversité des caractères (majuscules, minuscules, chiffres, symboles) et l'interdiction de mots de passe simples. 

102.	Qu’est-ce que l’hameçonnage ?

Le hameçonnage (phishing) est une technique utilisée par des cybercriminels pour voler des informations personnelles en envoyant des messages qui semblent légitimes. Ils peuvent se faire passer pour des entreprises ou créer un sentiment d'urgence pour inciter l'utilisateur à divulguer des informations sensibles. L'utilisateur, en suivant un lien vers une fausse page web, expose alors ses données (email, mot de passe, identité, etc.), que l'attaquant peut exploiter.

103.	Définir la « validation des entrées »

La validation des entrées consiste à filtrer les données saisies par un utilisateur dans un formulaire (inscription, contact, etc.) pour vérifier qu'elles respectent un format attendu. Cela permet de s'assurer que les données sont valides, sécurisées et exemptes d'erreurs ou de tentatives d'injection malveillante.

## RGPD
104.	Qu’est-ce que le RGPD ?
      
Le RGPD est l'acronyme de «Règlement Général de Protection des Données» en français. En anglais, cet acronyme sera écrit GDPR "General Data Protection Regulation".

105.	Quel est son objectif principal ?

Son objectif principal est de protéger les droits des personnes concernées par la collecte et le traitement de leurs données personnelles.
Ce aussi bien dans un contexte privé que public.

106.	Quelle est la date d’entrée en vigueur du RGPD ?

Le RGPD est entré en vigueur le 24 mai 2016 et s'applique depuis le 25 mai 2018.

107.	Quelles sont les sanctions possibles en cas de non-respect du RGPD ?

Les sanctions en cas de non-respect du RGPD peuvent être lourdes et peuvent engendrer des poursuites judiciaires.
Par exemple, le montant des sanctions pécuniaires peut s'élever jusqu'à 20 millions d'euros ou dans le cas d'une entreprise jusqu’à 4% du chiffre d'affaires annuel mondial.
En 2023, 42 sanctions dont 36 amendes pour un montant cumulé de 89 179 500 euros.

108.	En France, quel est l’autorité administrative qui s’occupe de faire appliquer le RGPD ?

En France, il s'agit de la CNIL : acronyme de la Commission Nationale de l'Informatique et des Libertés.
Elle est chargée de faire appliquer le RGPD auprès de toutes entreprises qui traitent des données personnelles.

109.	Quel est le consentement valide selon le RPGD ?

Le consentement d'un utilisateur doit être libre, spécifique, éclairé et univoque.

110.	Qu’est-ce qu’une politique de confidentialité ?

Une politique de confidentialité est un document légal expliquant comment une organisation collecte, utilise, stocke et protège les données personnelles des utilisateurs. Elle doit informer les utilisateurs de leurs droits et des pratiques de traitement des données, en conformité avec les lois sur la protection de la vie privée (comme le RGPD).

111.	Quelle est la durée de conservation maximale des données personnelles selon le RGPD ?

Le RGPD ne définit pas de durée de conservation maximale pour les données personnelles. Cependant, la durée de conservation doit être justifiée par le cycle de vie de la donnée et son objectif spécifique.

112.	Quels sont les droits des utilisateurs selon le RGPD ?

Les utilisateurs doivent avoir la possibilité d'accéder à leurs données personnelles, de connaître leur utilisation, de les modifier ou même de les supprimer, et ce, à tout moment.

113.	Qu’est-ce que le principe de minimisation des données selon le RGPD ?

Il s'agit de ne collecter que les données nécessaires au bon fonctionnement de l'application ou du service. Ce principe vise à limiter la collecte de données et à protéger la vie privée des individus.

## SEO
114.	Qu’est-ce que le SEO ? 

Le SEO (Search Engine Optimization), ou référencement naturel, consiste à optimiser son site web, notamment les mots-clés, la structure et l’aspect technique, pour améliorer sa visibilité et son classement sur les moteurs de recherche.

115.	Quel est l’objectif principal du SEO ?

L'objectif principal du SEO est d'améliorer la visibilité d'un site internet en suivant les critères établis par Google (leader des moteurs de recherche), afin d'assurer que le site soit bien indexé et facilement accessible pour les utilisateurs, tout en offrant une expérience de qualité.

116.	Existe-t-il plusieurs types de référencement ? Lesquels ?

Il existe plusieurs types de référencement : le SEO (référencement naturel, le SEA (référencement payant), le référencement international et le référencement local.

117.	Qu’est-ce que la densité de mots-clés en SEO ?

La densité de mots-clés désigne l'utilisation optimale d'un mot-clé dans une page pour en améliorer le référencement. Il est important de ne pas abuser de ce mot-clé afin d'éviter le 'keyword stuffing', qui peut pénaliser le site. Idéalement, la densité de mots-clés doit être comprise entre 1 % et 3 % du texte total sur la page.

118.	Qu’est-ce qu’un attribut « alt » ?

Un attribut « alt » en HTML permet de donner une description textuelle à une image. Le terme désigné texte alternatif, alternatif dans le cas où l'utilisateur ne pourrait pas accéder à l'image visuellement ou serait dans l'incapacité de voir l'image.
De ce fait, en donnant une description dans une chaine de caractères à l'attribut alt d'une image, on rend possible la retranscripption vocale du texte permettant à l'utilisateur de comprendre l'élément que l'on a intégré dans notre site internet.

119.	Qu’est-ce que la balise « meta description » ?

La balise "meta description" est un élément HTML ajoutant des informations essentielles au sujet d'une page web et ainsi permettre son bon référencement. Comme son nom l'indique, elle décrit brièvement le contenu de la page dont le lien est affiché dans le résultat de la recherche du moteur utilisé.

120.	Qu’est-ce que le « nofollow » en SEO ?

Le "nofollow" est un attribut HTML utilisé pour les liens publicitaires, les commentaires ou les contenus douteux afin d'éviter d'influencer le classement des pages liées.

121.	Quelle est l'importance du contenu de qualité pour le référencement d'un site web ?

Un contenu de qualité engage les utilisateurs en leur fournissant des informations pertinentes et utiles en réponse à leurs recherches. À l'inverse, un contenu de faible qualité ne sera pas bien indexé par les moteurs de recherche et risque de ne pas être mis en avant, ce qui nuit à la visibilité du site.

122.	Pourquoi est-il important d'utiliser des balises de titre (h1, h2, h3, etc.) de manière structurée ?

La sémantique en HTML permet d’attribuer un sens clair aux éléments d'une page, tant pour les moteurs de recherche que pour les utilisateurs. Une hiérarchie bien structurée facilite la compréhension et la lecture des informations, améliorant ainsi l'accessibilité et le référencement du site.

123.	Quelle est la recommandation pour les URL d'un site web bien référencé ?

Il est important de créer des URL courtes, concises et précises afin de ne pas perdre le lecteur et de maintenir sa confiance. Permettre à l'utilisateur de comprendre facilement où il se trouve dans le chemin URL améliore non seulement la visibilité du site, mais renforce également la confiance des visiteurs.

124.	Qu'est-ce que le maillage interne et pourquoi est-il important pour le référencement ?

Le maillage interne consiste à créer des liens entre les pages d'un même site, permettant de diriger les utilisateurs vers des pages plus profondes qui ne sont pas visibles dans les résultats de recherche initiaux. Cela favorise la sérendipité, augmentant ainsi le taux de clics et de conversion, tout en respectant la règle des trois clics, qui suggère qu'un utilisateur ne devrait pas avoir à cliquer plus de trois fois pour accéder à l'information qu'il recherche.

125.	Qu'est-ce qu'un plan de site (sitemap) et pourquoi est-il important pour le référencement ?

Un sitemap est un fichier au format XML qui permet aux moteurs de recherche de parcourir rapidement l'ensemble des pages d'un site web. Cela facilite l'indexation des pages et en fait un levier important pour améliorer le référencement du site.


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

JavaScript gives developers the ability to create dynamic pages and content, such as forms, animations, and updates, without needing to reload the page.

b.	Define the layout and design of web pages
c.	Handle server-side operations

2)	Which programming language is primarily used for server-side web development ?
a.	PHP

PHP is primarily used for server-side web development, allowing developers to create dynamic and interactive websites by handling server-side logic, such as database interactions and user authentication.

b.	JavaScript
c.	HTML

4)	What is the purpose of a web browser ?
a.	To render and display web pages

The browser renders and displays web pages thanks to HTML, CSS, and JavaScript. 
It interprets the content from a website and presents it in a user-friendly format.

b.	To execute serve-side code
c.	To manage databases

5)	What is the difference between GET and POST methods in HTTP ?
a.	GET retrieves data from a server, while POST submits data to a server

GET and POST are two superglobal methods in PHP that behave differently. GET retrieves data from the server and appends it to the URL, while POST submits data to the server within the request body, making it more secure for transmitting sensitive information.

b.	GET submits data to a server, while POST retrieves data from a server
c.	GET and POST methods are interchangeable

6)	What is the purpose of version control systems (e.g., Git) in web development ?
a.	To track changes and manage collaborative development

The purpose of version control systems is to enable a development team to collaborate on the same project without interfering with each other's work. Each team member can create a fork of the main code to develop new features and then merge their changes back into the main codebase, allowing everyone to work at their own pace while minimizing the risk of conflicts or errors.

b.	To optimize website loading speed
c.	To handle network protocols and data transfer

7)	What is the purpose of a framework in web development ?
a.	To provide a structured environment for building web applications

As its name suggests, a framework provides a structured foundation for the code, allowing developers to focus solely on building the necessary functionalities for the application, rather than dealing with the underlying infrastructure.

b.	To handle network protocols and data transfer
c.	To create visual designs and layouts for websites

8)	What does NoSQL stand for ?
a.	Not Only SQL

NoSQL stands for 'Not Only SQL,' meaning it doesn't solely rely on traditional SQL databases for operations like generating, updating, or deleting data. Instead, NoSQL databases offer flexible data models and allow for more scalable and dynamic ways of handling data.

b.	Non-Structured Query Language
c.	New Object-Oriented Language

9)	Which of the following is a characteristic of NoSQL databases ?
a.	Strict schema enforcement
b.	Support for complex transactions
c.	Scalability and flexible data models

NoSQL databases offer more flexible data models, allowing for better scalability in their usage.
