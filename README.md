# FoutaChat AI 💬

Application de messagerie intelligente africaine.  
**Créée par Abdoul Aziz Dia · UNCHK**

---

## 🚀 Déploiement sur Vercel (étape par étape)

### Étape 1 — Créer votre projet Firebase (GRATUIT)
1. Allez sur https://console.firebase.google.com
2. Cliquez **"Créer un projet"** → Nommez-le `foutachat-ai`
3. Dans **Authentication** → Activez **Email/Password**
4. Dans **Firestore Database** → Créez en **mode production**
5. Dans **Storage** → Activez Firebase Storage
6. Dans **Paramètres du projet** → Copiez vos clés de configuration

### Étape 2 — Créer votre clé Claude API
1. Allez sur https://console.anthropic.com
2. Créez un compte → Allez dans **API Keys**
3. Cliquez **"Create Key"** → Copiez la clé

### Étape 3 — Déployer sur Vercel (GRATUIT)
1. Allez sur https://vercel.com → Connectez-vous avec GitHub
2. Uploadez ce dossier sur GitHub (nouveau repo)
3. Dans Vercel → **"New Project"** → Importez votre repo
4. Dans **"Environment Variables"**, ajoutez ces variables :

```
NEXT_PUBLIC_FIREBASE_API_KEY          = votre_cle_firebase
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN      = votre_projet.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID       = votre_projet_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET   = votre_projet.appspot.com
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID = votre_sender_id
NEXT_PUBLIC_FIREBASE_APP_ID           = votre_app_id
ANTHROPIC_API_KEY                     = votre_cle_claude
```

5. Cliquez **"Deploy"** → Votre app est en ligne !

### Étape 4 — Configurer les règles Firestore
Dans Firebase Console → Firestore → Règles, collez ceci :

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read: if request.auth != null;
      allow write: if request.auth.uid == userId;
    }
    match /conversations/{convId} {
      allow read, write: if request.auth != null && 
        request.auth.uid in resource.data.participants;
      allow create: if request.auth != null;
      match /messages/{msgId} {
        allow read, write: if request.auth != null;
      }
    }
    match /scheduled/{msgId} {
      allow read, write: if request.auth != null && 
        request.auth.uid == resource.data.senderId;
      allow create: if request.auth != null;
    }
  }
}
```

---

## Fonctionnalités incluses
- ✅ Authentification (inscription/connexion)
- ✅ Messagerie en temps réel
- ✅ Envoi de photos
- ✅ Recherche d'utilisateurs
- ✅ Assistant IA (Claude)
- ✅ Quiz éducatif
- ✅ Messages programmés
- ✅ Coffre-fort sécurisé
- ✅ Profil utilisateur
