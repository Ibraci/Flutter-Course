# Flutter UI Components

Dans ce chapitre, nous allons explorer les différents composants d'interface utilisateur (UI) disponibles dans Flutter. Ces composants sont essentiels pour créer des applications mobiles interactives et visuellement attrayantes.

Sommaire

```
- Icône
- Expanded
- Case à cocher
- Carrousel d’images
- Indicateurs de progression circulaire et linéaire
- Boîte de dialogue d’alerte
- Dialogue
- Vidéos
- ListTile
- Onglets
- Graphiques
```

## Classe Icon dans Flutter

La classe `Icon` dans Flutter est utilisée pour afficher des icônes graphiques, généralement issues de la police Material Icons ou d'autres polices d'icônes. Les icônes sont évolutives, personnalisables et couramment utilisées dans les boutons, les barres de navigation, et plus encore.

### Utilisation de base

```dart
import 'package:flutter/material.dart';

class IconExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Icon(
        Icons.favorite, // Icône Material intégrée
        color: Colors.pink,
        size: 48.0,
      ),
    );
  }
}
```

### Personnalisation de l'icône

- **icon** : L'icône à afficher (par exemple, `Icons.home`).
- **color** : La couleur de l'icône.
- **size** : La taille de l'icône en pixels logiques.
- **semanticLabel** : Un label pour l'accessibilité.

```dart
Icon(
  Icons.home,
  color: Colors.blue,
  size: 36.0,
  semanticLabel: 'Accueil',
)
```

### Utiliser une icône dans un bouton

```dart
IconButton(
  icon: Icon(Icons.volume_up),
  color: Colors.green,
  onPressed: () {
    // Action lors de l'appui
  },
)
```

### Utiliser des polices d'icônes personnalisées

Vous pouvez également utiliser des polices d'icônes personnalisées en spécifiant l'`IconData` et en fournissant votre propre famille de polices.

```dart
Icon(
  IconData(0xe900, fontFamily: 'CustomIcons'),
  size: 40,
)
```

### Résumé

- La classe `Icon` est un moyen simple d'afficher des icônes dans votre application Flutter.
- Vous pouvez personnaliser l'apparence de l'icône avec la couleur, la taille, et plus encore.
- Elle fonctionne parfaitement avec d'autres widgets comme `IconButton`, `FloatingActionButton`, etc.

## Classe Expanded dans Flutter

La classe `Expanded` dans Flutter est utilisée pour faire en sorte qu'un widget enfant occupe l'espace disponible dans une colonne, une ligne ou une flexbox. Elle est très utile pour créer des interfaces réactives où les widgets doivent s'adapter dynamiquement à l'espace restant.

### Exemple de base

```dart
Row(
  children: <Widget>[
    Icon(Icons.star),
    Expanded(
      child: Container(
        color: Colors.blue,
        height: 40,
        child: Text('Ce texte occupe tout l\'espace restant'),
      ),
    ),
    Icon(Icons.star),
  ],
)
```

Dans cet exemple, le texte à l'intérieur du `Container` prendra tout l'espace horizontal disponible entre les deux icônes.

### Utilisation avec plusieurs widgets Expanded

```dart
Row(
  children: <Widget>[
    Expanded(
      flex: 2,
      child: Container(color: Colors.red, height: 40),
    ),
    Expanded(
      flex: 1,
      child: Container(color: Colors.green, height: 40),
    ),
  ],
)
```

Ici, le premier `Container` occupera deux fois plus d'espace que le second grâce à la propriété `flex`.

### Résumé

- `Expanded` permet à un widget de prendre tout l'espace disponible dans une `Row`, `Column` ou `Flex`.
- La propriété `flex` permet de répartir l'espace entre plusieurs widgets `Expanded`.

## Widget Checkbox dans Flutter

Le widget `Checkbox` dans Flutter permet d'afficher une case à cocher interactive. Il est très utilisé dans les formulaires pour permettre à l'utilisateur de sélectionner ou désélectionner une ou plusieurs options. La Checkbox peut être utilisée seule ou dans une liste.

### Utilisation de base

Voici comment afficher une simple case à cocher :

```dart
bool _isChecked = false;

Checkbox(
  value: _isChecked,
  onChanged: (bool? value) {
    setState(() {
      _isChecked = value!;
    });
  },
)
```

### Checkbox avec texte descriptif

Pour associer un texte à la case à cocher, on utilise généralement le widget `CheckboxListTile` :

```dart
CheckboxListTile(
  title: Text('Accepter les conditions'),
  value: _isChecked,
  onChanged: (bool? value) {
    setState(() {
      _isChecked = value!;
    });
  },
)
```

