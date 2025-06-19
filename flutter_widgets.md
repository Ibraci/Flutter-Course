# Flutter - Widgets

Dans cette section, vous allez explorer les widgets Flutter, qui sont des éléments préconçus utilisés pour construire les interfaces utilisateur dans les applications Flutter. Les widgets dans Flutter sont polyvalents et personnalisables, allant des composants de base comme les boutons et les champs de texte jusqu'aux mises en page complexes et aux animations. Flutter offre une riche bibliothèque de widgets intégrés que les développeurs peuvent utiliser directement ou personnaliser pour répondre à des besoins de conception spécifiques.

## Comprendre les Widgets dans Flutter

### Définition

En Flutter, **tout est widget**. Un widget est une classe qui décrit une partie de l'interface utilisateur en termes de configuration et de comportement. Les widgets ne dessinent pas directement à l'écran : ils sont des descriptions immuables de l'UI. Flutter se charge de convertir cet arbre de widgets en éléments visuels à l'aide du moteur de rendu.

> **À retenir** : Un widget = une description déclarative d'un élément d'interface.

### Architecture et rôle des widgets

- **Arbre de widgets** : L'UI Flutter est structurée comme un arbre, chaque nœud étant un widget. Cela permet une composition hiérarchique et modulaire.
- **Immutabilité** : Les widgets sont immuables. Pour refléter un changement (ex : interaction utilisateur), Flutter reconstruit une nouvelle arborescence de widgets.
- **Séparation configuration/état** : Les widgets (Stateless ou Stateful) séparent la configuration (propriétés) de l'état (State).

### Catégories de widgets

#### Widgets de structure et de mise en page
- **Container, Padding, Align, Center, SizedBox, Stack, Row, Column, Expanded, Flexible**
- Permettent d'organiser, positionner et dimensionner les éléments.

#### Widgets de contenu
- **Text, Image, Icon, RichText, Placeholder**
- Affichent des données ou des médias.

#### Widgets interactifs (Input & Contrôles)
- **ElevatedButton, TextButton, IconButton, GestureDetector, TextField, Checkbox, Switch, Slider, Radio**
- Permettent l'interaction utilisateur.

#### Widgets de navigation
- **AppBar, Drawer, BottomNavigationBar, TabBar, Navigator, PageView**
- Gèrent la navigation et la structure globale de l'application.

#### Widgets de style et de thème
- **Theme, DefaultTextStyle, MediaQuery, Directionality**
- Appliquent des styles globaux ou contextuels.

#### Widgets d'animation et d'effet
- **AnimatedContainer, AnimatedOpacity, Hero, FadeTransition, ScaleTransition**
- Ajoutent des animations et transitions.

### Design Systems dans Flutter

Flutter propose deux design systems principaux :

- **Material Design** (Android/Google) : widgets commençant par `Material`, ex : `Scaffold`, `AppBar`, `FloatingActionButton`, `Card`, etc.
- **Cupertino** (iOS/Apple) : widgets commençant par `Cupertino`, ex : `CupertinoButton`, `CupertinoNavigationBar`, etc.

Vous pouvez :
- Utiliser un design system natif selon la plateforme
- Mélanger les deux
- Créer votre propre design system en composant des widgets personnalisés

### Types de widgets

- **StatelessWidget** : ne possède pas d'état interne. Idéal pour les éléments statiques ou dont l'état est géré en externe.
- **StatefulWidget** : possède un état mutable via la classe associée `State<T>`. Utilisé pour les éléments dynamiques (ex : champs de saisie, animations, etc.).

#### Cycle de vie d'un StatefulWidget
- `createState()`
- `initState()`
- `build()`
- `didUpdateWidget()`
- `setState()`
- `dispose()`

### Composition et bonnes pratiques

- **Composition** : Composez des widgets simples pour créer des interfaces complexes (principe du "lego").
- **Réutilisabilité** : Créez des widgets personnalisés pour factoriser votre code.
- **Responsivité** : Utilisez des widgets adaptatifs (`LayoutBuilder`, `MediaQuery`) pour gérer différentes tailles d'écran.
- **Performance** : Privilégiez la composition à l'héritage, limitez la profondeur de l'arbre, utilisez les widgets const quand possible.

### Exemple professionnel : Carte de profil interactive

```dart
import 'package:flutter/material.dart';

class CarteProfil extends StatelessWidget {
  final String nom;
  final String imageUrl;
  final String description;
  final VoidCallback onContact;

  const CarteProfil({
    required this.nom,
    required this.imageUrl,
    required this.description,
    required this.onContact,
    Key? key,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 4,
      margin: const EdgeInsets.all(16),
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)),
      child: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            CircleAvatar(
              radius: 40,
              backgroundImage: NetworkImage(imageUrl),
            ),
            const SizedBox(height: 16),
            Text(
              nom,
              style: Theme.of(context).textTheme.headline6,
            ),
            const SizedBox(height: 8),
            Text(
              description,
              style: Theme.of(context).textTheme.bodyText2,
              textAlign: TextAlign.center,
            ),
            const SizedBox(height: 16),
            ElevatedButton.icon(
              onPressed: onContact,
              icon: const Icon(Icons.mail),
              label: const Text('Contacter'),
            ),
          ],
        ),
      ),
    );
  }
}
```

