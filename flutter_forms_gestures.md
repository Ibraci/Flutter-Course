# Formulaires et Gestes dans Flutter

Vous apprendrez à valider les entrées utilisateur et à gérer efficacement la soumission de formulaires. De plus, Flutter simplifie l’implémentation des gestes comme le tap, le swipe et le pinch, améliorant ainsi l’interaction utilisateur dans vos applications.

## Validation de formulaire dans Flutter

La validation de formulaire est une étape essentielle dans toute application. Dans Flutter, il existe plusieurs façons de valider un formulaire, comme l’utilisation d’un `TextEditingController`. Cependant, gérer un contrôleur pour chaque champ peut devenir complexe dans de grandes applications. Le widget `Form` offre une manière pratique de valider les entrées utilisateur.

Dans un formulaire, la validation s’effectue généralement dans la fonction de soumission (appelée lorsque l’utilisateur a rempli tous les champs). Chaque `TextFormField` possède une propriété `validator` qui prend une fonction de validation. Une clé globale (`GlobalKey<FormState>`) est utilisée pour accéder à l’état du formulaire et valider ou sauvegarder les champs.

### Étapes pour implémenter un formulaire dans Flutter

#### 1. Initialiser la clé globale

```dart
final _formKey = GlobalKey<FormState>();
```

#### 2. Envelopper le formulaire avec le widget `Form`

```dart
Form(
  key: _formKey,
  child: Column(
    children: <Widget>[
      // Champs du formulaire
    ],
  ),
)
```

#### 3. Valider et sauvegarder

```dart
final isValid = _formKey.currentState!.validate();
if (!isValid) {
  // Le formulaire n'est pas valide
  return;
} else {
  // Le formulaire est valide
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(
      backgroundColor: Colors.green,
      content: Text(
        "Connexion réussie",
        style: TextStyle(color: Colors.white),
      ),
    ),
  );
}
// Sauvegarder l'état du formulaire
_formKey.currentState!.save();
```

