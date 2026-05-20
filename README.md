# CHARRIERE Bois — Guide de déploiement

## Structure du projet

```
charriere-site/
├── index.html              ← Page d'accueil (lit les JSON)
├── equipe.html             ← Page équipe & atelier
├── netlify.toml            ← Config Netlify
├── admin/
│   ├── index.html          ← Interface back-office Decap CMS
│   └── config.yml          ← Configuration du CMS
├── content/                ← Données modifiables via le CMS
│   ├── infos.json          ← Coordonnées, email formulaire
│   ├── reseaux.json        ← Liens réseaux sociaux
│   ├── horaires.json       ← Horaires d'ouverture
│   ├── hero.json           ← Bandeau vidéo et textes accueil
│   ├── apropos.json        ← Bloc à propos + valeurs
│   ├── photos_equipe.json  ← Photos et fiches membres
│   ├── galerie.json        ← Galerie atelier
│   ├── popup.json          ← Popup d'annonce
│   ├── alerte.json         ← Bandeau alerte / actualité
│   └── evenements/         ← Articles événements (créés via CMS)
└── assets/
    ├── images/             ← Toutes les photos uploadées via CMS
    └── video/              ← Vidéo du bandeau hero

```

---

## Étapes de déploiement

### 1. Créer le dépôt GitHub

```bash
cd charriere-site
git init
git add .
git commit -m "🌲 Initial commit — CHARRIERE Bois"
# Créer un repo sur github.com, puis :
git remote add origin https://github.com/VOTRE_COMPTE/charriere-bois.git
git push -u origin main
```

### 2. Connecter à Netlify

1. Aller sur [netlify.com](https://netlify.com) → "Add new site" → "Import an existing project"
2. Choisir GitHub → sélectionner le repo `charriere-bois`
3. Build settings : laisser vide (site statique)
4. Cliquer **Deploy site**

### 3. Activer Netlify Identity (pour le CMS)

Dans Netlify → votre site → **Site configuration** → **Identity** :
1. Cliquer **Enable Identity**
2. Dans **Registration** → sélectionner **Invite only**
3. Dans **Services** → **Git Gateway** → cliquer **Enable Git Gateway**

### 4. Inviter Marie-France

Dans **Identity** → **Invite users** → entrer l'email de Marie-France.
Elle recevra un email avec un lien pour créer son mot de passe.

### 5. Connecter le domaine OVH

Dans Netlify → **Domain management** → **Add custom domain** :
1. Entrer `charrierebois.com`
2. Netlify vous donne 4 serveurs DNS (ex: `dns1.p04.nsone.net`)
3. Dans votre espace client OVH → **Domaine** → **Serveurs DNS** → remplacer par ceux de Netlify
4. Attendre 24-48h pour la propagation
5. Le HTTPS (cadenas) s'active automatiquement

---

## Utilisation du back-office par Marie-France

**Accès :** `https://charrierebois.com/admin`

### Ce qu'elle peut faire

| Section | Ce qu'elle peut modifier |
|---|---|
| ⚙️ Coordonnées | Téléphone, emails, adresse |
| 📱 Réseaux sociaux | Liens Facebook, Instagram |
| 🕐 Horaires | Tous les jours, message spécial |
| 🎬 Bandeau vidéo | Changer la vidéo, le poster, les textes |
| 👨‍👩‍👧 À propos | Photo, texte, valeurs |
| 📷 Photos équipe | Ajouter/modifier membres + photos |
| 🏭 Galerie atelier | Ajouter/supprimer des photos |
| 💬 Popup | Activer, rédiger, choisir le type, date de fin |
| 🔔 Bandeau alerte | Activer, texte (fermeture, promo, événement...) |
| 📅 Événements | Créer/modifier des articles d'actualité |

### Workflow d'une modification

1. Aller sur `/admin`
2. Se connecter avec email + mot de passe
3. Choisir la section à modifier dans le menu gauche
4. Modifier les champs → cliquer **Publish**
5. Netlify redéploie automatiquement en ~30 secondes
6. Le site est mis à jour

---

## Exemple : Activer le bandeau de fermeture estivale

1. Admin → **📣 Popup & Alertes** → **🔔 Bandeau d'alerte**
2. **Afficher le bandeau** → cocher ✅
3. **Type** → Fermeture exceptionnelle
4. **Texte** → `Fermé du 11 au 25 août. Réouverture lundi 26 août dès 8h.`
5. **Date de fin** → 25/08/2026
6. Cliquer **Publish**

Le bandeau orange apparaît en haut du site et disparaît automatiquement le 26 août.

---

## Questions fréquentes

**Le site ne se met pas à jour après une modification ?**
→ Attendre 30-60 secondes. Si toujours pas, aller dans Netlify → Deploys → vérifier le statut.

**Marie-France a oublié son mot de passe ?**
→ Netlify → Identity → cliquer sur son email → "Send reset password email"

**Ajouter un nouvel employé à l'équipe ?**
→ Admin → 📷 Photos du site → 👥 Photos de l'équipe → cliquer "+" pour ajouter un membre.
