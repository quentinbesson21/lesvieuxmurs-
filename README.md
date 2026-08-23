# Les Vieux Murs — site vitrine

Site d'une page pour le restaurant **Les Vieux Murs**, remparts d'Antibes.
Construit sur la nouvelle charte graphique : vert profond `#1A3224`, sable `#D7C6A7`, ivoire `#F8F6F2`.

Aucune dépendance, aucun build. Un fichier HTML, ses images et sa vidéo.

## Arborescence

```
.
├── index.html                    tout le site : structure, styles, scripts
├── assets/
│   ├── img/
│   │   ├── lvm-hero-poster.jpg   image d'attente de la vidéo
│   │   ├── lvm-salle-voutee.jpg  section « Découvrir »
│   │   ├── lvm-logo.png          logotype détouré, fond transparent
│   │   ├── favicon.png
│   │   └── apple-touch-icon.png
│   └── video/
│       ├── lvm-hero-1080.mp4     boucle du haut de page, écrans larges
│       └── lvm-hero-720.mp4      même boucle, écrans étroits
└── tools/
    └── build-hero.sh             remonte la vidéo depuis les rushes
```

## Voir le site en local

Ouvrir `index.html` dans un navigateur suffit. Pour un contexte identique à la
production (chemins relatifs, lecture vidéo) :

```bash
python3 -m http.server 8000
# puis http://localhost:8000
```

## Mise en ligne sur GitHub Pages

1. Pousser le dépôt sur GitHub.
2. `Settings` → `Pages` → source `Deploy from a branch`, branche `main`, dossier `/ (root)`.
3. Le site est servi à `https://<utilisateur>.github.io/<dépôt>/` en une minute environ.

Rien à configurer de plus : pas de générateur statique, donc pas besoin de `.nojekyll`
tant qu'aucun fichier ou dossier ne commence par un underscore.

Pour un nom de domaine, ajouter un fichier `CNAME` à la racine contenant le domaine,
puis pointer l'enregistrement DNS vers GitHub Pages.

## La vidéo du haut de page

Boucle muette de 21,5 s, montée à partir de sept rushes : cinq plans enchaînés en
fondus de 0,9 s, suivant le déroulé d'un service. Le dernier plan se dissout dans le
premier, la boucle démarre et finit sur la même image.

L'étalonnage est calé sur la charte : noirs relevés vers le vert, hautes lumières
poussées vers le sable, saturation à 0,78.

> **À traiter avant mise en ligne.** Les rushes utilisés portent le filigrane Artlist —
> ce sont les fichiers de prévisualisation. Une fois les versions sous licence
> téléchargées, relancer `tools/build-hero.sh` en ajustant le chemin `SRC` : mêmes
> points d'entrée, même étalonnage, montage identique sans filigrane.
>
> Les plans montrent une salle contemporaine, pas les voûtes ni la vue sur la baie.
> Des images tournées sur place remplaceraient utilement les plans 1 et 5.

Le script demande `ffmpeg` et `ffprobe` :

```bash
bash tools/build-hero.sh
```

## Typographies

Chargées depuis Google Fonts.

- **Fraunces** — titres et noms de plats. Substitut libre de TT Ramillas, la police de
  la charte : même élégance sérif contrastée, italique fluide. Si la licence TT Ramillas
  est acquise, la substitution se fait dans la variable CSS `--display`.
- **Archivo** (variable) — texte courant et micro-libellés en capitales espacées.

## Contenu

Les plats, prix, horaires, adresse et le parcours du chef proviennent du site actuel
`lesvieuxmurs.com`. La carte évolue avec les saisons : penser à la resynchroniser.

Le lien de réservation pointe vers le compte Zenchef existant.

## Accessibilité

- Repères de focus visibles, lien d'évitement vers le contenu.
- Onglets de la carte navigables au clavier (flèches gauche / droite).
- `prefers-reduced-motion` respecté : la vidéo laisse place à l'image fixe et les
  animations d'apparition sont désactivées.
- Bascule automatique sur la version 720p si le mode économie de données est actif.
