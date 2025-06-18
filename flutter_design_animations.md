# Flutter - Design & Animations

Dans cette section, vous apprendrez à utiliser ces widgets pour concevoir des boutons, des champs de texte et d'autres éléments qui s'affichent parfaitement sur les appareils Android et iOS. De plus, les puissantes capacités d'animation de Flutter vous permettent de créer des transitions fluides et des effets interactifs, améliorant ainsi l'expérience utilisateur.

## Personnalisation des polices dans Flutter

La personnalisation des polices dans Flutter est essentielle pour créer une identité visuelle unique pour votre application. Une bonne typographie peut améliorer considérablement l'expérience utilisateur et la lisibilité de votre application.

### Pourquoi personnaliser les polices ?

- **Identité visuelle** : Les polices personnalisées aident à établir une identité de marque cohérente
- **Lisibilité** : Certaines polices sont plus lisibles que d'autres selon le contexte
- **Performance** : Les polices optimisées peuvent améliorer les performances de l'application
- **Accessibilité** : Des polices bien choisies améliorent l'accessibilité de l'application

### Utilisation de polices personnalisées

#### 1. Ajout de polices personnalisées

Pour utiliser une police personnalisée, suivez ces étapes :

1. **Créez un dossier `fonts`** à la racine de votre projet
2. **Ajoutez vos fichiers de police** (par exemple, `Roboto.ttf`, `Montserrat.ttf`)
3. **Déclarez les polices dans `pubspec.yaml`** :

```yaml
flutter:
  fonts:
    - family: Roboto
      fonts:
        - asset: fonts/Roboto-Regular.ttf
        - asset: fonts/Roboto-Bold.ttf
          weight: 700
        - asset: fonts/Roboto-Light.ttf
          weight: 300
    - family: Montserrat
      fonts:
        - asset: fonts/Montserrat-Regular.ttf
```

#### 2. Utilisation dans l'application

```dart
// Utilisation simple
Text(
  'Ceci est un texte avec une police personnalisée',
  style: TextStyle(
    fontFamily: 'Roboto',
    fontSize: 20,
    fontWeight: FontWeight.bold,
  ),
)

// Utilisation avec différents styles
Text(
  'Texte en gras',
  style: TextStyle(
    fontFamily: 'Roboto',
    fontWeight: FontWeight.bold,
  ),
)

Text(
  'Texte léger',
  style: TextStyle(
    fontFamily: 'Roboto',
    fontWeight: FontWeight.w300,
  ),
)
```

### Utilisation des polices Google

Les polices Google offrent une grande variété de styles et sont facilement intégrables dans Flutter.

#### 1. Configuration

1. **Ajoutez la dépendance** dans `pubspec.yaml` :

```yaml
dependencies:
  google_fonts: ^2.1.0
```

2. **Importez le package** :

```dart
import 'package:google_fonts/google_fonts.dart';
```

#### 2. Exemples d'utilisation

```dart
// Utilisation simple
Text(
  'Ceci est un texte avec une police Google',
  style: GoogleFonts.lato(
    fontSize: 20,
    fontWeight: FontWeight.bold,
  ),
)

// Combinaison de styles
Text(
  'Titre principal',
  style: GoogleFonts.poppins(
    fontSize: 24,
    fontWeight: FontWeight.bold,
    color: Colors.blue,
    letterSpacing: 1.2,
  ),
)

// Utilisation avec des variantes
Text(
  'Texte italique',
  style: GoogleFonts.roboto(
    fontSize: 16,
    fontStyle: FontStyle.italic,
  ),
)
```

### Bonnes pratiques

1. **Limitez le nombre de polices** : Utilisez 2-3 polices maximum pour maintenir la cohérence
2. **Hiérarchie typographique** : Créez une hiérarchie claire avec différentes tailles et poids
3. **Performance** : Préchargez les polices si nécessaire pour éviter les flashs de texte
4. **Accessibilité** : Assurez-vous que les polices choisies sont lisibles pour tous les utilisateurs

### Exemple complet

```dart
class TypographyExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Titre principal
        Text(
          'Bienvenue',
          style: GoogleFonts.poppins(
            fontSize: 32,
            fontWeight: FontWeight.bold,
            color: Colors.blue,
          ),
        ),
        
        // Sous-titre
        Text(
          'Sous-titre',
          style: GoogleFonts.poppins(
            fontSize: 24,
            fontWeight: FontWeight.w500,
            color: Colors.grey[700],
          ),
        ),
        
        // Corps de texte
        Text(
          'Ceci est un exemple de texte avec différentes polices et styles.',
          style: GoogleFonts.roboto(
            fontSize: 16,
            height: 1.5,
          ),
        ),
        
        // Texte en gras
        Text(
          'Texte important',
          style: GoogleFonts.roboto(
            fontSize: 18,
            fontWeight: FontWeight.bold,
            color: Colors.red,
          ),
        ),
      ],
    );
  }
}
```

