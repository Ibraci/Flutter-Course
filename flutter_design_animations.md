# Flutter - Design & Animations

Dans cette section, vous apprendrez à utiliser ces widgets pour concevoir des boutons, des champs de texte et d'autres éléments qui s'affichent parfaitement sur les appareils Android et iOS. De plus, les puissantes capacités d'animation de Flutter vous permettent de créer des transitions fluides et des effets interactifs, améliorant ainsi l'expérience utilisateur.

## Personnalisation des polices dans Flutter

La personnalisation des polices dans Flutter est essentielle pour créer une identité visuelle unique pour votre application. Vous pouvez utiliser des polices personnalisées, modifier la taille et le style des textes, et intégrer des polices Google.

### Utilisation de polices personnalisées

Pour utiliser une police personnalisée, vous devez d'abord l'ajouter à votre projet. Voici comment procéder :

1. **Ajoutez la police à votre projet** : Placez le fichier de police (par exemple, `Roboto.ttf`) dans un dossier `fonts` à la racine de votre projet.

2. **Déclarez la police dans `pubspec.yaml`** :

```yaml
flutter:
  fonts:
    - family: Roboto
      fonts:
        - asset: fonts/Roboto.ttf
```

3. **Utilisez la police dans votre application** :

```dart
Text(
  'Ceci est un texte avec une police personnalisée',
  style: TextStyle(
    fontFamily: 'Roboto',
    fontSize: 20,
    fontWeight: FontWeight.bold,
  ),
)
```

### Utilisation des polices Google

Flutter permet d'utiliser facilement les polices Google. Voici comment les intégrer :

1. **Ajoutez la dépendance `google_fonts` dans `pubspec.yaml`** :

```yaml
dependencies:
  google_fonts: ^2.1.0
```

2. **Utilisez la police Google dans votre application** :

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

- La personnalisation des polices permet de créer une identité visuelle unique.
- Vous pouvez utiliser des polices personnalisées et des polices Google pour améliorer le design de votre application.

## Flutter - Thèmes

Les thèmes dans Flutter permettent de définir un style cohérent pour toute l'application. Cela facilite la maintenance et l'évolution du design.

### Création d'un thème

Voici comment créer un thème de base dans Flutter :

```dart
MaterialApp(
  theme: ThemeData(
    primarySwatch: Colors.blue,
    brightness: Brightness.light,
    textTheme: TextTheme(
      headline1: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
      bodyText1: TextStyle(fontSize: 16),
    ),
  ),
  home: MyHomePage(),
)
```

### Utilisation du thème

Vous pouvez utiliser le thème dans vos widgets :

```dart
Text(
  'Ceci est un titre',
  style: Theme.of(context).textTheme.headline1,
)
```

### Résumé

- Les thèmes permettent de définir un style cohérent pour toute l'application.
- Ils facilitent la maintenance et l'évolution du design.

## Flutter - Texte à taille automatique

Le texte à taille automatique permet d'ajuster la taille du texte en fonction de l'espace disponible, ce qui est utile pour les interfaces responsives.

### Exemple de base

```dart
AutoSizeText(
  'Ceci est un texte qui s\'ajuste automatiquement à la taille disponible',
  style: TextStyle(fontSize: 20),
  minFontSize: 12,
  maxFontSize: 20,
)
```

### Résumé

- Le texte à taille automatique s'ajuste en fonction de l'espace disponible.
- Il est idéal pour les interfaces responsives.

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