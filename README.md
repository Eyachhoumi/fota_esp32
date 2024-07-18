## Code ESP32

Le code de l'ESP32 est responsable de la gestion de la connectivité WiFi et de la communication MQTT pour la réception des informations de mise à jour de firmware. 

### Description Globale

Le code de l'ESP32 accomplit les tâches suivantes :

1. **Connexion WiFi** : 
   - L'ESP32 se connecte au réseau WiFi configuré pour permettre la communication avec le broker MQTT et le téléchargement des fichiers via HTTP.

2. **Souscription au Topic MQTT** :
   - L'ESP32 s'abonne à un topic spécifique sur le broker MQTT (Mosquitto) pour recevoir les messages contenant les informations de mise à jour de firmware, y compris le lien de téléchargement du fichier binaire et la valeur CRC.

3. **Réception et Transmission des Messages** :
   - Lorsqu'un message MQTT est reçu, l'ESP32 extrait le lien de téléchargement et la valeur CRC du message.
   - Il transmet ensuite ces informations au microcontrôleur STM32F407 via une interface série ou une autre méthode de communication inter-processeurs (comme SPI ou I2C).

### Flux de Travail du Code ESP32

1. **Initialisation** :
   - Configuration des paramètres WiFi (SSID, mot de passe).
   - Initialisation de la bibliothèque MQTT avec les paramètres du broker.

2. **Connexion au WiFi** :
   - Tentative de connexion au réseau WiFi avec gestion des erreurs en cas d'échec de la connexion.

3. **Souscription et Réception MQTT** :
   - Connexion au broker MQTT.
   - Souscription au topic défini pour les mises à jour de firmware.
   - Attente et réception des messages MQTT.

4. **Traitement des Messages** :
   - Extraction des informations (lien de téléchargement, CRC) du message reçu.
   - Transmission des informations extraites au STM32F407.
