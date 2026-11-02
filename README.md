# 📅 Mon Calendrier

Petite application personnelle (iPhone + ordinateur) qui reprend le fonctionnement du classeur **Calendrier 2026.xlsx** (onglets « Calendrier AAAA - VF ») :

- **Mois** : le calendrier du mois, semaine par semaine (numéros de semaine à gauche), avec les mêmes motifs que l'Excel : *Congé posé (C), Congé prévu (P), Récup (R), Pont (G), Férié (F), Travaillé (#), À travailler (T)*.
  Les jours de semaine passés comptent **automatiquement** comme travaillés, ceux à venir comme à travailler, et les jours fériés de Nouvelle-Calédonie sont déjà placés.
  Touche un jour pour changer son motif ou saisir des **heures de récup** : + en plus / − prise (2h30, 2:30 ou 2,5), avec une note.
- **Poser des jours** : une période d'un coup (seuls les jours travaillés sont pris). Un congé **prévu** passe en **posé** d'une touche.
- **Année** : les 12 mois en un coup d'œil + la synthèse de l'Excel :
  - Congés : reliquat N-1 + droits N − posés − prévus = restant
  - Récup : report au 1er janvier + heures en plus − récup prise = restante, en heures, jours (÷ 7,8), semaines (÷ 5) et mois (÷ 4)
  - Compteurs : travaillés, à travailler, fériés, ponts
  - La liste de tes absences de l'année
- **Récup** : le tableau mois par mois (solde au 1er, REC+, REC−, bilan) et le journal de toutes les heures saisies.
- **Import Excel** (Réglages) : reprend les onglets « Calendrier 2025 - VF », « 2026 - VF », « 2027 - VF » (et l'ancien « Calendrier 2024 »). La feuille « Crise » et les autres sont ignorées. Le fichier est lu sur l'appareil, il n'est envoyé nulle part.

## 🔒 Sécurité (même principe que Ma Maison et Mon Budget)

- L'**application** (le code) est publique sur GitHub Pages : elle ne contient **aucune donnée**.
- Tes **données** sont dans un **dépôt privé** séparé, dans un fichier `calendrier.enc.json`, **chiffré avec ton mot de passe** (AES-256-GCM, PBKDF2-SHA256 310 000 itérations) **sur le téléphone, avant l'envoi**.
- « Rester connecté » fonctionne comme dans tes autres apps (clé propre à l'appareil, le bouton 🔒 déconnecte).
- Les réglages de Mon Calendrier sont séparés de ceux de Ma Maison et Mon Budget (même adresse `github.io`, stockage distinct).
- ⚠️ **Mot de passe oublié = données perdues.** Fais de temps en temps Réglages → Exporter une sauvegarde.

---

## Installation (≈ 10 min, une seule fois)

### 1. Dépôt de l'application (public)
1. github.com → **New repository** → nom : `mon-calendrier` → **Public** → *Create*.
2. *Add file → Upload files* → dépose : `index.html`, `sw.js`, `manifest.webmanifest`, `icon-180.png`, `icon-192.png`, `icon-512.png`, `README.md` → *Commit*.
3. *Settings → Pages* → Source : **Deploy from a branch** → `main` / `(root)` → *Save*.
4. Après 1–2 minutes : `https://flonewcal988.github.io/mon-calendrier/`

### 2. Dépôt des données (privé)
**New repository** → nom : `mon-calendrier-donnees` → **Private** → coche **Add a README file** → *Create*.

### 3. Jeton d'accès (limité à ce seul dépôt)
1. Photo de profil → *Settings → Developer settings → Personal access tokens → Fine-grained tokens* → *Generate new token*.
2. Nom : `Mon Calendrier` · Expiration : 1 an.
3. **Repository access → Only select repositories →** `mon-calendrier-donnees`.
4. **Permissions → Contents : Read and write** (rien d'autre) → *Generate token* → copie le `github_pat_…`.

### 4. Premier lancement
1. Ouvre `https://flonewcal988.github.io/mon-calendrier/`
2. Pseudo et dépôt sont pré-remplis ; colle le jeton et **choisis un mot de passe** (8 caractères min.).
3. Réglages (⚙️) → **Importer mon fichier Excel** → choisis `Calendrier_2026.xlsx` → coche les années → *Importer*.

### 5. Sur iPhone
Safari → bouton **Partager** → **Sur l'écran d'accueil**. Sur l'ordinateur, refais l'étape 4 avec **le même mot de passe**.

## Bon à savoir
- **Résultats identiques à l'Excel** : 2026 → 41 j de congés et 215 h de récup restants ; 2025 → 34 j / 223,15 h ; 2027 → 30 j / 160,4 h.
- **Solde de récup en tête de mois** : dans l'Excel, à partir d'avril, la formule ajoute le bilan du mois lui-même au lieu de celui du mois précédent (ex. AC3 = U3+AF38 au lieu de U3+X38). L'Excel affiche donc 202 h à partir de juin alors que le total réel est 215 h. L'app fait le calcul juste (avril commence à 261,55 h).
- Comme les jours passés sont comptés travaillés automatiquement, le compteur « Travaillés » de 2026 est plus élevé que dans l'Excel (qui n'était rempli que jusqu'à mi-août).
- Une journée de récup (motif R) compte −7h48 si tu ne mets pas d'heures ; la durée d'une journée se règle dans Réglages.
- Nouvelle année : Réglages → Mes droits → « Préparer 2027 » propose de reprendre le restant de l'année.
- Hors ligne : l'app fonctionne, les modifications partent sur GitHub au retour du réseau.
