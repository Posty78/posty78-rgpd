# rgpd.posty78.fr — Setup

## 1. Repo GitHub
- Crée un repo (public ou privé, peu importe pour GitHub Pages avec un compte payant ; sinon public)
  ex: `posty78-rgpd`
- Mets `index.html` et `details.html` à la racine
- Active GitHub Pages : Settings → Pages → Branch `main` → `/ (root)`

## 2. Config Firebase
Dans `index.html`, remplace le bloc `firebaseConfig` par la config exacte de ton
projet `posty78-maps` (Console Firebase → Paramètres du projet → tes apps → SDK config).
C'est la même que celle utilisée sur tes autres sites (muscu, maps, etc.).

## 3. Firestore rules
Ouvre les règles Firestore de `posty78-maps` (Console Firebase → Firestore → Rules)
et ajoute le bloc du fichier `firestore-rules-a-ajouter.txt`, SANS toucher aux règles existantes.

## 4. DNS Infomaniak
Comme tes autres sous-domaines :
- Type CNAME
- Nom : `rgpd`
- Valeur : `posty78.github.io`

Puis dans GitHub : Settings → Pages → Custom domain → `rgpd.posty78.fr` → Save
→ coche "Enforce HTTPS" une fois le certificat généré (peut prendre quelques minutes/heures).

## 5. Email rgpd@posty78.fr
La page `details.html` pointe vers `rgpd@posty78.fr`. Si cette adresse n'existe pas
encore, crée une redirection depuis Infomaniak (Mail → Redirections) vers ton adresse
actuelle, ou une vraie boîte dédiée.

## 6. À compléter avant mise en ligne
Dans `details.html`, section "Qui traite tes données" :
- adresse du siège social de la SASU
- SIRET dès qu'il est attribué

## 7. Test
Ouvre `rgpd.posty78.fr` sur TON téléphone, accepte la géoloc, clique "J'AUTORISE",
puis vérifie dans Firestore (collection `consentements`) qu'un document est bien créé
avec horodatage, étape, geoloc, userAgent.

## Notes techniques
- Le numéro d'étape (McDo en cours) se règle en tapant sur le petit tag "#" en haut
  à droite — reste en mémoire (localStorage) tant que tu ne le changes pas.
- La géolocalisation est demandée en silence au chargement de la page ; si le
  participant/tel refuse, le consentement est quand même enregistré (geoloc = null).
- Firestore garde les preuves en local et les synchronise dès que le réseau revient
  (utile en zone blanche).
- La page n'est pas dans le menu, n'est pas indexée (`noindex`), et n'a aucun lien
  entrant depuis tes autres sites — seul le lien direct y mène.
