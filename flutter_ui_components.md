# Flutter UI Components

Dans ce chapitre, nous allons explorer les différents composants d'interface utilisateur (UI) disponibles dans Flutter. Ces composants sont essentiels pour créer des applications mobiles interactives et visuellement attrayantes.

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

Expanded Class in Flutter
Flutter – Checkbox Widget
Flutter - Carousel Slider
Flutter - Staggered Grid View
Flutter - Circular & Linear Progress Indicators
Alert Dialog box in Flutter
Flutter - Dialogs
Flutter - Handling videos
Flutter - Expansion Tile Card
Flutter - Tabs
Flutter - Horizontal List
Flutter - Working with Charts
Flutter - Convex Bottombar
Flutter - Slidable
Flutter – Snackbar