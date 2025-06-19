# Routes et Navigateur dans Flutter

Route : Les applications sont la nouvelle tendance. Le nombre d'applications disponibles sur le Play Store et l'App Store de nos jours est assez important. Les applications affichent leur contenu dans un conteneur plein écran appelé pages ou écrans. Dans Flutter, les pages ou écrans sont appelés Routes. Sous Android, ces pages/écrans sont appelés Activity et sous iOS, ils sont appelés ViewController. Mais, dans Flutter, les routes sont des Widgets. Dans Flutter, une page/écran est appelée une Route.

## Création de routes dans Flutter

Une route peut être écrite sous la forme d'une "Classe" en Dart en utilisant les concepts orientés objet. Chaque route peut être écrite comme une classe séparée et possède son propre contenu et UI.

Créons maintenant deux routes, chacune ayant une AppBar et un bouton Élevé uniques. Le code est le suivant :

```dart
class HomeRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Geeks for Geeks'),
        backgroundColor: Colors.green,
      ),
      body: Center(
        child: ElevatedButton(
          child: Text('Cliquez-moi !'),
          onPressed: () {
            // Contient le code qui nous aide
            // à naviguer vers la seconde route.
          },
        ),
      ),
    );
  }
}

class SecondRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Page Cliquez-moi"),
        backgroundColor: Colors.green,
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Contient le code qui nous aide
            // à revenir à la première route.
          },
          child: Text('Accueil !'),
        ),
      ),
    );
  }
}
```

## Navigateur dans Flutter

Comme son nom l'indique, Navigator est un widget qui nous aide à naviguer entre les routes. Le navigateur suit la méthode de la pile (stack) lorsqu'il gère les routes. Selon les actions de l'utilisateur, les routes sont empilées les unes sur les autres et, lorsqu'on appuie sur retour, on revient à la route la plus récemment visitée. Navigator est un widget qui suit la discipline de la pile.

- **Définir l'accueil (Home)** : Lors de la navigation, la première chose à faire est de définir ou d'initialiser la "page d'accueil". La page d'accueil peut être n'importe quelle route selon nos besoins. L'accueil sera généralement placé en bas de la pile du navigateur. Voyons comment initialiser notre `HomeRoute()` comme page d'accueil :

```dart
void main() {
  runApp(MaterialApp(
    home: HomeRoute(),
  ));
}
```

- **Naviguer vers une page** : Puisque nous avons défini notre accueil, il ne reste plus qu'à naviguer de l'accueil vers une autre route de l'application. Pour cela, le widget Navigator possède une méthode appelée `Navigator.push()`. Cette méthode pousse la route au-dessus de l'accueil, affichant ainsi la seconde route. Le code pour empiler une route est le suivant :

```dart
// Dans le widget `HomeRoute`
onPressed: () {
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => const SecondRoute()),
  );
},
```

- **Revenir à l'accueil** : Maintenant que nous sommes arrivés à destination, comment revenir à l'accueil ? Pour cela, le navigateur possède une méthode appelée `Navigator.pop()`. Cela nous aide à retirer la route actuelle de la pile afin de revenir à notre route d'accueil. Cela peut se faire ainsi :

```dart
// Dans le widget SecondRoute
onPressed: () {
  Navigator.pop(context);
}
```

## Exemple de Routes et Navigator dans Flutter

Voici comment nous pouvons naviguer entre deux pages dans une application. Le code complet de l'application Flutter ci-dessus est le suivant :

```dart
import 'package:flutter/material.dart';
void main() {
  runApp(const MaterialApp(
    debugShowCheckedModeBanner: false,
    home: HomeRoute(),
  ));
}

class HomeRoute extends StatelessWidget {
  const HomeRoute({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Geeks for Geeks'),
        backgroundColor: Colors.green,
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: ElevatedButton(
            style: ButtonStyle(
                backgroundColor: WidgetStateProperty.all(Colors.green),
                foregroundColor: WidgetStateProperty.all(Colors.white)),
            child: const Text('Cliquez-moi !'),
            onPressed: () {
              Navigator.push(
                context,
                MaterialPageRoute(builder: (context) => const SecondRoute()),
              );
            }),
      ),
    );
  }
}

class SecondRoute extends StatelessWidget {
  const SecondRoute({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Page Cliquez-moi"),
        backgroundColor: Colors.green,
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: ElevatedButton(
          style: ButtonStyle(
              backgroundColor: WidgetStateProperty.all(Colors.green),
              foregroundColor: WidgetStateProperty.all(Colors.white)),
          onPressed: () {
            Navigator.pop(context);
          },
          child: const Text('Accueil !'),
        ),
      ),
    );
  }
}