### Résumé

- La personnalisation des polices permet de créer une identité visuelle unique
- Vous pouvez utiliser des polices personnalisées et des polices Google
- Suivez les bonnes pratiques pour une typographie efficace
- Testez vos choix de polices sur différents appareils et tailles d'écran

## Flutter - Thèmes

Les thèmes dans Flutter sont un outil puissant pour maintenir une cohérence visuelle dans votre application. Ils permettent de définir des styles globaux pour les couleurs, les textes, les boutons et autres éléments de l'interface utilisateur.

### Pourquoi utiliser des thèmes ?

- **Cohérence** : Assure une apparence uniforme dans toute l'application
- **Maintenance** : Facilite les modifications globales du design
- **Accessibilité** : Permet de gérer facilement les thèmes sombres et clairs
- **Réutilisabilité** : Les styles définis peuvent être réutilisés dans toute l'application

### Création d'un thème de base

#### 1. Définition du thème principal

```dart
MaterialApp(
  theme: ThemeData(
    // Couleurs principales
    primarySwatch: Colors.blue,
    primaryColor: Colors.blue,
    accentColor: Colors.blueAccent,
    
    // Mode clair/sombre
    brightness: Brightness.light,
    
    // Thème des textes
    textTheme: TextTheme(
      headline1: TextStyle(
        fontSize: 32,
        fontWeight: FontWeight.bold,
        color: Colors.black,
      ),
      headline2: TextStyle(
        fontSize: 24,
        fontWeight: FontWeight.w600,
        color: Colors.black87,
      ),
      bodyText1: TextStyle(
        fontSize: 16,
        color: Colors.black54,
      ),
      button: TextStyle(
        fontSize: 14,
        fontWeight: FontWeight.w500,
        color: Colors.white,
      ),
    ),
    
    // Thème des boutons
    elevatedButtonTheme: ElevatedButtonThemeData(
      style: ElevatedButton.styleFrom(
        primary: Colors.blue,
        onPrimary: Colors.white,
        padding: EdgeInsets.symmetric(horizontal: 16, vertical: 12),
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(8),
        ),
      ),
    ),
    
    // Thème des cartes
    cardTheme: CardTheme(
      elevation: 4,
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(12),
      ),
    ),
  ),
  home: MyHomePage(),
)
```

#### 2. Thème sombre

```dart
MaterialApp(
  theme: ThemeData.light(), // Thème clair par défaut
  darkTheme: ThemeData.dark().copyWith(
    primaryColor: Colors.blue,
    scaffoldBackgroundColor: Colors.grey[900],
    cardColor: Colors.grey[800],
    textTheme: TextTheme(
      headline1: TextStyle(
        fontSize: 32,
        fontWeight: FontWeight.bold,
        color: Colors.white,
      ),
      bodyText1: TextStyle(
        fontSize: 16,
        color: Colors.white70,
      ),
    ),
  ),
  themeMode: ThemeMode.system, // Suit les préférences système
  home: MyHomePage(),
)
```

### Utilisation du thème

#### 1. Accès aux styles du thème

```dart
// Dans un widget
Text(
  'Titre',
  style: Theme.of(context).textTheme.headline1,
)

// Utilisation des couleurs
Container(
  color: Theme.of(context).primaryColor,
  child: Text(
    'Contenu',
    style: TextStyle(
      color: Theme.of(context).colorScheme.onPrimary,
    ),
  ),
)
```

#### 2. Création de widgets personnalisés avec le thème

```dart
class CustomButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;

  const CustomButton({
    Key? key,
    required this.text,
    required this.onPressed,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    final theme = Theme.of(context);
    
    return ElevatedButton(
      onPressed: onPressed,
      style: theme.elevatedButtonTheme.style,
      child: Text(
        text,
        style: theme.textTheme.button,
      ),
    );
  }
}
```

### Bonnes pratiques

1. **Organisation** : Créez un fichier séparé pour votre thème
2. **Cohérence** : Utilisez des constantes pour les valeurs réutilisées
3. **Flexibilité** : Permettez la personnalisation des thèmes
4. **Accessibilité** : Assurez un bon contraste dans les thèmes clairs et sombres