### Liste dynamique de Checkbox

Pour gérer une liste de cases à cocher, on peut utiliser une liste de booléens :

```dart
List<bool> _checked = [false, false, false];
List<String> _options = ['Option 1', 'Option 2', 'Option 3'];

ListView.builder(
  itemCount: _options.length,
  itemBuilder: (context, index) {
    return CheckboxListTile(
      title: Text(_options[index]),
      value: _checked[index],
      onChanged: (bool? value) {
        setState(() {
          _checked[index] = value!;
        });
      },
    );
  },
)
```

### Personnalisation avancée

Vous pouvez personnaliser la couleur, la forme et l'apparence de la Checkbox :

```dart
Checkbox(
  value: _isChecked,
  onChanged: (bool? value) {
    setState(() {
      _isChecked = value!;
    });
  },
  activeColor: Colors.green,
  checkColor: Colors.white,
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(6),
  ),
)
```

### Astuces

- Utilisez `CheckboxListTile` pour une meilleure accessibilité et une interface plus propre.
- Pour des formulaires complexes, combinez Checkbox avec `Form` et `FormField`.
- Pensez à gérer l'état de vos Checkbox dans un `StatefulWidget` ou avec un gestionnaire d'état (Provider, Riverpod, etc.).

### Résumé

- Le widget `Checkbox` permet de créer des cases à cocher simples ou multiples.
- Il est hautement personnalisable et s'intègre facilement dans les formulaires Flutter.

## Carousel Slider dans Flutter

Le `Carousel Slider` est un widget qui permet de créer un carrousel d'images ou de widgets. Il est idéal pour afficher des diaporamas ou des galeries d'images.

### Exemple de base

```dart
CarouselSlider(
  options: CarouselOptions(
    height: 200.0,
    autoPlay: true,
    enlargeCenterPage: true,
  ),
  items: [1, 2, 3, 4, 5].map((i) {
    return Builder(
      builder: (BuildContext context) {
        return Container(
          width: MediaQuery.of(context).size.width,
          margin: EdgeInsets.symmetric(horizontal: 5.0),
          decoration: BoxDecoration(color: Colors.amber),
          child: Center(child: Text('Image $i')),
        );
      },
    );
  }).toList(),
)
```

### Personnalisation

- **options** : Options de configuration du carrousel (hauteur, autoplay, etc.).
- **items** : Liste des widgets à afficher dans le carrousel.

### Résumé

- Le `Carousel Slider` est utilisé pour créer des diaporamas interactifs.
- Il peut être configuré pour jouer automatiquement et agrandir les images centrales.

## Vue en grille en escalier (Staggered Grid View) dans Flutter

La `Staggered Grid View` permet de créer une grille où les éléments peuvent avoir des tailles différentes, créant ainsi un effet visuel dynamique.

### Exemple de base

```dart
StaggeredGridView.countBuilder(
  crossAxisCount: 4,
  itemCount: 8,
  itemBuilder: (BuildContext context, int index) => Container(
    color: Colors.green,
    child: Center(child: Text('Item $index')),
  ),
  staggeredTileBuilder: (int index) => StaggeredTile.count(2, index.isEven ? 2 : 1),
  mainAxisSpacing: 4.0,
  crossAxisSpacing: 4.0,
)
```

### Personnalisation

- **crossAxisCount** : Nombre de colonnes dans la grille.
- **itemBuilder** : Fonction qui construit chaque élément de la grille.
- **staggeredTileBuilder** : Fonction qui définit la taille de chaque élément.

### Résumé

- La `Staggered Grid View` est utilisée pour créer des grilles dynamiques avec des éléments de tailles différentes.
- Elle est idéale pour les galeries d'images ou les mises en page créatives.

## Indicateurs de progression circulaire et linéaire dans Flutter

Les indicateurs de progression (`CircularProgressIndicator` et `LinearProgressIndicator`) sont utilisés pour montrer la progression d'une tâche en cours.

### Exemple de base

```dart
CircularProgressIndicator(
  value: 0.7, // Progression de 70%
  color: Colors.blue,
)

LinearProgressIndicator(
  value: 0.5, // Progression de 50%
  backgroundColor: Colors.grey,
  valueColor: AlwaysStoppedAnimation<Color>(Colors.green),
)
```

### Personnalisation

- **value** : Valeur de progression (entre 0 et 1).
- **color** : Couleur de l'indicateur.
- **backgroundColor** : Couleur de fond de l'indicateur linéaire.

### Résumé

- Les indicateurs de progression sont utilisés pour montrer l'avancement d'une tâche.
- Ils peuvent être personnalisés avec des couleurs et des valeurs de progression.

