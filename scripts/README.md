# Travailler sur le site de Porcom

Du HTML statique, une feuille de style et un petit script, publiés par GitHub Pages. Le design, en mode sombre
seulement, reprend celui de Reliure (`../reliure`) : titres en Headland One (hébergée dans `assets/fonts/`),
texte en Helvetica, et un accueil en deux colonnes, les mots à gauche, un grand iPhone à droite dont l’écran
suit la section lue. Le rouge de Porcom sert au trait de surligneur du titre, au halo et aux anneaux de focus.

## Pages

| English | Français | Español |
| --- | --- | --- |
| `/` | `/fr/` | `/es/` |
| `/support/` | `/fr/assistance/` | `/es/soporte/` |
| `/privacy/` | `/fr/confidentialite/` | `/es/privacidad/` |
| `/tv-show-tracker/` | `/fr/suivi-de-series/` | `/es/seguimiento-de-series/` |
| `/movie-diary/` | `/fr/journal-de-films/` | `/es/diario-de-peliculas/` |
| `/watchlist-app/` | `/fr/liste-a-voir/` | `/es/lista-para-ver/` |
| `/year-in-review/` | `/fr/bilan-annuel/` | `/es/resumen-anual/` |
| `/where-to-watch/` | `/fr/ou-regarder/` | `/es/donde-ver/` |
| `/tv-time-alternative/` | `/fr/alternative-tv-time/` | `/es/alternativa-tv-time/` |
| `/letterboxd-alternative/` | `/fr/alternative-letterboxd/` | `/es/alternativa-letterboxd/` |
| `/trakt-alternative/` | `/fr/alternative-trakt/` | `/es/alternativa-trakt/` |
| `/serializd-alternative/` | `/fr/alternative-serializd/` | `/es/alternativa-serializd/` |
| `/whats-new/` | `/fr/nouveautes/` | `/es/novedades/` |

Les guides (suivi de séries, journal de films, liste à voir, bilan, où regarder) suivent la mise en page de
l’accueil, téléphone à droite ; les pages « alternative à… » et les nouveautés sont en une colonne. Les
tableaux comparatifs datent de novembre 2026 : revérifier les faits des concurrents (prix, pubs, compte)
avant de changer la date « Dernière mise à jour ». L’accueil les liste tous dans la section « Guides ».

L’espagnol (`/es/`) ne traduit que le site : l’app est en anglais et en français. Les pages espagnoles le
disent, montrent les captures anglaises et gardent les libellés de l’app en anglais (Continue, To watch,
Profile › Data…). Espagnol neutre, tutoyé. L’anglais est la langue par défaut (`x-default`). Chaque page déclare son équivalent (`hreflang`) et
le lien de langue mène à la même page dans l’autre langue. Les liens sont relatifs
(`../assets/…`), donc les pages s’ouvrent aussi bien depuis le disque que servies d’un sous-dossier ;
seule `404.html` garde des liens depuis la racine, puisque GitHub Pages la sert à n’importe quelle adresse. Le français est tutoyé, comme
l’app, avec des espaces insécables avant `? ! : ;` et dans les « guillemets ».

## Au quotidien

- **Styles** : modifier `assets/style.css`, puis `scripts/build-css.sh` pour produire `style.min.css`,
  que les pages chargent. Le logo est l’avatar du blogue détouré (`assets/logo-blog.png`) ; les favicons
  restent l’icône de l’app.
- **Script** : `assets/main.js` change l’écran du téléphone selon la section lue et ajoute les points de navigation ; sans JavaScript, le premier écran reste affiché.
- **Captures de l’app** : `scripts/capture-screens.sh fr` (puis `en`) compile l’app, la lance dans
  le simulateur avec les données de démo du blogue et capture les sept écrans du téléphone, en sombre,
  en AVIF et WebP. `SCREENS="home:"` n’en refait qu’une partie ; `APPEARANCES="light dark"` capture aussi le clair.
- **Prévisualiser** : ouvrir `index.html`, ou `python3 -m http.server` à la racine puis http://localhost:8000.
- **Publier** : un push sur `main` déploie avec `.github/workflows/pages.yml`.

## Lancement

- **App Store** : les liens pointent vers https://apps.apple.com/app/id6825954523 (en-tête, titre, appel à
  l’action, pied de page, `apple-itunes-app`, `installUrl` du JSON-LD). Le QR code y mène aussi ; pour le
  régénérer : `npx qrcode -t svg -d '#f2f2f3' -l '#0000' -m 0 -o assets/qr.svg <lien>`.
- **Captures** : sans jeton TMDB, les affiches sont des affiches de remplacement et l’écran d’ajout
  dit que la recherche est indisponible. Avec un jeton dans `Config/Secrets.xcconfig`, relancer les captures.

