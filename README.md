Rapport LAB16 : Inspection HTTPS Android avec Objection


1. Objectifs
Installer Objection (outil basé sur Frida)

Contourner le SSL Pinning sans écrire de code

Inspecter le trafic HTTPS via Burp Suite

2. Environnement
Élément	Configuration
PC	Windows 11 + Frida + Objection + Burp Suite
Android	Pixel 3a rooté + frida-server
App cible	TargetSSL.apk
3. Déroulement
Étape 1 — Installation
bash
pip install objection
Étape 2 — Démarrage frida-server (Android)
bash
adb shell su -c /data/local/tmp/frida-server &
Étape 3 — Configuration proxy
Burp Suite : écoute sur 192.168.1.45:8080

Wi-Fi Android : proxy manuel vers cette IP

Installation du certificat CA Burp

Étape 4 — Lancement Objection et bypass
bash
objection -g com.example.targetapp explore
Puis dans la console :

text
android sslpinning disable
Étape 5 — Validation
Le trafic HTTPS devient visible dans Burp Suite

4. Résultats
✅ SSL Pinning contourné avec succès
✅ Trafic HTTPS inspectable en clair
✅ Aucun code écrit (vs LAB15)

5. Difficultés et solutions
Problème	Solution
Commande non reconnue	android ssltap disable (nouvelle syntaxe)
Processus introuvable	Vérifier frida-ps -U
App plante	Relancer la commande immédiatement
6. Conclusion
Objection simplifie considérablement le contournement du SSL Pinning par rapport aux scripts Frida manuels du LAB15. Il est idéal pour les audits rapides.

<img width="1114" height="866" alt="img1" src="https://github.com/user-attachments/assets/872110f9-000b-4b92-9284-55dae8441059" />

<img width="1457" height="1146" alt="imG2" src="https://github.com/user-attachments/assets/5a7114da-e837-4799-91cc-3832c429807a" />

<img width="1099" height="556" alt="IMG3" src="https://github.com/user-attachments/assets/7c0d56d3-a41c-43cf-b6ff-fbb88e647f57" />

<img width="362" height="715" alt="IMG4" src="https://github.com/user-attachments/assets/c760c6c2-b0fb-4246-8439-5e28aee52d43" />
<img width="600" height="283" alt="img5" src="https://github.com/user-attachments/assets/2b9bac81-3388-4b8a-9b0b-67482667b12a" />
<img width="1722" height="180" alt="img6" src="https://github.com/user-attachments/assets/9d5ac4d0-0cab-4e87-89fc-70834464aa9f" />

<img width="1722" height="180" alt="img7" src="https://github.com/user-attachments/assets/26df7b7c-05b2-483d-b0d1-f610e577f06f" />