**Utilisation :**
```dart
CarteProfil(
  nom: 'Alice Dupont',
  imageUrl: 'https://randomuser.me/api/portraits/women/1.jpg',
  description: 'Développeuse Flutter passionnée par le design et l'UX.',
  onContact: () => print('Contact demandé'),
)
```

---

### Résumé

- Les widgets sont la pierre angulaire de Flutter, permettant une composition flexible et puissante de l'UI.
- Il existe de nombreuses catégories de widgets, couvrant tous les besoins d'une application moderne.
- Flutter s'appuie sur des design systems robustes, mais permet aussi la personnalisation totale.
- La maîtrise des widgets et de leur composition est essentielle pour créer des applications performantes, maintenables et élégantes.

## Flutter – Stateful vs Stateless Widgets

## Différence fondamentale entre StatelessWidget et StatefulWidget

Un **StatelessWidget** est un widget dont l'interface ne dépend que de ses propriétés (paramètres) et ne change jamais après sa création. Il est **immuable** : une fois construit, il ne peut pas changer d'apparence ou de comportement, sauf si Flutter le reconstruit avec de nouvelles propriétés.

**Cas d'usage typiques :**
- Affichage de texte statique
- Boutons sans état interne
- Icônes, images, logos, etc.

**Exemple :**
```dart
import 'package:flutter/material.dart';

class MonStatelessWidget extends StatelessWidget {
  final String message;

  const MonStatelessWidget({required this.message, Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Text(
      message,
      style: TextStyle(fontSize: 24, color: Colors.blue),
    );
  }
}

// Utilisation :
MonStatelessWidget(message: 'Bonjour, Flutter !')
```

---

Un **StatefulWidget** est un widget qui peut changer d'apparence ou de comportement en réponse à des interactions utilisateur ou à des événements asynchrones. Il possède un **état interne** (State) qui peut évoluer au fil du temps grâce à la méthode `setState()`.

**Cas d'usage typiques :**
- Champs de saisie (TextField)
- Boutons à bascule (Switch, Checkbox)
- Listes dynamiques, compteurs, animations, etc.

**Exemple :**
```dart
import 'package:flutter/material.dart';

class MonStatefulWidget extends StatefulWidget {
  const MonStatefulWidget({Key? key}) : super(key: key);

  @override
  _MonStatefulWidgetState createState() => _MonStatefulWidgetState();
}

class _MonStatefulWidgetState extends State<MonStatefulWidget> {
  int compteur = 0;

  void _incrementer() {
    setState(() {
      compteur++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text(
          'Compteur : $compteur',
          style: TextStyle(fontSize: 24, color: Colors.green),
        ),
        ElevatedButton(
          onPressed: _incrementer,
          child: Text('Incrémenter'),
        ),
      ],
    );
  }
}

// Utilisation :
MonStatefulWidget()
```

---

### Résumé

|                | StatelessWidget                | StatefulWidget                  |
|----------------|-------------------------------|---------------------------------|
| **État interne** | Non (immuable)                | Oui (mutable via State)         |
| **Usage**        | UI statique                   | UI dynamique/interactive        |
| **Exemple**      | Texte, icône, logo            | Compteur, formulaire, animation |

---

**À retenir :**
- Utilisez un `StatelessWidget` pour les éléments qui ne changent jamais après leur création.
- Utilisez un `StatefulWidget` pour les éléments qui doivent réagir à des interactions ou des changements d'état.


## MaterialApp class in Flutter

`MaterialApp` est le widget racine d'une application Flutter utilisant le design system Material. Il configure le thème, la navigation, la gestion des routes, la langue, etc.

**Principaux usages :**
- Définir le thème global (couleurs, polices)
- Gérer la navigation et les routes
- Définir la page d'accueil (`home`)

**Exemple :**
```dart
MaterialApp(
  title: 'Ma première app Flutter',
  theme: ThemeData(primarySwatch: Colors.blue),
  home: HomePage(),
  debugShowCheckedModeBanner: false,
)
```

## Scaffold class in Flutter

`Scaffold` fournit la structure de base d'une page Material : barre d'applications, tiroir, bouton flottant, etc. Il facilite la mise en page cohérente des écrans.

**Principaux usages :**
- Ajouter une `AppBar`, un `Drawer`, un `FloatingActionButton`
- Gérer le corps de la page (`body`)

**Exemple :**
```dart
Scaffold(
  appBar: AppBar(title: Text('Accueil')),
  body: Center(child: Text('Bienvenue !')),
  floatingActionButton: FloatingActionButton(
    onPressed: () {},
    child: Icon(Icons.add),
  ),
)
```

## Flutter - AppBar Widget

`AppBar` est la barre supérieure d'une page, affichant le titre, des actions, des icônes ou un menu.