### Exemple complet de validation de formulaire

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomePage(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  final _formKey = GlobalKey<FormState>();

  void _submit() {
    final isValid = _formKey.currentState!.validate();
    if (!isValid) {
      return;
    } else {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(
          backgroundColor: Colors.green,
          content: Text(
            "Connexion réussie",
            style: TextStyle(color: Colors.white),
          ),
        ),
      );
    }
    _formKey.currentState!.save();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Validation de formulaire"),
        leading: Icon(Icons.filter_vintage),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: <Widget>[
              Text(
                "Validation de formulaire dans Flutter",
                style: TextStyle(fontSize: 24.0, fontWeight: FontWeight.bold),
              ),
              SizedBox(height: 24),
              TextFormField(
                decoration: InputDecoration(labelText: 'E-mail'),
                keyboardType: TextInputType.emailAddress,
                validator: (value) {
                  if (value == null || value.isEmpty ||
                      !RegExp(r"^[a-zA-Z0-9.a-zA-Z0-9.!#\$%&'*+-/=?^_`{|}~]+@[a-zA-Z0-9]+\.[a-zA-Z]+")
                          .hasMatch(value)) {
                    return 'Entrez un e-mail valide !';
                  }
                  return null;
                },
              ),
              SizedBox(height: 24),
              TextFormField(
                decoration: InputDecoration(labelText: 'Mot de passe'),
                obscureText: true,
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Entrez un mot de passe valide !';
                  }
                  return null;
                },
              ),
              SizedBox(height: 24),
              SizedBox(
                width: double.infinity,
                child: ElevatedButton(
                  style: ButtonStyle(
                    backgroundColor: WidgetStateProperty.all(Colors.green),
                  ),
                  child: Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: Text(
                      "Soumettre",
                      style: TextStyle(color: Colors.white, fontSize: 20),
                    ),
                  ),
                  onPressed: _submit,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## Concevoir une page de soumission de formulaire dans Flutter

Il existe plusieurs façons de soumettre des données saisies par l’utilisateur dans Flutter. La méthode la plus courante est d’utiliser des `TextFields`, mais cela nécessite un contrôleur pour chaque champ, ce qui peut devenir lourd. Le widget `Form` permet de centraliser la gestion des champs avec une seule clé globale.

### Étapes pour implémenter un formulaire

1. **Initialiser la clé globale**
   ```dart
   final _formKey = GlobalKey<FormState>();
   ```
2. **Envelopper avec le widget Form**
   ```dart
   Form(
     key: _formKey,
     child: Column(
       children: <Widget>[
         // Champs du formulaire
       ],
     ),
   )
   ```
3. **Déclarer les variables**
   ```dart
   String email = "";
   String password = "";
   ```
4. **Stocker les entrées utilisateur**
   ```dart
   TextFormField(
     decoration: InputDecoration(labelText: 'E-mail'),
     keyboardType: TextInputType.emailAddress,
     onFieldSubmitted: (value) {
       setState(() {
         email = value;
       });
     },
     validator: (value) {
       if (value == null || value.isEmpty || !value.contains('@')) {
         return 'E-mail invalide !';
       }
       return null;
     },
   ),
   ```

### Exemple complet

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "ValidationFormulaire",
      debugShowCheckedModeBanner: false,
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final GlobalKey<FormState> _formKey = GlobalKey();
  String email = "";
  String password = "";

  void _submit() {
    // Ajoutez ici votre logique de soumission
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Validation de formulaire"),
        centerTitle: true,
        backgroundColor: Colors.green,
        foregroundColor: Colors.white,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: <Widget>[
            Form(
              key: _formKey,
              child: Column(
                children: <Widget>[
                  TextFormField(
                    decoration: InputDecoration(labelText: 'E-mail'),
                    keyboardType: TextInputType.emailAddress,
                    onFieldSubmitted: (value) {
                      setState(() {
                        email = value;
                      });
                    },
                    validator: (value) {
                      if (value == null || value.isEmpty || !value.contains('@')) {
                        return 'E-mail invalide !';
                      }
                      return null;
                    },
                  ),
                  TextFormField(
                    decoration: InputDecoration(labelText: 'Mot de passe'),
                    keyboardType: TextInputType.visiblePassword,
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.length < 7) {
                        return 'Mot de passe invalide !';
                      }
                      return null;
                    },
                    onFieldSubmitted: (value) {
                      setState(() {
                        password = value;
                      });
                    },
                  ),
                  TextButton(
                    onPressed: _submit,
                    child: Text("Soumettre"),
                  ),
                ],
              ),
            ),
            SizedBox(height: 20),
            Column(
              children: <Widget>[
                email.isEmpty ? Text("Aucune donnée") : Text(email),
                SizedBox(height: 10),
                password.isEmpty ? Text("Aucune donnée") : Text(password),
              ],
            )
          ],
        ),
      ),
    );
  }
}
```

---

# Gestes dans Flutter

Les gestes sont utilisés pour interagir avec une application, en particulier sur les appareils tactiles. Cela va du simple tap à des interactions plus complexes comme le swipe, le pinch ou le scroll. Les gestes sont omniprésents dans les applications modernes.

**Gestes courants :**
- **Tap** : Appuyer brièvement sur l’écran
- **Double Tap** : Appuyer deux fois rapidement
- **Drag** : Appuyer puis déplacer le doigt
- **Flick** : Glisser rapidement
- **Pinch** : Pincer avec deux doigts
- **Zoom** : Écarter deux doigts
- **Panning** : Déplacer le doigt sans le lever

Le widget `GestureDetector` permet de détecter ces interactions et d’y associer des actions.

### Propriétés principales de GestureDetector

| Propriété         | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| `child`           | Le widget enfant à surveiller                                               |
| `onTapDown`       | Appui initial détecté                                                       |
| `onTapUp`         | Relâchement du doigt après un tap                                           |
| `onTap`           | Tap détecté                                                                 |
| `onTapCancel`     | Tap annulé                                                                 |
| `onDoubleTap`     | Double tap détecté                                                          |
| `onLongPress`     | Appui long détecté                                                          |

### Exemple d’utilisation de GestureDetector

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    const title = 'Gestes';

    return MaterialApp(
      title: title,
      home: const MyHomePage(title: title),
      debugShowCheckedModeBanner: false,
    );
  }
}

class MyHomePage extends StatelessWidget {
  final String title;

  const MyHomePage({Key? key, required this.title}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Exemple de Gestes'),
        backgroundColor: Colors.green,
        foregroundColor: Colors.white,
      ),
      body: const Center(child: MonBouton()),
    );
  }
}

class MonBouton extends StatelessWidget {
  const MonBouton({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        const snackBar = SnackBar(content: Text("Vous avez tapé sur le bouton"));
        ScaffoldMessenger.of(context).showSnackBar(snackBar);
      },
      child: Container(
        padding: const EdgeInsets.all(12.0),
        decoration: BoxDecoration(
          color: Colors.green,
          borderRadius: BorderRadius.circular(8.0),
        ),
        child: const Text(
          'Bouton tactile',
          style: TextStyle(color: Colors.white),
        ),
      ),
    );
  }
}
```