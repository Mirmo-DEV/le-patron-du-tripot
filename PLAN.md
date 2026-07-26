# PLAN — Le Patron du Tripot (clicker casino)

Jeu de clic / idle sur le thème du casino. Un seul fichier `index.html` autonome
(HTML + CSS + JS vanilla). Aucune dépendance externe (Google Fonts en option avec
police de secours). Hébergeable en glissant le fichier sur un hébergement web.

## 1. Mécaniques

- **Jeton central** cliquable : chaque clic rapporte des jetons (valeur de base = 1,
  multipliée par les améliorations de clic, la frénésie, le prestige, les succès…).
  Nombre flottant animé à chaque clic. Activable clavier (Espace / Entrée).
- **10 bâtiments** produisant des jetons/seconde, coût = base × 1,15^possédés.
  Sélecteur d'achat x1 / x10 / max.
- **Améliorations** :
  - Par bâtiment : 3 paliers débloqués à 10 / 25 / 50 exemplaires, chacun ×2 la prod.
  - Clic : série de ×2 successifs.
  - Global : +5 % de production totale (empilables).
  Galerie des améliorations achetées.
- **Roulette du patron** : roue 37 cases (0 inclus), espérance négative.
  Paris Rouge/Noir (×2), Pair/Impair (×2), Douzaine (×3), Plein (×36).
  Mises rapides 10/25/50/tout. Recharge 20–30 s. Historique 10 résultats + stats.
  Architecture prévue pour ajouter blackjack + bandit manchot plus tard.
- **Jeton d'or** : toutes les 60–180 s, traverse l'écran quelques secondes.
  Cliqué : frénésie ×7 (15 s), coffre (10 min de prod), ou clic ×777 (10 s).
- **Gains hors ligne** : 50 % de la prod pendant l'absence, plafonné à 3 h.
- **Prestige** : « revendre l'empire », reset, gagne des diamants (+2 %/diamant).
  Formule racine cubique du total gagné, seuil minimum.
- **Succès** (~25) : chacun +1 % de production totale.
- **Événements aléatoires** rares : inspection / descente, choix payer ou tenter.

## 2. Courbe d'équilibrage (valeurs de départ, ajustées à la Cookie Clicker)

| # | Bâtiment            | Coût base | Prod base (jps) |
|---|---------------------|-----------|-----------------|
| 1 | Machine à sous      | 15        | 0,1             |
| 2 | Table de blackjack  | 100       | 1               |
| 3 | Roulette            | 1 100     | 8               |
| 4 | Salle de poker      | 12 000    | 47              |
| 5 | Bar VIP             | 130 000   | 260             |
| 6 | Hôtel-casino        | 1 400 000 | 1 400           |
| 7 | Casino flottant     | 20 000 000| 7 800           |
| 8 | Quartier de Vegas   | 330 M     | 44 000          |
| 9 | Casino orbital      | 5,1 Md    | 260 000         |
| 10| Casino quantique    | 75 Md     | 1 600 000       |

Clic de base = 1. Espérance roulette ~ -2,7 % (case 0). Prestige : seuil ~1e12 total.

## 3. Structure du code (sections)

1. CONFIG — tableaux `BATIMENTS`, `AMELIORATIONS`, `SUCCES`, `PARIS_ROULETTE`, constantes.
2. ÉTAT (`etat`) — banque, total, clics, possédés, améliorations, prestige, roulette…
3. UTILITAIRES — formatage grands nombres (k/M/Md…), RNG, temps.
4. LOGIQUE — coûts, production/s, achat, améliorations, prestige, succès, événements.
5. BOUCLE — tick logique basé sur `performance.now()` (pas de dérive), rendu 30 fps.
6. SAUVEGARDE — localStorage, auto-save 10 s + `beforeunload`, export/import.
7. ROULETTE — état, mise, tirage, animation.
8. INTERFACE — rendu des panneaux (Boutique / Améliorations / Roulette / Succès / Stats).
9. INIT — chargement, gains hors ligne, écouteurs.

## 4. Direction visuelle

« L'arrière-salle privée à 3 h du matin ». Feutre vert profond, laiton, ivoire,
rouge carmin en accent. Titres en serif gras façon affiche de saloon (Playfair
Display + secours serif), interface en sans condensée (Oswald/Barlow Condensed +
secours). Gros jeton central à bordure laiton crantée, s'enfonce au clic, projette
de petits jetons. Bandeau supérieur (banque + jps), table à gauche, panneau à
onglets à droite. Sur mobile, tout s'empile. `prefers-reduced-motion` respecté,
focus visible, zones tactiles généreuses, pas de zoom double-tap.

## 5. Méthode

Commits atomiques en français, tests à chaque étape (ouverture navigateur, avance
du temps par script, sauvegarde/rechargement, écran étroit), README FR, git local
(gh absent → instructions de mise en ligne fournies).