## Boîte de dialogue d'alerte dans Flutter

La boîte de dialogue d'alerte (`AlertDialog`) est utilisée pour afficher des messages importants à l'utilisateur, souvent pour confirmer une action ou afficher une erreur.

### Exemple de base

```dart
AlertDialog(
  title: Text('Titre de l\'alerte'),
  content: Text('Ceci est un message d\'alerte.'),
  actions: <Widget>[
    TextButton(
      child: Text('Annuler'),
      onPressed: () {
        Navigator.of(context).pop();
      },
    ),
    TextButton(
      child: Text('OK'),
      onPressed: () {
        // Action à effectuer
        Navigator.of(context).pop();
      },
    ),
  ],
)
```

### Personnalisation

- **title** : Titre de la boîte de dialogue.
- **content** : Contenu de la boîte de dialogue.
- **actions** : Boutons d'action (par exemple, Annuler, OK).

### Résumé

- La boîte de dialogue d'alerte est utilisée pour afficher des messages importants.
- Elle peut inclure des boutons d'action pour interagir avec l'utilisateur.

## Dialogues dans Flutter

Les dialogues (`Dialog`) sont des fenêtres modales qui peuvent être utilisées pour afficher des informations ou des formulaires.

### Exemple de base

```dart
Dialog(
  child: Container(
    padding: EdgeInsets.all(16.0),
    child: Column(
      mainAxisSize: MainAxisSize.min,
      children: <Widget>[
        Text('Titre du dialogue'),
        Text('Contenu du dialogue'),
        TextButton(
          child: Text('Fermer'),
          onPressed: () {
            Navigator.of(context).pop();
          },
        ),
      ],
    ),
  ),
)
```

### Personnalisation

- **child** : Contenu du dialogue.
- **actions** : Boutons d'action (par exemple, Fermer).

### Résumé

- Les dialogues sont utilisés pour afficher des informations ou des formulaires de manière modale.
- Ils peuvent être personnalisés avec des titres, du contenu et des boutons d'action.

## Gestion des vidéos dans Flutter

Flutter permet de gérer les vidéos en utilisant des packages comme `video_player` pour lire des vidéos dans votre application.

### Exemple de base

```dart
import 'package:video_player/video_player.dart';

class VideoPlayerExample extends StatefulWidget {
  @override
  _VideoPlayerExampleState createState() => _VideoPlayerExampleState();
}

class _VideoPlayerExampleState extends State<VideoPlayerExample> {
  VideoPlayerController _controller;

  @override
  void initState() {
    super.initState();
    _controller = VideoPlayerController.network('https://example.com/video.mp4')
      ..initialize().then((_) {
        setState(() {});
        _controller.play();
      });
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: _controller.value.isInitialized
          ? AspectRatio(
              aspectRatio: _controller.value.aspectRatio,
              child: VideoPlayer(_controller),
            )
          : CircularProgressIndicator(),
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

### Personnalisation

- **VideoPlayerController** : Contrôleur pour gérer la lecture de la vidéo.
- **VideoPlayer** : Widget pour afficher la vidéo.

### Résumé

- Flutter permet de lire des vidéos en utilisant des packages comme `video_player`.
- Vous pouvez personnaliser la lecture et l'affichage des vidéos.

## Carte à volet extensible (Expansion Tile Card) dans Flutter

La `ExpansionTile` est utilisée pour créer des cartes qui peuvent être développées pour afficher plus d'informations.

### Exemple de base

```dart
ExpansionTile(
  title: Text('Titre de la carte'),
  children: <Widget>[
    ListTile(
      title: Text('Contenu de la carte'),
    ),
  ],
)
```

### Personnalisation

- **title** : Titre de la carte.
- **children** : Contenu à afficher lorsque la carte est développée.

### Résumé

- La `ExpansionTile` est utilisée pour créer des cartes extensibles.
- Elle permet d'afficher des informations supplémentaires de manière interactive.

## Onglets dans Flutter

Les onglets (`TabBar` et `TabBarView`) sont utilisés pour créer des interfaces à onglets, permettant aux utilisateurs de naviguer entre différentes sections.

### Exemple de base

```dart
DefaultTabController(
  length: 3,
  child: Scaffold(
    appBar: AppBar(
      bottom: TabBar(
        tabs: [
          Tab(icon: Icon(Icons.home)),
          Tab(icon: Icon(Icons.business)),
          Tab(icon: Icon(Icons.school)),
        ],
      ),
    ),
    body: TabBarView(
      children: [
        Center(child: Text('Onglet 1')),
        Center(child: Text('Onglet 2')),
        Center(child: Text('Onglet 3')),
      ],
    ),
  ),
)
```

### Personnalisation

- **length** : Nombre d'onglets.
- **tabs** : Liste des onglets à afficher.
- **children** : Contenu de chaque onglet.

### Résumé

- Les onglets sont utilisés pour créer des interfaces à onglets.
- Ils permettent aux utilisateurs de naviguer entre différentes sections de l'application.

## Liste horizontale dans Flutter

La liste horizontale (`ListView` avec `scrollDirection: Axis.horizontal`) permet de créer une liste d'éléments qui défile horizontalement.

### Exemple de base

```dart
ListView(
  scrollDirection: Axis.horizontal,
  children: <Widget>[
    Container(
      width: 160.0,
      color: Colors.red,
      child: Center(child: Text('Item 1')),
    ),
    Container(
      width: 160.0,
      color: Colors.blue,
      child: Center(child: Text('Item 2')),
    ),
    Container(
      width: 160.0,
      color: Colors.green,
      child: Center(child: Text('Item 3')),
    ),
  ],
)
```

### Personnalisation

- **scrollDirection** : Direction de défilement (horizontal ou vertical).
- **children** : Liste des éléments à afficher.

### Résumé

- La liste horizontale est utilisée pour créer des listes qui défilent horizontalement.
- Elle est idéale pour afficher des éléments comme des images ou des cartes.

## Travailler avec des graphiques dans Flutter

Flutter permet de créer des graphiques en utilisant des packages comme `fl_chart` pour afficher des données sous forme de graphiques.

### Exemple de base

```dart
import 'package:fl_chart/fl_chart.dart';