**Principaux usages :**
- Afficher le titre de la page
- Ajouter des boutons d'action (icônes, menus)
- Intégrer un bouton de navigation (menu, retour)

**Exemple :**
```dart
AppBar(
  title: Text('Mon Application'),
  actions: [
    IconButton(
      icon: Icon(Icons.search),
      onPressed: () {},
    ),
  ],
)
```

## Flutter – FloatingActionButton

`FloatingActionButton` (FAB) est un bouton circulaire flottant, utilisé pour l'action principale d'un écran.

**Principaux usages :**
- Déclencher une action importante (ajout, création)
- Mettre en avant une fonctionnalité clé

**Exemple :**
```dart
FloatingActionButton(
  onPressed: () {
    // Action à effectuer
  },
  child: Icon(Icons.add),
  tooltip: 'Ajouter',
)
```

## BottomNavigationBar Widget in Flutter

`BottomNavigationBar` affiche une barre de navigation en bas de l'écran, permettant de passer d'une section à l'autre.

**Principaux usages :**
- Navigation entre 2 à 5 sections principales
- Affichage d'icônes et de labels

**Exemple :**
```dart
BottomNavigationBar(
  currentIndex: 0,
  onTap: (index) {
    // Changer de page
  },
  items: [
    BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Accueil'),
    BottomNavigationBarItem(icon: Icon(Icons.settings), label: 'Paramètres'),
  ],
)
```

## Drawer Widget in Flutter

`Drawer` est un panneau latéral coulissant, souvent utilisé pour la navigation ou l'accès à des options secondaires.

**Principaux usages :**
- Afficher un menu de navigation
- Proposer des liens vers des pages secondaires

**Exemple :**
```dart
Drawer(
  child: ListView(
    children: [
      DrawerHeader(child: Text('Menu')),
      ListTile(
        leading: Icon(Icons.home),
        title: Text('Accueil'),
        onTap: () {},
      ),
    ],
  ),
)
```

## Container class in Flutter

`Container` est un widget polyvalent pour la mise en page : il permet de définir la taille, la marge, la couleur, la bordure, etc.

**Principaux usages :**
- Encapsuler et styliser d'autres widgets
- Gérer l'espacement, l'alignement, la décoration

**Exemple :**
```dart
Container(
  padding: EdgeInsets.all(16),
  margin: EdgeInsets.symmetric(vertical: 8),
  decoration: BoxDecoration(
    color: Colors.blue[100],
    borderRadius: BorderRadius.circular(12),
  ),
  child: Text('Contenu du container'),
)
```

## Flutter – SizedBox Widget

`SizedBox` permet de créer un espace vide ou de forcer une taille précise à un widget enfant.

**Principaux usages :**
- Ajouter de l'espace entre les widgets
- Contraindre la taille d'un widget

**Exemple :**
```dart
SizedBox(height: 20), // Espace vertical
SizedBox(width: 100, child: ElevatedButton(onPressed: () {}, child: Text('OK')))
```

## ClipRRect Widget in Flutter

`ClipRRect` permet de découper (clipper) un widget enfant avec des coins arrondis.

**Principaux usages :**
- Afficher des images ou des widgets avec des bords arrondis

**Exemple :**
```dart
ClipRRect(
  borderRadius: BorderRadius.circular(16),
  child: Image.network('https://picsum.photos/200'),
)
```

## Flutter - RichText Widget

`RichText` permet d'afficher du texte avec plusieurs styles (gras, couleur, taille, etc.) dans une même ligne ou paragraphe.

**Principaux usages :**
- Mélanger différents styles dans un même texte
- Créer des liens ou des effets de texte avancés

**Exemple :**
```dart
RichText(
  text: TextSpan(
    text: 'Flutter ',
    style: TextStyle(color: Colors.black, fontSize: 18),
    children: [
      TextSpan(
        text: 'est ',
        style: TextStyle(fontWeight: FontWeight.bold),
      ),
      TextSpan(
        text: 'génial !',
        style: TextStyle(color: Colors.blue),
      ),
    ],
  ),
)
```

## ListView Class in Flutter

`ListView` est un widget de liste déroulante, idéal pour afficher un grand nombre d'éléments de façon performante.

**Principaux usages :**
- Afficher des listes dynamiques ou statiques
- Gérer le défilement vertical ou horizontal

**Exemple :**
```dart
ListView.builder(
  itemCount: 10,
  itemBuilder: (context, index) => ListTile(
    leading: Icon(Icons.person),
    title: Text('Utilisateur $index'),
  ),
)
```

## Flutter – GridView

`GridView` est un widget de grille, idéal pour afficher un grand nombre d'éléments dans une grille.

**Principaux usages :**
- Afficher des éléments dans une grille
- Gérer le défilement vertical ou horizontal

**Exemple :**
```dart
GridView.count(
  crossAxisCount: 2,
  children: List.generate(20, (index) => ListTile(
    leading: Icon(Icons.person),
    title: Text('Utilisateur $index'),
  )),
)
```

## Flutter - TextField