### Exemple complet

```dart
// theme/app_theme.dart
class AppTheme {
  static ThemeData get lightTheme {
    return ThemeData(
      primarySwatch: Colors.blue,
      brightness: Brightness.light,
      // ... autres configurations
    );
  }

  static ThemeData get darkTheme {
    return ThemeData(
      primarySwatch: Colors.blue,
      brightness: Brightness.dark,
      // ... autres configurations
    );
  }
}

// main.dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: AppTheme.lightTheme,
      darkTheme: AppTheme.darkTheme,
      themeMode: ThemeMode.system,
      home: HomePage(),
    );
  }
}

// home_page.dart
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final theme = Theme.of(context);
    
    return Scaffold(
      appBar: AppBar(
        title: Text(
          'Accueil',
          style: theme.textTheme.headline1,
        ),
      ),
      body: Column(
        children: [
          Card(
            child: Padding(
              padding: EdgeInsets.all(16),
              child: Text(
                'Contenu de la carte',
                style: theme.textTheme.bodyText1,
              ),
            ),
          ),
          CustomButton(
            text: 'Cliquez-moi',
            onPressed: () {
              // Action
            },
          ),
        ],
      ),
    );
  }
}
```

### Résumé

- Les thèmes permettent de maintenir une cohérence visuelle dans l'application
- Ils facilitent la maintenance et les modifications globales
- Ils supportent les modes clair et sombre
- Ils peuvent être personnalisés selon les besoins de l'application

## Flutter - Texte à taille automatique

Le texte à taille automatique est une fonctionnalité essentielle pour créer des interfaces responsives qui s'adaptent à différentes tailles d'écran. Il permet d'ajuster automatiquement la taille du texte en fonction de l'espace disponible, évitant ainsi les problèmes de débordement ou de texte trop petit.

### Pourquoi utiliser le texte à taille automatique ?

- **Responsive Design** : S'adapte automatiquement à différentes tailles d'écran
- **Lisibilité** : Maintient une taille de texte lisible dans tous les cas
- **Flexibilité** : Fonctionne avec différents types de conteneurs
- **Performance** : Optimise l'espace disponible

### Installation

Pour utiliser le texte à taille automatique, ajoutez la dépendance `auto_size_text` dans votre `pubspec.yaml` :

```yaml
dependencies:
  auto_size_text: ^3.0.0
```

### Utilisation de base

#### 1. Texte simple

```dart
AutoSizeText(
  'Ceci est un texte qui s\'ajuste automatiquement à la taille disponible',
  style: TextStyle(fontSize: 20),
  minFontSize: 12,
  maxFontSize: 20,
)
```

#### 2. Texte avec contraintes

```dart
Container(
  width: 200,
  height: 100,
  child: AutoSizeText(
    'Ce texte s\'ajustera pour tenir dans ce conteneur',
    style: TextStyle(fontSize: 20),
    minFontSize: 12,
    maxLines: 2,
    overflow: TextOverflow.ellipsis,
  ),
)
```

### Options avancées

#### 1. Texte avec groupe

```dart
AutoSizeGroup(
  children: [
    AutoSizeText(
      'Premier texte',
      group: group,
      style: TextStyle(fontSize: 20),
    ),
    AutoSizeText(
      'Deuxième texte',
      group: group,
      style: TextStyle(fontSize: 20),
    ),
  ],
)
```

#### 2. Texte avec animation

```dart
AutoSizeText(
  'Texte animé',
  style: TextStyle(fontSize: 20),
  minFontSize: 12,
  maxFontSize: 20,
  animation: AutoSizeTextAnimation(
    duration: Duration(milliseconds: 300),
    curve: Curves.easeInOut,
  ),
)
```

### Cas d'utilisation courants

#### 1. Titres de cartes

```dart
Card(
  child: Padding(
    padding: EdgeInsets.all(16),
    child: Column(
      children: [
        AutoSizeText(
          'Titre de la carte qui peut être long',
          style: TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.bold,
          ),
          maxLines: 2,
          minFontSize: 16,
        ),
        // Contenu de la carte
      ],
    ),
  ),
)
```

#### 2. Boutons avec texte long

```dart
ElevatedButton(
  onPressed: () {},
  child: AutoSizeText(
    'Texte long du bouton qui doit s\'adapter',
    style: TextStyle(fontSize: 16),
    minFontSize: 12,
    maxLines: 1,
  ),
)
```

### Bonnes pratiques