LineChart(
  LineChartData(
    // Configuration du graphique
  ),
)
```

### Personnalisation

- **LineChartData** : Configuration des données du graphique.
- **BarChart** : Pour créer des graphiques en barres.

### Résumé

- Flutter permet de créer des graphiques interactifs en utilisant des packages comme `fl_chart`.
- Vous pouvez personnaliser les graphiques pour afficher des données de manière visuelle.

## Barre de navigation inférieure convexe (Convex Bottombar) dans Flutter

La `Convex Bottombar` est une barre de navigation inférieure avec un design convexe, offrant une expérience utilisateur moderne.

### Exemple de base

```dart
ConvexAppBar(
  items: [
    TabItem(icon: Icons.home, title: 'Accueil'),
    TabItem(icon: Icons.map, title: 'Carte'),
    TabItem(icon: Icons.people, title: 'Profil'),
  ],
  onTap: (int i) => print('Tapped index: $i'),
)
```

### Personnalisation

- **items** : Liste des éléments de la barre de navigation.
- **onTap** : Fonction appelée lorsqu'un élément est touché.

### Résumé

- La `Convex Bottombar` est utilisée pour créer une barre de navigation inférieure avec un design convexe.
- Elle offre une expérience utilisateur moderne et interactive.

## Glissable (Slidable) dans Flutter

Le widget `Slidable` permet de créer des éléments de liste qui peuvent être glissés pour révéler des actions.

### Exemple de base

```dart
Slidable(
  actionPane: SlidableDrawerActionPane(),
  actionExtentRatio: 0.25,
  child: Container(
    color: Colors.white,
    child: ListTile(
      title: Text('Élément glissable'),
    ),
  ),
  actions: <Widget>[
    IconSlideAction(
      caption: 'Supprimer',
      color: Colors.red,
      icon: Icons.delete,
      onTap: () => print('Supprimer'),
    ),
  ],
)
```

### Personnalisation

- **actionPane** : Configuration du panneau d'action.
- **actions** : Liste des actions à afficher lors du glissement.

### Résumé

- Le widget `Slidable` est utilisé pour créer des éléments de liste interactifs.
- Il permet de révéler des actions en glissant l'élément.

## Snackbar dans Flutter

Le `Snackbar` est un widget qui affiche un message temporaire en bas de l'écran, souvent utilisé pour informer l'utilisateur d'une action.

### Exemple de base

```dart
Scaffold(
  body: Center(
    child: ElevatedButton(
      child: Text('Afficher Snackbar'),
      onPressed: () {
        ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(
            content: Text('Ceci est un Snackbar'),
            duration: Duration(seconds: 3),
          ),
        );
      },
    ),
  ),
)
```

### Personnalisation

- **content** : Contenu du Snackbar.
- **duration** : Durée d'affichage du Snackbar.

### Résumé

- Le `Snackbar` est utilisé pour afficher des messages temporaires.
- Il est idéal pour informer l'utilisateur d'une action ou d'un événement.
