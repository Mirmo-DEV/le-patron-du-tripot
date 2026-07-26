# Le Patron du Tripot 🎰

Un jeu de clic / *idle game* sur le thème du casino, jouable dans le navigateur.
Vous n'êtes pas le joueur au tapis : vous êtes **le patron**. Vous démarrez avec une
machine à sous poisseuse dans un bar et vous finissez à la tête d'un empire — casino
orbital et casino quantique compris. Toute la tension est là : votre banque monte
toute seule, mais la table vous propose en permanence de la risquer pour aller plus vite.

> **Ceci est une simulation.** La monnaie (« jetons ») est entièrement fictive.
> Aucun achat réel, aucun gain réel, aucun argent véritable n'est impliqué. Jeu de
> divertissement, sans aucune incitation au jeu d'argent — adapté à un cadre d'animation.

---

## Comment jouer

- **Tapez le gros jeton central** pour gagner des jetons (souris, doigt, ou **Espace / Entrée** au clavier).
- Dans **Boutique**, achetez des bâtiments qui produisent des jetons par seconde
  (sélecteur d'achat **×1 / ×10 / Max**).
- Dans **Améliorations**, débloquez des bonus permanents (×2 par bâtiment, clics plus
  puissants, +5 % de production globale).
- **La roulette du patron** : misez vos propres jetons. Attention, l'espérance est
  volontairement négative (le zéro vert travaille pour la maison) — c'est tentant, jamais rentable.
- Attrapez les **jetons d'or** qui traversent l'écran : frénésie, coffre, ou clics démultipliés.
- Quand la partie s'essouffle, **revendez l'empire (prestige)** : vous repartez de zéro
  mais gagnez des **diamants** permanents (+2 % de production chacun).
- Débloquez les **succès** (chacun donne +1 % de production).

Le jeu tourne aussi quand l'onglet est fermé : à votre retour, vous récupérez
**50 % de la production** de votre absence (plafonnée à 3 heures).

---

## Mettre le jeu en ligne (hébergement web)

Le jeu tient dans **un seul fichier** : [`index.html`](index.html). Aucune installation,
aucune dépendance, aucun serveur particulier.

1. Récupérez le fichier `index.html`.
2. **Déposez-le sur votre hébergement web** (via le gestionnaire de fichiers de votre
   hébergeur, un client FTP, etc.), à la racine ou dans un dossier de votre choix.
3. Ouvrez l'adresse correspondante dans un navigateur. C'est tout.

> 💡 Pour tester en local sans hébergement, il suffit d'ouvrir `index.html` par un
> double-clic. (Certaines fonctions comme le petit son de clic peuvent être bridées
> selon le navigateur en ouverture locale, mais le jeu fonctionne.)

### GitHub Pages (pour faire tester à des amis)

Si vous hébergez le dépôt sur GitHub, vous pouvez obtenir une URL de test gratuite :

1. Sur la page du dépôt : **Settings → Pages**.
2. **Source** : « Deploy from a branch », branche `main`, dossier `/ (root)`. **Save**.
3. Après une minute, votre jeu est en ligne à une adresse du type
   `https://<votre-pseudo>.github.io/<nom-du-depot>/`. Partagez ce lien.

---

## Sauvegarder ma partie

- La partie est **sauvegardée automatiquement** dans votre navigateur (`localStorage`)
  toutes les 10 secondes et à la fermeture de l'onglet.
- Pour ne **rien perdre** (changement d'appareil, vidage du cache…), utilisez l'onglet
  **Stats** :
  - **Exporter la sauvegarde** → copie un code (ou télécharge un fichier `.txt`).
    Gardez-le précieusement.
  - **Importer une sauvegarde** → collez le code pour restaurer votre partie.
- **Tout effacer** repart de zéro (pensez à exporter avant).

⚠️ La sauvegarde automatique est **liée au navigateur et à l'appareil**. Vider les
données du site efface la partie : exportez régulièrement si elle compte pour vous.

---

## Modifier l'équilibrage

Tout est pensé pour être ajusté facilement, **sans être développeur**. Ouvrez
`index.html` dans un éditeur de texte et cherchez la section commentée
`1. CONFIG` (au début de la balise `<script>`). Vous y trouverez, en français :

| Ce que vous voulez changer                 | Où regarder                                   |
|--------------------------------------------|-----------------------------------------------|
| Prix et production des bâtiments           | tableau `BATIMENTS` (`coutBase`, `prodBase`)  |
| Noms / descriptions / paliers des bâtiments| tableau `BATIMENTS` (`nom`, `desc`, `paliers`)|
| Vitesse d'inflation des prix               | constante `FACTEUR_COUT` (par défaut `1.15`)  |
| Valeur d'un clic de base                   | constante `CLIC_BASE`                         |
| Améliorations de clic / globales           | tableaux `AMEL_CLIC` et `AMEL_GLOBAL`         |
| Liste et conditions des succès             | tableau `SUCCES`                              |
| Cotes et types de paris à la roulette      | objet `PARIS_ROULETTE`                        |
| Recharge de la roulette                    | `ROULETTE_RECHARGE_MIN` / `MAX`               |
| Fréquence / durée du jeton d'or            | `OR_MIN`, `OR_MAX`, `OR_DUREE`                |
| Gains hors ligne (part et plafond)         | `HORS_LIGNE_FRACTION`, `HORS_LIGNE_PLAFOND`   |
| Difficulté du prestige                     | constante `PRESTIGE_SEUIL`                    |
| Fréquence des événements aléatoires        | `EVENT_MIN`, `EVENT_MAX`                      |
| Répliques des habitués                     | tableau `REPLIQUES`                           |

Après modification, enregistrez le fichier et rechargez la page. Les grands nombres
s'affichent toujours avec des suffixes lisibles (k, M, Md…), jamais en notation scientifique.

---

## Caractéristiques techniques

- **Un seul fichier autonome** : HTML + CSS + JavaScript vanilla, zéro dépendance
  (polices Google Fonts optionnelles avec police de secours système).
- **Responsive** : jouable au doigt sur téléphone comme au clic sur ordinateur.
- **Accessible** : jeton activable au clavier, focus visible, `prefers-reduced-motion` respecté.
- **Tick logique basé sur le temps réel** : pas de dérive quand l'onglet passe en
  arrière-plan ; animation limitée à 30 images/seconde.
- Architecture prévue pour **ajouter plus tard** un blackjack simplifié et un bandit
  manchot (la roulette sert de modèle).

Bonne nuit à l'arrière-salle, patron. 🃏
