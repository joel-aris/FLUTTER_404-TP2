FLUTTER_404-TP2
Application Flutter de Gestion de Produits avec Authentification Multi-Providers

FLUTTER_404-TP2 est une application mobile moderne développée avec Flutter, conçue pour la gestion de produits avec un système d’authentification sécurisé multi-providers et un stockage temps réel via Firebase Firestore.

Ce projet met en œuvre des standards professionnels de développement mobile, incluant la séparation des responsabilités, la persistance de session, la sécurité des données et une architecture claire et maintenable.

Équipe de développement

Ce projet a été conçu et réalisé par :

Bukasa Shimatu Junior

Lolonga Epanda Roger

Mukendi Mulu Joel

Ngandu Kashinda Franck

Pini Mpanza Kevin

Dépôt GitHub

Code source officiel :
https://github.com/joel-aris/FLUTTER_404-TP2

Fonctionnalités principales
Authentification utilisateur

Inscription et connexion par email et mot de passe

Authentification via Google

Authentification via X (Twitter)

Persistance de session via SharedPreferences

Gestion sécurisée des sessions utilisateurs

Gestion des produits

Ajout de produits (nom, description, prix, quantité)

Affichage dynamique de la liste des produits

Suppression de produits

Association des produits à l’utilisateur authentifié

Base de données et synchronisation

Firebase Firestore comme base de données NoSQL

Synchronisation en temps réel

Collections structurées et sécurisées (users, products)

Prérequis techniques

Flutter SDK version 3.9.2 ou supérieure

Un projet Firebase avec Firestore activé

Un compte Google Cloud (authentification Google)

Un compte Twitter Developer (authentification X – optionnel)

Installation et configuration
1. Clonage du projet
git clone https://github.com/joel-aris/FLUTTER_404-TP2.git
cd FLUTTER_404-TP2

2. Installation des dépendances
flutter pub get

3. Configuration Firebase
Android

Télécharger google-services.json depuis Firebase Console

Le placer dans android/app/

Ajouter Google Services dans android/build.gradle :

dependencies {
    classpath 'com.google.gms:google-services:4.4.0'
}


Activer le plugin dans android/app/build.gradle :

apply plugin: 'com.google.gms.google-services'

iOS

Télécharger GoogleService-Info.plist

Le placer dans ios/Runner/

Ouvrir ios/Runner.xcworkspace avec Xcode et ajouter le fichier au projet

4. Configuration Twitter / X (optionnelle)

Renseigner les clés API dans lib/config/api_config.dart

Activer l’authentification Twitter dans Firebase Console

Configurer correctement les URLs de callback

Un guide détaillé est disponible dans le fichier CONFIGURATION_COMPLETE.md.

5. Configuration Firebase Console

Activer l’authentification Email/Mot de passe

Activer Google Sign-In

Activer Twitter Sign-In (si utilisé)

Firestore créera automatiquement les collections :

users

products

Exécution de l’application
flutter run

Architecture du projet
lib/
├── main.dart
├── models/
│   ├── user_model.dart
│   └── product_model.dart
├── services/
│   ├── auth_service.dart
│   ├── product_service.dart
│   └── preferences_service.dart
└── screens/
    ├── login_screen.dart
    ├── signup_screen.dart
    └── menu_screen.dart


Cette structure garantit une bonne séparation des responsabilités et facilite la maintenance et l’évolution du projet.

Design et expérience utilisateur

Basé sur Material Design 3

Interface responsive et intuitive

Animations fluides

Palette principale : Indigo (#6366F1)

Modèle des données Firestore
Collection users
{
  "uid": "string",
  "email": "string",
  "displayName": "string",
  "photoURL": "string",
  "authProvider": "email | google | twitter"
}

Collection products
{
  "id": "string",
  "name": "string",
  "description": "string",
  "price": "number",
  "quantity": "number",
  "imageUrl": "string",
  "userId": "string",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}

Sécurité

Authentification entièrement gérée par Firebase Authentication

Accès aux données restreint par utilisateur

Sécurisation via règles Firestore

Exemple de règles Firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }

    match /products/{productId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update, delete: if request.auth != null &&
        resource.data.userId == request.auth.uid;
    }
  }
}

Dépannage courant
Firebase non initialisé

Vérifier la présence des fichiers Firebase

Vérifier l’appel à Firebase.initializeApp() dans main.dart

Échec Google Sign-In

Vérifier l’activation Google dans Firebase Console

Vérifier le SHA-1 Android dans Firebase

Échec Twitter Sign-In

Vérifier les clés API

Vérifier l’activation Twitter dans Firebase

Licence

Projet réalisé à des fins pédagogiques et académiques.

Auteur

Projet Flutter réalisé dans le cadre du TP26 – FLUTTER_404
