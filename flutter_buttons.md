# Les boutons disponibles avec Flutter

## ElevatedButton

Bouton principal utilisé pour attirer l’attention sur une action importante, grâce à son effet d’élévation. Idéal pour valider ou soumettre des informations.

```dart
ElevatedButton(
    onPressed: () {
        // Action à exécuter
    },
    child: Text('Soumettre'),
)
```

## TextButton

Bouton plat sans élévation, parfait pour les actions secondaires ou les liens discrets dans l’interface, comme la navigation ou les options moins importantes.

```dart
TextButton(
    onPressed: () {
        // Action à exécuter
    },
    child: Text('Mot de passe oublié ?'),
)
```

## OutlinedButton

Bouton avec une bordure, utilisé pour des actions alternatives ou complémentaires à l’action principale, souvent placé à côté d’un bouton principal.

```dart
OutlinedButton(
    onPressed: () {
        // Action à exécuter
    },
    child: Text('Annuler'),
)
```

## IconButton

Bouton affichant uniquement une icône, idéal pour les actions rapides ou contextuelles comme aimer, partager ou rechercher.

```dart
IconButton(
    icon: Icon(Icons.favorite),
    onPressed: () {
        // Action à exécuter
    },
)
```

## FloatingActionButton

Bouton flottant circulaire, utilisé pour mettre en avant une action principale sur l’écran, comme l’ajout d’un nouvel élément.

```dart
FloatingActionButton(
    onPressed: () {
        // Action à exécuter
    },
    child: Icon(Icons.add),
)
```

## DropdownButton

Bouton permettant de sélectionner une valeur parmi plusieurs options dans une liste déroulante, pratique pour les choix uniques.

```dart
DropdownButton<String>(
    value: 'Français',
    items: <String>['Français', 'Anglais', 'Espagnol']
            .map((String value) {
        return DropdownMenuItem<String>(
            value: value,
            child: Text(value),
        );
    }).toList(),
    onChanged: (String? newValue) {
        // Action à exécuter
    },
)
```

## PopupMenuButton

Bouton qui affiche un menu contextuel d’actions supplémentaires, souvent utilisé dans les barres d’applications ou pour des options avancées.

```dart
PopupMenuButton<String>(
    onSelected: (String value) {
        // Action à exécuter
    },
    itemBuilder: (BuildContext context) => [
        PopupMenuItem(
            value: 'Option 1',
            child: Text('Option 1'),
        ),
        PopupMenuItem(
            value: 'Option 2',
            child: Text('Option 2'),
        ),
    ],
)
```

## BackButton & CloseButton

Boutons de navigation utilisés pour revenir à l’écran précédent ou fermer une page. Ils sont généralement placés dans la barre d’applications.

```dart
BackButton(
    onPressed: () {
        // Action à exécuter
    },
)

CloseButton(
    onPressed: () {
        // Action à exécuter
    },
)
```

---

**Remarque** : Tous ces boutons sont personnalisables pour s’adapter à vos besoins d’interface.