1. **Définissez des limites** : Utilisez `minFontSize` et `maxFontSize` pour éviter les tailles extrêmes
2. **Gérez le débordement** : Utilisez `overflow` pour gérer les textes trop longs
3. **Optimisez les performances** : Limitez le nombre de lignes avec `maxLines`
4. **Testez sur différents appareils** : Vérifiez le comportement sur différentes tailles d'écran

### Exemple complet

```dart
class ResponsiveTextExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Titre principal
        Container(
          width: double.infinity,
          padding: EdgeInsets.all(16),
          child: AutoSizeText(
            'Titre principal qui peut être très long et doit s\'adapter',
            style: TextStyle(
              fontSize: 32,
              fontWeight: FontWeight.bold,
            ),
            minFontSize: 20,
            maxLines: 2,
            textAlign: TextAlign.center,
          ),
        ),

        // Sous-titre
        Container(
          width: 300,
          child: AutoSizeText(
            'Sous-titre avec une largeur fixe',
            style: TextStyle(
              fontSize: 24,
              color: Colors.grey[700],
            ),
            minFontSize: 16,
            maxLines: 1,
          ),
        ),

        // Texte dans une carte
        Card(
          child: Padding(
            padding: EdgeInsets.all(16),
            child: Column(
              children: [
                AutoSizeText(
                  'Contenu de la carte qui peut être très long et doit s\'adapter à l\'espace disponible',
                  style: TextStyle(fontSize: 16),
                  minFontSize: 12,
                  maxLines: 3,
                ),
                SizedBox(height: 8),
                AutoSizeText(
                  'Texte secondaire',
                  style: TextStyle(
                    fontSize: 14,
                    color: Colors.grey[600],
                  ),
                  minFontSize: 10,
                  maxLines: 1,
                ),
              ],
            ),
          ),
        ),
      ],
    );
  }
}
```

### Résumé

- Le texte à taille automatique est essentiel pour les interfaces responsives
- Il s'adapte automatiquement à l'espace disponible
- Il offre de nombreuses options de personnalisation
- Il améliore l'expérience utilisateur sur différents appareils

## Flutter - Texte squelette

Le texte squelette est utilisé comme placeholder pendant le chargement des données, améliorant ainsi l'expérience utilisateur.

### Exemple de base

```dart
SkeletonText(
  lines: 3,
  loading: true,
)
```

### Résumé

- Le texte squelette améliore l'expérience utilisateur pendant le chargement des données.
- Il peut être personnalisé pour correspondre au style de votre application.

## Flutter - Animation dans la transition de route

Les animations dans la transition de route permettent de créer des transitions fluides entre les écrans de l'application.

### Exemple de base

```dart
Navigator.push(
  context,
  PageRouteBuilder(
    pageBuilder: (context, animation, secondaryAnimation) => SecondScreen(),
    transitionsBuilder: (context, animation, secondaryAnimation, child) {
      return FadeTransition(
        opacity: animation,
        child: child,
      );
    },
  ),
)
```

### Résumé

- Les animations dans la transition de route améliorent la fluidité de la navigation.
- Elles peuvent être personnalisées pour créer des effets visuels uniques.

## Flutter - Effet de vague

L'effet de vague (ripple) est utilisé pour les boutons et autres éléments interactifs, améliorant le retour visuel lors des interactions utilisateur.

### Exemple de base

```dart
InkWell(
  onTap: () {
    // Action lors de l'appui
  },
  child: Container(
    padding: EdgeInsets.all(16),
    child: Text('Appuyez ici'),
  ),
)
```

### Résumé

- L'effet de vague améliore le retour visuel lors des interactions utilisateur.
- Il est facile à implémenter avec le widget `InkWell`.

## Flutter - Chargeur paresseux

Le chargeur paresseux permet de charger des données de manière asynchrone, améliorant ainsi les performances de l'application.

### Exemple de base

```dart
FutureBuilder<String>(
  future: fetchData(),
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.waiting) {
      return CircularProgressIndicator();
    } else if (snapshot.hasError) {
      return Text('Erreur: ${snapshot.error}');
    } else {
      return Text('Données: ${snapshot.data}');
    }
  },
)
```

### Résumé

- Le chargeur paresseux améliore les performances en chargeant les données de manière asynchrone.
- Il est facile à implémenter avec `FutureBuilder`.

## Flutter - Animation héro radiale

L'animation héro radiale permet de créer des transitions visuelles entre les écrans, en mettant en avant un élément spécifique.

### Exemple de base

