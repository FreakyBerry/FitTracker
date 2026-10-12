# FitTracker

## Objectif

FitTracker est une application mobile cross-platform (iOS / Android) de suivi d'entraînement de musculation. Elle permet de :

- Enregistrer ses séances d'entraînement
- Suivre les exercices réalisés, avec le nombre de séries et de répétitions (et les charges utilisées)
- Planifier quelles séances faire sur quels jours de la semaine
- Consulter l'historique et la progression dans le temps

## Stack technique (choix initial)

- **React Native** (via Expo) pour une base de code unique entre iOS et Android

De nombreux autres choix techniques restent à trancher (voir ci-dessous).

## Questions techniques à trancher

Cette section liste les décisions techniques encore ouvertes. Chaque question devra être tranchée avant ou pendant le développement des fonctionnalités correspondantes.

### 1. Données & stockage

- Stockage **local uniquement** (SQLite embarqué) ou **synchronisation cloud** (multi-appareils, sauvegarde) ?
- Si cloud : quel backend ? (Supabase, Firebase, backend custom, autre ?)
- Si local : SQLite brut (`expo-sqlite`) ou via un ORM (Drizzle, WatermelonDB, autre) ?
- Faut-il prévoir un export/import des données (JSON, CSV) pour sauvegarde manuelle ou changement d'appareil ?
- Faut-il un mode **hors-ligne** complet, même si on choisit une synchro cloud (stratégie offline-first) ?

### 2. Authentification & comptes

- L'appli nécessite-t-elle un compte utilisateur, ou reste-t-elle mono-utilisateur sans login ?
- Si compte : email/mot de passe, ou connexion via un provider (Google, Apple, autre) ?
- Apple impose une connexion "Sign in with Apple" si on propose d'autres logins sociaux sur iOS — à anticiper si authentification sociale.
- Faut-il gérer plusieurs profils sur un même appareil (ex. usage familial) ?

### 3. Modèle de données métier

- Comment modéliser un **exercice** : bibliothèque prédéfinie, exercices personnalisés, ou les deux ?
- Une **séance** est-elle un modèle figé (template réutilisable chaque semaine) ou une séance = une séance (instance unique à chaque fois) ? Ou les deux (template + instances générées) ?
- Quelles unités gérer (kg/lb, répétitions, temps de repos, RPE/RIR) ? Faut-il les rendre configurables ?
- Faut-il gérer les supersets, circuits, ou drop sets, ou seulement des séries classiques dans un premier temps ?

### 4. Planification

- Comment représenter la planification hebdomadaire (ex. "Push/Pull/Legs" les lundi/mercredi/vendredi) ?
- Faut-il des rappels/notifications pour les séances planifiées ?
- Faut-il gérer les cycles d'entraînement (mésocycles, périodisation) ou rester simple au départ ?

### 5. Navigation & UX

- Quelle librairie de navigation ? (React Navigation étant le standard avec Expo)
- Design system : composants custom, ou librairie UI (React Native Paper, Tamagui, NativeBase, autre) ?
- Faut-il un mode sombre dès le départ ?

### 6. Statistiques & historique

- Quelles statistiques afficher (volume total, 1RM estimé, progression par exercice, graphiques) ?
- Quelle librairie de graphiques (Victory Native, React Native SVG Charts, autre) ?

### 7. Plateformes & distribution

- Cibles : iOS et Android dès le départ, ou un seul OS en premier (MVP) ?
- Utilisation d'Expo managed workflow, ou besoin anticipé de code natif custom (Expo bare / modules natifs) ?
- Build & déploiement : EAS Build/Submit ? Publication sur App Store / Play Store envisagée, ou usage perso uniquement (build de dev/TestFlight) ?

### 8. Langage & outillage

- TypeScript ou JavaScript ?
- Gestion d'état : Context API natif, Zustand, Redux, Jotai, autre ?
- Tests : faut-il mettre en place des tests (unitaires, end-to-end avec Detox/Maestro) dès le début ?

### 9. Internationalisation

- L'appli doit-elle supporter plusieurs langues dès le départ, ou français uniquement pour l'instant ?

## Prochaines étapes

Répondre aux questions ci-dessus, section par section, afin de figer une architecture technique avant de commencer le développement des fonctionnalités.
