# Photo ID HD — application Android (APK) construite par GitHub

Photos d'identité en haute définition : appareil photo intégré, cadrage du visage,
dimensions officielles, fond blanc, export JPG / PNG / BMP / TIFF / WebP / PDF / ZIP
et planche d'impression (10×15, 13×18, A4).

Tout est traité sur le téléphone : aucune photo n'est envoyée sur Internet.

## Obtenir l'APK (sans rien installer sur votre ordinateur)

1. **Créez un compte GitHub** (gratuit) sur https://github.com/signup
2. **Créez un dépôt** : bouton « + » en haut à droite → *New repository*.
   Nom : `photo-id-hd`, laissez *Public* ou *Private*, ne cochez rien d'autre → *Create repository*.
3. **Envoyez les fichiers** de ce dossier dans le dépôt. Deux façons :
   - *Ordinateur avec Git* (recommandé, garde bien le dossier caché `.github`) :
     ```
     cd photo-id-hd
     git init -b main
     git add .
     git commit -m "Première version"
     git remote add origin https://github.com/VOTRE-NOM/photo-id-hd.git
     git push -u origin main
     ```
   - *Sans Git* : sur la page du dépôt, *Add file → Upload files*, glissez tout le contenu du dossier.
     Si le dossier `.github` n'est pas pris en compte, faites *Add file → Create new file*, tapez
     `.github/workflows/build-apk.yml` comme nom de fichier et collez-y le contenu du fichier du même nom.
4. **Attendez la construction** : onglet **Actions** du dépôt → le workflow « Construire l'APK »
   démarre tout seul (5 à 10 minutes la première fois). Une coche verte = terminé.
   S'il ne démarre pas : *Actions → Construire l'APK → Run workflow*.
5. **Téléchargez l'APK** :
   - colonne de droite de la page du dépôt → **Releases → « Photo ID HD — dernière version »** → `PhotoID-HD.apk`
   - ou dans l'exécution du workflow, section *Artifacts* → `PhotoID-HD-apk` (zip contenant l'APK).
6. **Installez-le sur le téléphone** : ouvrez le lien de la release depuis le téléphone, téléchargez
   `PhotoID-HD.apk`, touchez-le, et autorisez « Installer des applications inconnues » pour votre
   navigateur ou gestionnaire de fichiers si Android le demande.
   À la première ouverture, acceptez l'accès à la caméra.

## Mettre à jour l'application

Modifiez un fichier (par exemple `www/index.html`) puis `git push` : un nouvel APK est construit et
remplace la release « dernière version ». L'APK est toujours signé avec la même clé
(`keystore/debug.keystore`) : vous pouvez l'installer par-dessus l'ancien sans rien perdre.

Pour publier une version numérotée : `git tag v1.0 && git push origin v1.0`.

## Si ça ne marche pas

- **Le workflow est rouge** : cliquez sur l'étape en erreur dans *Actions* et copiez le message.
- **« Resource not accessible by integration » à l'étape Releases** : *Settings → Actions → General →
  Workflow permissions* → cochez **Read and write permissions** → *Save*, puis relancez le workflow.
- **« Application non installée »** : désinstallez l'ancienne version (signée avec une autre clé) puis réinstallez.
- **La caméra ne s'ouvre pas** : *Paramètres Android → Applications → Photo ID HD → Autorisations → Appareil photo*.

## Contenu du dossier

| Fichier / dossier | Rôle |
|---|---|
| `www/` | l'application (page web + icônes + manifeste) ; fonctionne aussi seule dans un navigateur en HTTPS |
| `capacitor.config.json`, `package.json` | configuration de l'emballage Android (Capacitor) |
| `scripts/patch_android.py` | ajoute la permission caméra, le mode portrait, les icônes et le n° de version |
| `.github/workflows/build-apk.yml` | la recette de construction de l'APK |
| `keystore/debug.keystore` | clé de signature de test, identique à chaque build (pour usage personnel) |

La clé fournie convient pour installer l'application sur vos propres appareils. Pour la publier
sur le Play Store, il faudra créer votre propre clé de publication.
