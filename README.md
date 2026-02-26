 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/Smart_Home_Network_PKT_Build_Guide.md b/Smart_Home_Network_PKT_Build_Guide.md
new file mode 100644
index 0000000000000000000000000000000000000000..5a92c733ea3ef546a14ae23de2eee75475ae8249
--- /dev/null
+++ b/Smart_Home_Network_PKT_Build_Guide.md
@@ -0,0 +1,106 @@
+# Atelier 1 — Smart Home Network (Packet Tracer)
+
+Ce document fournit **la construction complète** du fichier `Smart_Home_Network.pkt` à partir des consignes fournies.
+
+> Important : le format `.pkt` est un format propriétaire Packet Tracer. La génération d'un `.pkt` final doit être faite dans l'application Packet Tracer, puis sauvegardée.
+> Ce guide contient toutes les étapes et valeurs nécessaires pour recréer le fichier final attendu.
+
+## 1) Topologie attendue (état final)
+
+Infrastructure et accès :
+- 1 x **Home Gateway**
+- 1 x **Tablet**
+
+Objets IoT (minimum demandé dans l'atelier) :
+- Appareils IoT déjà présents dans le modèle initial (selon fichier de départ)
+- 1 x **Lawn Sprinkler** (filaire)
+- 1 x **Wind Detector** (sans fil)
+
+## 2) Paramètres réseau de référence
+
+Depuis **Home Gateway** :
+- LAN : relever l'adresse du réseau local (dépend du fichier de départ)
+- WLAN SSID : relever le SSID du réseau domestique
+- Sécurité : WPA2-PSK
+- PSK : `mySecretKey`
+
+Identifiants IoT Monitor (Tablet) :
+- Username : `admin`
+- Password : `admin`
+
+## 3) Ajout de l'appareil IoT filaire — Lawn Sprinkler
+
+1. Ouvrir `End Devices` > `Home`.
+2. Glisser-déposer **Lawn Sprinkler** dans la zone logique.
+3. Ouvrir `Connections` (icône éclair).
+4. Choisir **Copper Straight-Through**.
+5. Relier :
+   - `Lawn Sprinkler FastEthernet0` ->
+   - un port Ethernet libre de `Home Gateway`.
+
+### Configuration de Lawn Sprinkler
+
+Dans la fenêtre de l'appareil :
+- Onglet `Config`
+  - `Display Name` = `Sprinkler1`
+  - `IoT Server` = `Home Gateway`
+- `FastEthernet0`
+  - `IP Configuration` = `DHCP`
+
+### Vérification
+
+Depuis `Tablet` :
+- `Desktop` > `IoT Monitor`
+- Login `admin/admin`
+- Vérifier que `Sprinkler1` apparaît dans la liste des appareils IoT.
+
+## 4) Ajout de l'appareil IoT sans fil — Wind Detector
+
+1. Ouvrir `End Devices` > `Home`.
+2. Glisser-déposer **Wind Detector** dans la zone logique.
+3. Ouvrir la fenêtre de l'appareil.
+4. Cliquer **Advanced**.
+5. Onglet `I/O Config` :
+   - `Network Adapter` = `PT-IOT-NM-1W` (module sans fil)
+
+### Configuration réseau sans fil
+
+Dans l'onglet `Config` :
+- `Display Name` = `Wind_Detector`
+- `IoT Server` = `Home Gateway`
+- `Wireless0` :
+  - Authentication = `WPA2-PSK`
+  - PSK Pass Phrase = `mySecretKey`
+
+### Vérification
+
+Depuis `Tablet` :
+- `Desktop` > `IoT Monitor`
+- Login `admin/admin`
+- Vérifier que `Wind_Detector` apparaît dans la liste IoT.
+
+## 5) Tests de validation finaux (à exécuter avant sauvegarde)
+
+- [ ] `Sprinkler1` apparaît en ligne dans l'IoT Monitor.
+- [ ] `Wind_Detector` apparaît en ligne dans l'IoT Monitor.
+- [ ] Les deux appareils sont associés au serveur IoT `Home Gateway`.
+- [ ] `Sprinkler1` obtient une adresse IP via DHCP.
+- [ ] `Wind_Detector` est connecté en WPA2-PSK avec la clé `mySecretKey`.
+
+## 6) Nommage et livraison du fichier
+
+Nom recommandé du fichier final :
+- `Atelier1_Smart_Home_Network_Complet.pkt`
+
+Procédure de sauvegarde :
+1. `File` > `Save As...`
+2. Sélectionner : `Atelier1_Smart_Home_Network_Complet.pkt`
+3. Vérifier la réouverture du fichier et la présence des deux nouveaux objets IoT.
+
+## 7) Extension (Exercice demandé)
+
+Pour les essais supplémentaires, ajouter d'autres équipements IoT :
+- Filaire : Camera, Door, Siren, etc. reliés en Ethernet + DHCP
+- Sans fil : capteurs/actuateurs avec `PT-IOT-NM-1W` + WPA2-PSK `mySecretKey`
+
+Valider chaque ajout via `Tablet > IoT Monitor`.
 
EOF
)
