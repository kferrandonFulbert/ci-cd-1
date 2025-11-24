# 🚀 Exercice CI/CD avec GitHub Actions — Guide pas à pas

Objectif : apprendre à automatiser l’exécution des tests avec **GitHub Actions (CI)** pour détecter automatiquement les erreurs à chaque *push* ou *pull request*.

---

## 🧰 Prérequis

Avant de commencer, assure-toi d’avoir :

* Node.js (version 16+ recommandée)
* npm
* Git installé et configuré :

  ```
  git config --global user.name "Ton Nom"
  git config --global user.email "ton@mail"
  ```
* Un compte GitHub
* (Optionnel) **GitHub CLI (`gh`)** si tu veux créer le repo depuis le terminal

---

## 📁 Contenu du projet

```
.
├── index.js                # Petite fonction (addition)
├── test.js                 # Test simple : addition(2,3) === 5
├── package.json            # script "test": "node test.js"
└── .github/
   └── workflows/
       └── ci.yml           # Workflow GitHub Actions (CI)
```

---

## ✅ Étape 1 — Installer les dépendances et exécuter le test localement

1. Ouvre un terminal à la racine du projet.

2. Installe les dépendances :

   ```
   npm install
   ```

3. Lance les tests :

   ```
   npm test
   ```

Résultat attendu :
✔ **Test réussi : addition(2,3) = 5**

---

## ✅ Étape 2 — Initialiser Git et préparer le dépôt local

Si ton projet n’a pas encore de repo Git :

```
git init
git add .
git commit -m "Initial: ajout exercice CI/CD"
```

---

## ✅ Étape 3 — Créer le dépôt GitHub

### Méthode via site Web

1. Va sur [https://github.com](https://github.com)
2. Clique **New repository**
3. Nomme ton repo (ex : `exercice-ci-cd`)
4. Clique **Create repository**

### Méthode GitHub CLI

```
gh repo create TON_COMPTE/exercice-ci-cd --public --source=. --remote=origin --push
```

---

## ✅ Étape 4 — Pousser ton code vers GitHub

Si tu as créé le repo via l’interface Web :

```
git remote add origin https://github.com/<TON_COMPTE>/<TON_REPO>.git
git branch -M main
git push -u origin main
```

---

## ✅ Étape 5 — Vérifier GitHub Actions

1. Va dans l’onglet **Actions** de ton repo
2. Tu verras un workflow nommé **CI Demo** (d’après ton `ci.yml`)
3. Clique dessus pour voir les étapes :

   * checkout
   * setup-node
   * npm install
   * npm test

Chaque étape affiche ses logs.

---

## 🔎 Lire les logs & relancer un job

Dans une exécution :

* clique sur le job
* développe une étape pour lire les logs
* pour relancer :

  * fais un nouveau commit/push
  * **ou** clique sur **Re-run jobs**

---

## 🛠️ Dépannage courant

### 🔴 Le workflow est rouge

Ouvre les logs pour comprendre l’erreur.

Erreurs fréquentes :

* Mauvaise version de Node
* `npm install` échoue
* Le test retourne un code ≠ 0
* `package.json` mal structuré

Ajoute temporairement des `console.log()` pour diagnostiquer.

---

## 🧪 Exercice pratique

1. Modifie `test.js` pour casser volontairement le test. Exemple :

   ```js
   const result = addition(10, 4);  // au lieu de 2 + 3
   ```

2. Puis :

   ```
   git add .
   git commit -m "Test cassé volontairement"
   git push
   ```

3. Observe GitHub Actions → le pipeline doit devenir **rouge**.

---

## ⚙️ Ajouter un badge de statut dans le README

```
![CI](https://github.com/<USER>/<REPO>/actions/workflows/ci.yml/badge.svg)
```

Exemple :

```
![CI](https://github.com/mon-compte/exercice-ci-cd/actions/workflows/ci.yml/badge.svg)
```

---

## 🔁 Extensions possibles

* Utiliser Jest pour les tests
* Ajouter un job de **lint (ESLint)**
* Ajouter un job de build (front ou backend)
* Déployer automatiquement (GitHub Pages, Netlify, Vercel…)
* Configurer des **protections de branche** sur `main`

---

## 📚 Bonnes pratiques rapides

* Place ton workflow dans `.github/workflows/ci.yml`
* Parallélise avec plusieurs jobs si besoin (lint, test, build)
* Utilise **GitHub Secrets** pour les tokens et clés API
* Documente les étapes importantes dans le README

---

🎉 **Bravo ! Tu as un pipeline CI fonctionnel avec GitHub Actions.**
