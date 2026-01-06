

# **FLUTTER_404-TP2**

## **Application Flutter de Gestion de Produits avec Authentification Multi-Providers**

---

**FLUTTER_404-TP2** est une application mobile moderne développée avec **Flutter**, dédiée à la **gestion de produits** et intégrant un système d’**authentification sécurisée multi-providers** reposant sur **Firebase Authentication** et **Cloud Firestore**.

Ce projet met en œuvre des **bonnes pratiques professionnelles** en développement mobile : architecture claire, séparation des responsabilités, persistance de session, sécurité des données et synchronisation en temps réel.

---

## **Équipe de développement**

Ce projet a été réalisé par :

* **BUKASA SHIMATU Junior**
* **LOLONGA EPANDA Roger**
* **MUKENDI MULU Joel**
* **NGANDU KASHINDA Franck**
* **PINI MPANZA Kevin**

---

## **Dépôt GitHub**

Code source officiel du projet :
**[https://github.com/joel-aris/FLUTTER_404-TP2](https://github.com/joel-aris/FLUTTER_404-TP2)**

---

## **Fonctionnalités principales**

### **Authentification utilisateur**

* Inscription et connexion par **email et mot de passe**
* Connexion via **Google**
* Connexion via **X (Twitter)**
* **Persistance de session** grâce à SharedPreferences
* Gestion sécurisée des sessions utilisateur

### **Gestion des produits**

* Ajout de produits (**nom**, **description**, **prix**, **quantité**)
* Affichage dynamique de la liste des produits
* Suppression de produits
* Association des produits à l’utilisateur authentifié

### **Base de données**

* Utilisation de **Firebase Firestore**
* Synchronisation **temps réel**
* Collections structurées : **users** et **products**

---

## **Prérequis techniques**

* **Flutter SDK** version **3.9.2** ou supérieure
* Un **projet Firebase** avec Firestore activé
* Un **compte Google Cloud** pour l’authentification Google
* Un **compte Twitter Developer** pour l’authentification X (optionnel)

---

## **Installation et configuration**

### **1. Clonage du projet**

```bash
git clone https://github.com/joel-aris/FLUTTER_404-TP2.git
cd FLUTTER_404-TP2
```

### **2. Installation des dépendances**

```bash
flutter pub get
```

---

## **Configuration Firebase**

### **Android**

* Télécharger le fichier **google-services.json** depuis la Firebase Console
* Le placer dans **android/app/**
* Ajouter Google Services dans **android/build.gradle** :

```gradle
dependencies {
    classpath 'com.google.gms:google-services:4.4.0'
}
```

* Activer le plugin dans **android/app/build.gradle** :

```gradle
apply plugin: 'com.google.gms.google-services'
```

### **iOS**

* Télécharger **GoogleService-Info.plist**
* Le placer dans **ios/Runner/**
* Ouvrir **ios/Runner.xcworkspace** avec Xcode
* Ajouter le fichier au projet via Xcode

---

## **Configuration Twitter / X (optionnelle)**

* Renseigner les clés API dans **lib/config/api_config.dart**
* Activer l’authentification Twitter dans la **Firebase Console**
* Configurer correctement les **URLs de callback**

Un guide détaillé est disponible dans le fichier **CONFIGURATION_COMPLETE.md**.

---

## **Configuration Firebase Console**

* Activer l’authentification **Email / Mot de passe**
* Activer **Google Sign-In**
* Activer **Twitter Sign-In** (si utilisé)
* Les collections suivantes seront créées automatiquement :

  * **users**
  * **products**

---

## **Exécution de l’application**

```bash
flutter run
```

---

## **Architecture du projet**

```
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
```

Cette architecture garantit une **bonne lisibilité**, une **maintenance facilitée** et une **évolutivité du projet**.

---

## **Design et expérience utilisateur**

* Basé sur **Material Design 3**
* Interface **intuitive**, **responsive** et fluide
* Animations légères et cohérentes
* Couleur principale : **Indigo (#6366F1)**

---

## **Modèle des données Firestore**

### **Collection `users`**

```json
{
  "uid": "string",
  "email": "string",
  "displayName": "string",
  "photoURL": "string",
  "authProvider": "email | google | twitter"
}
```

### **Collection `products`**

```json
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
```

---

## **Sécurité**

* Authentification gérée par **Firebase Authentication**
* Accès aux données restreint par utilisateur
* Sécurisation via **règles Firestore**

### **Exemple de règles Firestore**

```javascript
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
```

---

## **Dépannage**

### **Firebase non initialisé**

* Vérifier les fichiers de configuration Firebase
* Vérifier l’appel à **Firebase.initializeApp()** dans `main.dart`

### **Échec Google Sign-In**

* Vérifier l’activation Google dans Firebase Console
* Vérifier le **SHA-1** Android

### **Échec Twitter Sign-In**

* Vérifier les clés API
* Vérifier l’activation Twitter dans Firebase Console

---

## **Licence**

Projet réalisé à des fins **pédagogiques et académiques**.

---

## **Auteur**

Projet Flutter réalisé dans le cadre du **TP26 – FLUTTER_404**

