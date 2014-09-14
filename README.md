#Mobops - client#

La web application qui consomme et affiche les données de **mobops-server**

L'idée est de faire une application la plus légère possible au niveau des ressources CPU et réseau utilisées, avec une compatibilité large.

La version actuelle est une version avec un design adaptatif,  compatible avec les navigateurs mobile et desktop  des familles de Firefox, webkit (notamment chrome, safari, opera) et IE10+ . Toutefois certaines fonctionnalités ne sont disponibles que sur certains navigateurs : les notifications sur le desktop,la gestion du capteur de lumière

Un minimum d'images sont utilisées pour réduire le nombre de requêtes : celles de fontawesome et celles de meteocon. Le client de production est contenu dans 18 fichiers, et utilise moins de 500ko de réseau.


##installation##

Prévoir une bonne connexion internet et un peu de temps libre

    npm install -g grunt bower yo
    bower install && npm install
    grunt dist


##Architecture##
[Backbone.js](backbonejs.org) est utilisé pour structurer le code javascript

[require.js](requirejs.org) est utilisé pour gérer les dépendances

[Bootstrap 3.x](getbootstrap.com) est utilisé pour la mise en page, mais la majeure partie de l'application utilise des display:flex plutôt que la grille de bootstrap

[Grunt](gruntjs.com) est utilisé pour le développement et le packaging, avec notamment les tâches suivantes: 
* autoprefixer : ajoute les prefixes aux fonctionnalités css qui sont spécifiques à un navigateur : flex, gradient, animation
* uglify/require : assemble les fichiers *.js en un seul, enlève tout ce qui n'est pas nécessaires (espaces, tabulation, réduis les noms de variables,...)
* htmlmin/css/min: réduit les fichiers css et html
* manifest : génère le fichier de manifeste pour l'application cache. Ceci permet de gérer de manière directive ce que le navigateur met en cache.

[Yeoman](yeoman.io) est utilisé pour bootstraper l'application, mais aussi pour créer de nouveaux modèles/collections/crouter et view

##Cordova##
L'architecture de mobops rends l'intégration dans cordova triviale. Deux possibilités sont envisageables : 

1. donner directement https://serveur.mobops.fr/android.html comme target de la webview cordova . La webview gérant l'application cache il n'y aura des télchargements d'assets que lors de mise à jour. /android diffère de /index.html en ajoutant les js nécessaires à l'exécution des plugins

2. `cordova create Mobops  "fr.sdis71.mobops" "Mobops" --link-to ~/dist/directory/of/mobops` . Dans ce cas là il faut modifier les chemins de conf, et permettre un choix intelligent du bon fichier de configuration


