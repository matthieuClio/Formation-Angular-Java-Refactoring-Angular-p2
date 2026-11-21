# Informations

## Deux pages principales :
Dashboard (page d'accueil) - Route par défaut :
(1) Présentera le contexte de l’application.
(2) Contiendra un graphique (type “bar” ou “pie”, comme vous pouvez le voir dans le 
design sur Figma).
(3) Ce graphique permettra la visualisation du nombre de médailles pour chaque pays, toutes 
années confondues. Pour pouvoir présenter ce graphique, l’affichage de la page d’accueil 
devra automatiquement déclencher la récupération des données nécessaires. 
(4)En cliquant sur un des pays, l'utilisateur sera redirigé vers une page “détail” à propos de 
ce pays.

Page détail pays :
(1) Lors de son affichage, cette page devra automatiquement récupérer les données propres 
au pays sélectionné par l’utilisateur.
(2) Cette page devra ensuite afficher les données relatives à ce pays : - 
nombre de participations aux JOs ; - - 
nombre total de médailles obtenues ; 
nombre total d'athlètes présentés aux JOs.
(3) Pour finir, un nouveau graphique (de type “line” ou “bar”) devra permettre à l’utilisateur 
de visualiser sur cette page le nombre de médailles obtenues par le pays au cours de 
chaque édition des Jeux olympiques.
(4) Il sera bien entendu essentiel de pouvoir retourner à la page d'accueil depuis cette page. 
Aussi, l’utilisateur peut saisir dans l’URL le pays dont il souhaite connaître les détails. Il 
faut donc vérifier que le pays existe.

## Modifications
### Navigation fluide
### UI responsive

### Interface TypeScript - src/app/models/ :
export interface Participation { 
    id: number, 
    year: number, 
    city: string, 
    medalsCount: number, 
    athleteCount: number 
} 
export interface Olympic { 
    id: number, 
    country: string, 
    participations: Participation[] 
}
### DataService dans src/app/services/data.service.ts 

### HeaderComponent (composant réutilisable) :
On constate que la page d’accueil et la page de détails d’un pays ont une structure 
d’en-tête similaire.  
● on a toujours le titre de la page et l’affichage d’indicateurs propres à chaque page, 
un indicateur étant caractérisé par un libellé et une valeur.  
● créer donc un composant HeaderComponent réutilisable qui affiche un titre et 
itère sur une liste d’indicateurs pour les afficher (pour chaque indicateur, le 
composant affiche le libellé et la valeur).

### DashboardPage (page conteneur) 
● utiliser le composant réutilisable HeaderComponent développé précédemment : 
titre de la page + KPIs (nombre de pays, nombre de JOs) 
● ajouter un pie chart qui représente les pays 

### CountryDetailPage (page conteneur) 
● utiliser un composant réutilisable HeaderComponent développé 
précédemment (titre de la page contenant le nom du pays + KPIs : participations, 
athlètes, total) 
● une graphique ligne/aire par année

### Règles d’affichage 
● Totals = gold + silver + bronze 
● Tri libre (alphabétique ou par total), mais cohérent Dashboard ↔ Détail 
● Cliquer un élément du graphe Dashboard → /country/:id 
● Bouton « Retour » sur la page détail (routerLink="/")

### États, accessibilité & responsive 
● Loading : squelettes simples (boîtes grises) ou spinner 
● Empty : message « Aucune donnée » 
● Error : message clair + bouton retour 
● Responsive : 
○ Desktop ≥ 1200px : 12 colonnes, contenus côte à côte 
○ Tablette ~ 768–1199px : 8 colonnes, graphe pleine largeur 
○ Mobile ≤ 767px : 4 colonnes, pile verticale 
● A11y : contrastes AA, focus visibles, aria-label sur boutons/icônes, descriptions 
textuelles pour les graphes

## Résultat attendu
Graphiques (barres pour totaux ; ligne/aires pour évolution)
Tri/sélection simple et navigation par clic
Gestion des états : loading, empty, error (au minimum visuels) 
Accessibilité de base (contraste, focus visibles, ARIA simples) 

## Hors périmètre
Authentification, rôles 
● Édition/saisie des données 
● Persistance réelle côté serveur

## Contraintes non fonctionnelles 
● Style : cohérent, sobre (utilisez CSS/SCSS fournis par le starter ou Angular styles 
par défaut) 
● Code : pas de any, factorisation des constantes, fichiers < 300 lignes idéalement 
● Git : commits atomiques et messages clairs (feat, fix, refactor, docs)

## Critères d’acceptation (check‑list) 
● ng serve OK sans erreur 
● / affiche un graphe fonctionnel des pays et totaux 
● Clic pays → /country/:id 
● /country/:id affiche KPI + évolution 
● Gestion d’ID invalide → message d’erreur/redirect 
● Responsive testé (desktop/tablette/mobile) 
● DataService centralise toutes les données (zéro tableau en dur dans les 
composants) 
● Types TS définis (interfaces) 
● README.md documente installation/structure/décisions 
● ARCHITECTURE.md présent et compréhensible

# Mauvaises pratiques

## Ecriture
Manque de commentaire (aucun commentaire dans le code actuel).
TypeScript : trop de any
console.log() dans la version final

## Layout
Il n'y a pas de layout pour les différentes pages.

## Architecture
Il semble ne pas y avoir de design pattern bien défini.

### Composant
Les composants doivent être placés dans un dossier component de manière à pourvoir les réutiliser dans d'autres pages.

### Service
Les éléments comme les appels HTTP doivent être dans des services.

### Structure html
Avoir une structure permettant d'intégrer le côté responsive.
