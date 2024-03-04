# OLLAMA
## À propos d'OLLAMA
OLLAMA est une plateforme innovante conçue pour faciliter l'utilisation locale des modèles de langage de grande taille. Avec OLLAMA, les utilisateurs peuvent rapidement télécharger, configurer et interagir avec une variété de modèles de langage sur macOS, Windows, Linux, et via Docker. OLLAMA vise à rendre l'accès aux technologies d'intelligence artificielle de pointe plus accessible et plus pratique pour les développeurs, les chercheurs et les passionnés d'IA.

## Fonctionnalités Principales
- **Compatibilité Multiplateforme**: Prise en charge de macOS, Windows (en aperçu), et Linux.
- **Librairies pour Divers Langages**: Support pour Python et JavaScript, permettant une intégration facile dans vos projets existants.
- **Sélection de Modèles Étendue**: Accès à une bibliothèque de modèles variés, allant de Llama 2 à Vicuna, avec des options de configuration avancées.
- **Personnalisation de Modèle**: Possibilité d'importer et de personnaliser vos propres modèles à l'aide de Modelfile.
- **API REST**: Interface de programmation pour l'exécution et la gestion des modèles à distance.
- **Documentation Complète**: Documentation détaillée pour vous aider à démarrer et à tirer le meilleur parti de la plateforme.
- **Support Actif**: Équipe de support dédiée pour répondre à vos questions et résoudre vos problèmes.
- **Licence Libre**: OLLAMA est distribué sous une licence libre, vous permettant de l'utiliser, de le modifier et de le distribuer librement.
- **Sécurité**: OLLAMA est conçu pour protéger la confidentialité et la sécurité de vos données.
- **Performances**: OLLAMA est optimisé pour des performances élevées, même sur des modèles de langage de grande taille.
- **Facilité d'Utilisation**: Interface en ligne de commande (CLI) intuitive pour une utilisation facile et rapide.
- **Mises à Jour Régulières**: OLLAMA est régulièrement mis à jour avec de nouvelles fonctionnalités, des améliorations de performances et des correctifs de sécurité.
- **Compatibilité avec les Modèles Hugging Face**: OLLAMA est compatible avec les modèles Hugging Face, vous permettant d'accéder à une large gamme de modèles de langage pré-entraînés.
- **Modèles de Langage de Grande Taille**: OLLAMA prend en charge des modèles de langage de grande taille, tels que Llama 2, Vicuna, et d'autres modèles de la bibliothèque OLLAMA.

## Commencer
### Prérequis
- macOS, Windows ou Linux
- Docker (optionnel)
- Au moins 8 GB de RAM pour les modèles 7B, 16 GB pour les 13B, et 32 GB pour les 33B

### Installation
- **macOS & Windows** : Téléchargez OLLAMA depuis [ollama.com](https://ollama.com) (choisissez la version correspondant à votre système d'exploitation).
- **Linux** : Exécutez la commande suivante dans votre terminal :
```bash
curl -fsSL https://ollama.com/install.sh | sh
```
- **Docker** : Téléchargez l'image officielle OLLAMA depuis Docker Hub :
```bash
docker pull ollama/ollama
```

## Utilisation Rapide
Pour interagir avec un modèle comme Llama 2, exécutez :
```bash
ollama run llama2
```

## Bibliothèque de Modèles
Consultez [ollama.com/library](https://ollama.com/library) pour une liste complète des modèles disponibles et des instructions de téléchargement.
Créer son propre modèle à l'aide de Modelfile
```bash
ollama pull llama2 # télécharger le modèle de base
nano mario.modelfile # créer un fichier de configuration pour le modèle
```
Dans le fichier de configuration écrire les lignes suivantes:
```bash
FROM llama2 # modèle de base ou choisir son modele de base
PARAMETER temperature 1 # augmenter la température pour plus de diversité
SYSTEM """
Vous êtes Mario Bros, et vous devez sauver la princesse Peach.
Répondre en tant que Mario avec des phrases tel que 'C'est moi Mario Youhou'.
Imaginer que vous êtes dans le monde de Mario Bros.
Proposer un voyage dans le monde de Mario Bros à votre interlocuteur.
""" # ajouter le texte pour le model personnel
```
Enregistrer le fichier et exécuter la commande suivante pour créer le modèle
```bash
ollama create mario -f mario.modelfile
ollama run mario
```

## Personnalisation de Modèle
OLLAMA offre des options avancées pour personnaliser et importer vos propres modèles. Consultez la documentation pour plus de détails sur l'utilisation de Modelfile et l'importation de modèles.

## CLI Référence
OLLAMA fournit une interface en ligne de commande (CLI) riche pour créer, gérer, et interagir avec les modèles. Voici quelques commandes utiles :
```bash
ollama create <nom> # Créer un modèle à partir d'un Modelfile.
ollama pull <modèle> # Télécharger ou mettre à jour un modèle.
ollama list # Lister les modèles installés sur votre machine.
```
## API REST
OLLAMA offre également une API REST pour l'exécution et la gestion des modèles à distance. Consultez la documentation de l'API pour plus de détails.

## Documentation pour installation et utilisation sur un Raspberry Pi 5 8go

### Prérequis
- Raspberry Pi 5 8go

### Installation
- **Raspberry Pi 5 8go** : 
```bash
curl -fsSL https://ollama.com/install.sh | sh
```
- **Tester l'installation**:
```bash
ollama run mistral
```
Afin de faciliter l'utilisation, mettons en place ollama-webui pour une interface graphique.
prerequis:
- python3
- nodejs 20
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - && sudo apt install -y nodejs # installation de nodejs
sudo bash install setup_20.x # installation de nodejs
```
- Cloner le repository ollama-webui et l'installer
```bash
git clone https://github.com/ollama-webui/ollama-webui.git
cd ollama-webui
npm i
npm audit fix # si besoin
npm run build
cd ./backend/
pip install -r requirements.txt --break-system-packages # break-system-packages pour installer sur les packages systemes pas obligatoire si vous avez un environnement virtuel (virtualenv)
export PATH=$PATH:$HOME/.local/bin # ajouter le path pour les commandes
sudo mousepad /etc/init.d/ollama # créer un ficheir de configuration pour le service
```
Dans le fichier de configuration écrire les lignes suivantes:
```bash
#! /bin/bash
### BEGIN INIT INFO
#Â Provides: OllamaWeb
# Required-Start: $all
# Required-Stop:
# Default-Start: 5
# Default-Stop: 6
# Short-Description: Ollama Web interface
### END INIT INFO

TARGET_USER='$USER' # remplacer par le nom de l'utilisateur
COMMAND='$HOME/ollama-webui/backend/start.sh'
sudo -u $TARGET_USER -i -- $COMMAND
```
Mise en place du démararage automatique
```bash
sudo chmod +x /etc/init.d/ollama
sudo update-rc.d ollama defaults
```
Démarrer le service
```bash
sh start.sh
```
