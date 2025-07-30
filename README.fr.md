[**English**](https://github.com/ystemsrx/mini-nanoGPT) | [简体中文](README.zh.md) | [Français](README.fr.md)

# Mini NanoGPT 🚀

#### Entraîner un GPT peut vraiment être aussi simple ?

> Rendre l'entraînement de GPT amusant et accessible ! Une plateforme d'entraînement visuelle basée sur [karpathy/nanoGPT](https://github.com/karpathy/nanoGPT).

## 📖 Qu'est-ce que c'est ?

Mini-NanoGPT est un outil qui vous aide à démarrer avec l'entraînement de modèles GPT sans effort. Que vous soyez :

* 🎓 Un débutant en apprentissage profond
* 👨‍🔬 Un chercheur
* 🛠️ Un développeur

Ou simplement curieux des grands modèles de langage et que vous vouliez expérimenter leur magie,

Vous pouvez entraîner un modèle via une interface graphique intuitive !

> Pour la version originale de Mini NanoGPT (qui n'est plus mise à jour), veuillez consulter la branche [**old**](https://github.com/ystemsrx/mini-nanoGPT/tree/old).

## ✨ Fonctionnalités clés

### 1. Facile à utiliser

* 📱 **Interface visuelle** : Dites adieu à la ligne de commande ; cliquez pour commencer l'entraînement
* 🌍 **Interface utilisateur bilingue** : Prise en charge complète des interfaces en anglais et en chinois
* 🎯 **Opérations en un clic** : Prétraitement des données, entraînement et génération de texte — le tout en un seul clic

### 2. Fonctionnalités puissantes

* 🔤 **Tokenisation flexible** : Prend en charge les tokenizers au niveau des caractères et GPT-2/Qwen, avec prise en charge multilingue
* 🚄 **Entraînement efficace** : Prend en charge l'accélération multi-processus et l'entraînement distribué
* 📊 **Rétroaction en temps réel** : Affichage en direct de la progression de l'entraînement et des performances
* ⚙️ **Visualisation des paramètres** : Tous les paramètres d'entraînement peuvent être ajustés directement dans l'interface utilisateur
* 🧩 **Base de données de modèles** : Gérez facilement les modèles et réutilisez les paramètres d'entraînement à tout moment

## 🚀 Démarrage rapide

### Option 1 : Déploiement avec Docker (Recommandé) 🐳

Le moyen le plus simple de commencer !

```bash
# Cloner le dépôt
git clone --depth 1 https://github.com/ystemsrx/mini-nanoGPT.git
cd mini-nanogpt

# Démarrer avec Docker Compose (recommandé)
docker-compose up --build

# Ou construire et exécuter manuellement
docker build -t mini-nanogpt .
docker run --gpus all -p 7860:7860 -v $(pwd)/data:/app/data mini-nanogpt
```

Cela construira automatiquement l'image Docker et exécutera le conteneur. Le conteneur détectera automatiquement votre environnement système (CPU/GPU). Pendant ce temps, les répertoires `data`, `models` et `assets` du répertoire de travail actuel seront montés dans le conteneur, vous permettant de stocker des données directement dans ces répertoires.

Une fois démarré, visitez http://localhost:7860 pour accéder à l'application.

### Option 2 : Installation locale

Tout d'abord, créez un environnement virtuel avec une version de Python jusqu'à 3.12. Ceci est nécessaire en raison des compatibilités avec `torch` 2.0.

**Avec bash :**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Avec PowerShell :**
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Une fois l'environnement virtuel activé, installez les dépendances :
```bash
# Cloner le dépôt
git clone --depth 1 https://github.com/ystemsrx/mini-nanoGPT.git
cd mini-nanogpt

# Installer les dépendances
pip install -r requirements.txt
```

### 2. Lancer l'application

```bash
python app.py
```

Ouvrez le lien affiché dans votre navigateur (généralement [http://localhost:7860](http://localhost:7860)) pour voir l'interface d'entraînement !

## 🎮 Guide de l'utilisateur

### Étape 1 : Préparer les données

* Ouvrez la page "Traitement des données", collez votre texte d'entraînement et choisissez une méthode de tokenisation. Pour de meilleurs résultats, cochez l'option d'utiliser un tokenizer — il construira automatiquement un vocabulaire basé sur votre texte.
* Si vous ne voulez pas utiliser d'ensemble de validation, cochez l'option "Sauter l'ensemble de validation".
* Cliquez sur "Démarrer le traitement" lorsque vous avez terminé.

Voici un petit exemple pour la démonstration :

![Traitement des données](https://github.com/ystemsrx/mini-nanoGPT/blob/master/assets/imgs/en_data_process.png?raw=true)

### Étape 2 : Entraîner le modèle

* Passez à la page "Entraînement" et ajustez les paramètres si nécessaire (ou laissez-les par défaut pour un essai rapide).
* Les courbes de perte d'entraînement et de validation sont affichées en temps réel. Si vous avez généré un ensemble de validation à l'étape 1, vous devriez voir deux courbes : bleue pour la perte d'entraînement, orange pour la perte de validation.
* Si une seule courbe est affichée, vérifiez la sortie du terminal. Si vous voyez une erreur comme :

  ```
  Error while evaluating val loss: Dataset too small: minimum dataset(val) size is 147, but block size is 512. Either reduce block size or add more data.
  ```

  cela signifie que votre `block size` est trop grand pour l'ensemble de validation. Essayez de le réduire, par exemple à 128.
* Vous devriez maintenant voir les deux courbes de perte se mettre à jour dynamiquement.
* Cliquez sur "Démarrer l'entraînement" et attendez la fin de l'entraînement.

![Entraînement](https://github.com/ystemsrx/mini-nanoGPT/blob/master/assets/imgs/en_train.png?raw=true)

#### Mode évaluation uniquement ?

* Ce mode vous permet d'évaluer la perte du modèle sur l'ensemble de validation. Réglez le `Nombre de graines d'évaluation` sur une valeur > 0 pour activer le mode d'évaluation uniquement. Vous verrez comment le modèle se comporte avec différentes graines aléatoires.

### Étape 3 : Générer du texte

1. Allez à la page "Inférence"
2. Entrez une invite
3. Cliquez sur "Générer" et voyez ce que le modèle propose !

![Inférence](https://github.com/ystemsrx/mini-nanoGPT/blob/master/assets/imgs/en_inference.png?raw=true)

### Étape 4 : Comparaison de modèles

1. Allez à la page "Comparaison"
2. Sélectionnez deux modèles à comparer — ils peuvent même être le même modèle avec des paramètres différents
3. Leurs configurations seront affichées automatiquement
4. Vous pouvez entrer la même invite et voir comment les deux modèles génèrent du texte
5. Ou, appliquez différents paramètres d'inférence (température, top_k, etc.) pour comparer les sorties

![Comparaison](https://github.com/ystemsrx/mini-nanoGPT/blob/master/assets/imgs/en_comparison.png?raw=true)

## 📁 Structure du projet

```
mini-nanogpt/
├── app.py           # Point d'entrée de l'application
├── src/             # Configuration et modules principaux
├── data/            # Stockage des données
├── out/             # Points de contrôle du modèle
└── assets/          # Fichiers de tokenizer et autres ressources
```

## ❓ FAQ

### C'est trop lent ?

* 💡 Essayez de réduire la taille du lot ou la taille du modèle
* 💡 Utilisez un GPU pour améliorer considérablement la vitesse
* 💡 Augmentez l'intervalle d'évaluation

### Le texte généré n'est pas bon ?

* 💡 Essayez d'augmenter les données d'entraînement
* 💡 Ajustez les hyperparamètres du modèle
* 💡 Ajustez la température pendant la génération

### Vous voulez reprendre un entraînement précédent ?

* 💡 Sur la page "Entraînement", sélectionnez "reprendre" sous Initialisation
* 💡 Pointez vers le répertoire de sortie précédent

## 🤝 Contribuer

Les suggestions et améliorations sont les bienvenues ! Vous pouvez :

* Soumettre une Issue
* Ouvrir une Pull Request
* Partager votre expérience d'utilisation de l'outil

## 📝 Licence

Ce projet est open-source sous la [Licence MIT](LICENSE).

---

🎉 **Commencez votre voyage GPT maintenant !**