```dart
Hero(
  tag: 'heroTag',
  child: Image.asset('assets/image.png'),
)
```

### Résumé

- L'animation héro radiale crée des transitions visuelles fluides entre les écrans.
- Elle est idéale pour mettre en avant des éléments spécifiques.

## Flutter - Animation de charnière

L'animation de charnière permet de créer des effets de rotation ou de pivotement.

### Exemple de base

```dart
AnimatedBuilder(
  animation: _controller,
  builder: (context, child) {
    return Transform.rotate(
      angle: _controller.value * 2 * 3.14159,
      child: Icon(Icons.rotate_right),
    );
  },
)
```

### Résumé

- L'animation de charnière permet de créer des effets de rotation.
- Elle est facile à implémenter avec `AnimatedBuilder`.

## Flutter - Animation Lottie

L'animation Lottie permet d'intégrer des animations vectorielles dans l'application, offrant ainsi des animations de haute qualité.

### Exemple de base

```dart
Lottie.asset('assets/animation.json'),
```

### Résumé

- L'animation Lottie offre des animations vectorielles de haute qualité.
- Elle est facile à intégrer dans votre application.

## Indicateur de progression dans Flutter

L'indicateur de progression est utilisé pour montrer l'avancement d'une tâche, comme le chargement de données.

### Exemple de base

```dart
CircularProgressIndicator(
  value: 0.7, // Progression de 70%
  color: Colors.blue,
)
```

### Résumé

- L'indicateur de progression montre l'avancement d'une tâche.
- Il peut être personnalisé avec des couleurs et des valeurs de progression.

## Flutter - Simulation physique dans l'animation

La simulation physique permet de créer des animations réalistes, comme des effets de rebond ou de gravité.

### Exemple de base

```dart
PhysicsSimulation(
  // Configuration de la simulation
)
```

### Résumé

- La simulation physique crée des animations réalistes.
- Elle est idéale pour des effets de rebond ou de gravité.

## Flutter - Utilisation des polices Google

L'utilisation des polices Google permet d'intégrer une grande variété de styles de texte dans votre application.

### Exemple de base

```dart
import 'package:google_fonts/google_fonts.dart';

Text(
  'Ceci est un texte avec une police Google',
  style: GoogleFonts.lato(
    fontSize: 20,
    fontWeight: FontWeight.bold,
  ),
)
```

### Résumé

- Les polices Google offrent une grande variété de styles de texte.
- Elles sont faciles à intégrer dans votre application.

## Flutter - Transition de rotation

La transition de rotation permet d'animer les changements d'état des widgets, comme la rotation d'une icône.

### Exemple de base

```dart
AnimatedBuilder(
  animation: _controller,
  builder: (context, child) {
    return Transform.rotate(
      angle: _controller.value * 2 * 3.14159,
      child: Icon(Icons.rotate_right),
    );
  },
)
```

### Résumé

- La transition de rotation anime les changements d'état des widgets.
- Elle est facile à implémenter avec `AnimatedBuilder`.

## Flutter - Écran de démarrage animé

L'écran de démarrage animé peut être utilisé pour afficher un logo ou une animation pendant le chargement de l'application.

### Exemple de base

```dart
SplashScreen(
  seconds: 3,
  navigateAfterSeconds: HomePage(),
  title: Text('Bienvenue'),
  image: Image.asset('assets/logo.png'),
  backgroundColor: Colors.white,
  styleTextUnderTheLoader: TextStyle(),
  photoSize: 100.0,
  loaderColor: Colors.blue,
)
```

### Résumé

- L'écran de démarrage animé améliore l'expérience utilisateur pendant le chargement de l'application.
- Il peut être personnalisé pour correspondre au style de votre application.

## Flutter - Effet de scintillement

L'effet de scintillement est utilisé pour attirer l'attention sur certains éléments de l'interface utilisateur.

### Exemple de base

```dart
Shimmer.fromColors(
  baseColor: Colors.grey[300],
  highlightColor: Colors.grey[100],
  child: Text('Ceci est un texte qui scintille'),
)
```

### Résumé

- L'effet de scintillement attire l'attention sur certains éléments de l'interface utilisateur.
- Il est facile à implémenter avec le widget `Shimmer`.

## Animations Rive dans Flutter

Les animations Rive permettent de créer des animations interactives et personnalisées dans l'application.

### Exemple de base

```dart
RiveAnimation.asset('assets/animation.riv'),
```

### Résumé

- Les animations Rive offrent des animations interactives et personnalisées.
- Elles sont faciles à intégrer dans votre application.