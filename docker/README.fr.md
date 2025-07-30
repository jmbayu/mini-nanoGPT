[English](README.md) | [Français](README.fr.md)

Les fichiers de ce répertoire sont utilisés pour exécuter et initialiser des applications dans des conteneurs.

# Guide de Déploiement Docker pour Mini-NanoGPT

Ce projet fournit une solution Docker complète qui prend en charge la détection automatique de CUDA et la sélection de l'environnement PyTorch correspondant.

## 🚀 Démarrage Rapide

### Utiliser Docker Compose (recommandé)

```bash
# Démarrer le conteneur en avant-plan
docker-compose up --build

# Arrêter le service
docker-compose down
```

### Utiliser les Commandes Docker

```bash
# Construire l'image
docker build -t mini-nanogpt .

# Exécuter le conteneur (détection automatique du GPU)
docker run --gpus all -p 7860:7860 -v $(pwd)/data:/app/data mini-nanogpt

# Exécuter le conteneur (mode CPU uniquement)
docker run -p 7860:7860 -v $(pwd)/data:/app/data mini-nanogpt
```

## 🐛 Dépannage

### Problèmes Courants

1. **GPU non reconnu**
   ```bash
   # Vérifier les pilotes NVIDIA
   nvidia-smi

   # Vérifier le support GPU de Docker
   docker run --rm --gpus all nvidia/cuda:11.8-base-ubuntu22.04 nvidia-smi
   ```

2. **Port déjà utilisé**
   ```bash
   # Modifier le mappage des ports dans docker-compose.yml
   ports:
     - "8080:7860"  # Utiliser le port 8080
   ```

3. **Mémoire insuffisante**
   ```bash
   # Vérifier les ressources système
   docker stats

   # Limiter l'utilisation de la mémoire du conteneur
   docker run -m 4g mini-nanogpt
   ```

### Consulter les Logs
```bash
# Logs de Docker Compose
docker-compose logs -f

# Logs du conteneur Docker
docker logs mini-nanogpt
```

## 🔄 Mise à Jour et Maintenance

```bash
# Reconstruire l'image
docker-compose build --no-cache

# Nettoyer les images inutilisées
docker image prune

# Réinitialisation complète
docker-compose down
docker system prune -a
```

## 📝 Variables d'Environnement

La configuration peut être personnalisée via des variables d'environnement :

```yaml
environment:
  - GRADIO_SERVER_NAME=0.0.0.0
  - GRADIO_SERVER_PORT=7860
  - PYTHONUNBUFFERED=1
  - MINI_NANOGPT_ENV_TYPE=AUTO  # AUTO, CUDA, CPU
```
