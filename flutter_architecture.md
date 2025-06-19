# Architecture de Flutter

Flutter est un framework UI open-source développé par Google pour créer des applications multiplateformes. Son architecture repose sur plusieurs couches qui facilitent la création d'interfaces performantes et réactives.

## Architecture de base de Flutter

1. **Dart Framework**

   - Widgets (StatelessWidget, StatefulWidget)
   - Gestion de l’état (State, InheritedWidget, Provider, etc.)

2. **Engine**

   - Écrit en C++, gère le rendu (Skia), l’accès au système, etc.

3. **Embedder**
   - Interface avec la plateforme cible (Android, iOS, Web, Desktop).

## Architectures d’application dans Flutter

### 1. Architecture MVC (Model-View-Controller)

- Sépare la logique métier (Model), l’interface utilisateur (View) et la gestion des interactions (Controller).
- Peu utilisée dans Flutter à cause de la nature déclarative des widgets.

### 2. Architecture MVVM (Model-View-ViewModel)

- Utilise des ViewModels pour gérer l’état et la logique métier.
- Peut être implémentée avec des outils comme `Provider` ou `Riverpod`.

### 3. Architecture BLoC (Business Logic Component)

- Sépare la logique métier de l’UI via des streams et des sinks.
- Utilise des packages comme `bloc` ou `flutter_bloc`.

### 4. Clean Architecture (Architecture propre)

- Proposée par Robert C. Martin (Uncle Bob).
- Sépare l’application en couches indépendantes :
  - **Presentation** : UI et gestion de l’état.
  - **Domain** : Logique métier pure (use cases, entités).
  - **Data** : Accès aux données (API, base de données).

#### Exemple de structure Clean Architecture

```
lib/
├── data/
│   └── repositories/
├── domain/
│   ├── entities/
│   └── usecases/
├── presentation/
│   ├── blocs/
│   └── pages/
└── main.dart
```

## Pourquoi choisir la Clean Architecture ?

- **Testabilité** : Chaque couche peut être testée indépendamment.
- **Scalabilité** : Facilite l’évolution du projet.
- **Maintenance** : Le code est mieux organisé et plus facile à comprendre.

## Conclusion

Adopter une architecture adaptée comme la Clean Architecture dans Flutter permet de structurer son code, d’améliorer la maintenabilité et de faciliter la collaboration en équipe.
