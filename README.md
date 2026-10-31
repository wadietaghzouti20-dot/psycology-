# RENDEVO — Psychologie

Site de réservation en français, responsive, avec parcours en cinq étapes, services de psychologie, disponibilités en direct et confirmation côté serveur.

## Fonctions
- Première consultation, suivi, gestion du stress, soutien émotionnel, adolescent, parental, couple et autre motif.
- Créneaux selon les horaires, durées, réservations existantes et événements Google Calendar.
- Vérification anti-double réservation.
- Google Sheets : Appointments, Settings, AuditLog.
- Événement Google Calendar à la réservation.
- E-mails au patient et au cabinet.
- Lien sécurisé d'annulation : mise à jour Sheets, suppression Calendar et notifications.
- Rappel automatique environ 24 h avant (vérification horaire).
- Le champ libre du formulaire n'est pas enregistré côté serveur ; ne pas y saisir de données sensibles.

## Installer le backend
1. Créez un Google Sheets privé nommé RENDEVO — Psychologie.
2. Ouvrez Extensions → Apps Script.
3. Remplacez le contenu de Code.gs par le code de [apps-script/Code.gs](apps-script/Code.gs).
4. Dans Paramètres du projet → Propriétés du script, ajoutez :
   - SPREADSHEET_ID : identifiant du classeur (entre /d/ et /edit dans l'URL).
   - ADMIN_EMAIL : adresse de notification du cabinet.
   - CLINIC_NAME : nom du cabinet (facultatif).
   - CALENDAR_ID : ID Calendar (facultatif ; vide = calendrier principal).
5. Fuseau horaire du projet : Africa/Algiers.
6. Enregistrez, sélectionnez setup, cliquez Exécuter et autorisez les accès.
7. setup crée Appointments, Settings, AuditLog et le déclencheur horaire.

## Horaires par défaut
Modifiez l'onglet Settings :
- OPEN_TIME = 09:00
- CLOSE_TIME = 17:00
- WORKING_DAYS = 1,2,3,4,5,6 (lundi à samedi ; 0 = dimanche)
- SLOT_STEP_MINUTES = 30
- BUFFER_MINUTES = 10
- ADVANCE_DAYS = 90

Première consultation et couple : 60 min ; autres motifs : 50 min. Les durées peuvent être modifiées dans SERVICES au début du code.

## Déployer et connecter
1. Apps Script → Déployer → Nouveau déploiement → Application Web.
2. Exécuter en tant que : vous. Accès : Tout le monde.
3. Déployez et copiez l'URL /exec.
4. Dans config.js de ce dépôt, remplacez appsScriptUrl par cette URL et committez.

## Tests obligatoires
- L'URL /exec doit répondre success: true.
- Faire une réservation fictive et vérifier Sheets, Calendar et e-mails.
- Refaire la même réservation : elle doit être refusée.
- Ouvrir le lien d'annulation : statut CANCELLED et événement Calendar supprimé.
- Vérifier les exécutions et un rappel de test dans les 24 h.

Après une modification du backend : Déployer → Gérer les déploiements → Modifier → Nouvelle version → Déployer.

## Confidentialité
Gardez le classeur et le calendrier privés, avec accès limité. Vérifiez les obligations de confidentialité, conservation et suppression avant toute utilisation de données réelles. Le formulaire n'est pas un service d'urgence.
