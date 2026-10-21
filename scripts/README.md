# Travailler sur le site de Porcom

Du HTML statique, une feuille de style et un petit script, publiés par GitHub Pages. Le design, en mode sombre
seulement, s’inspire de Rollie (via One Page Love), comme celui de Reliure (`../reliure`).

## Pages

| English | Français |
| --- | --- |
| `/` | `/fr/` |
| `/support/` | `/fr/assistance/` |
| `/privacy/` | `/fr/confidentialite/` |

L’anglais est la langue par défaut (`x-default`). Chaque page déclare son équivalent (`hreflang`) et
le lien de langue mène à la même page dans l’autre langue. Les liens sont relatifs
(`../assets/…`), donc les pages s’ouvrent aussi bien depuis le disque que servies d’un sous-dossier ;
seule `404.html` garde des liens depuis la racine, puisque GitHub Pages la sert à n’importe quelle adresse. Le français est tutoyé, comme
l’app, avec des espaces insécables avant `? ! : ;` et dans les « guillemets ».

## Au quotidien

- **Styles** : modifier `assets/style.css`, puis `scripts/build-css.sh` pour produire `style.min.css`,
  que les pages chargent. Le logo est l’avatar du blogue détouré (`assets/logo-blog.png`) ; les favicons
  restent l’icône de l’app.
- **Script** : `assets/main.js` fait apparaître les sections au défilement ; sans JavaScript, tout reste visible.
- **Captures de l’app** : `scripts/capture-screens.sh fr` (puis `en`) compile l’app, la lance dans
  le simulateur avec les données de démo du blogue et capture les sept écrans de la rangée, en sombre,
  en AVIF et WebP. `SCREENS="home:"` n’en refait qu’une partie ; `APPEARANCES="light dark"` capture aussi le clair.
- **Prévisualiser** : ouvrir `index.html`, ou `python3 -m http.server` à la racine puis http://localhost:8000.
- **Publier** : un push sur `main` déploie avec `.github/workflows/pages.yml`.

## Avant le lancement

- **App Store** : l’app n’est pas encore en ligne. À sa sortie, transformer « Coming soon to the App Store » /
  « Bientôt sur l’App Store » (en-tête, titre, appel à l’action) en lien vers l’App Store, régénérer le QR code
  (`npx qrcode -t svg -d '#f2f2f3' -l '#0000' -m 0 -o assets/qr.svg <lien>`, il mène à porcom.app pour l’instant)
  et ajouter `apple-itunes-app` et `installUrl` dans le JSON-LD.
- **Captures** : sans jeton TMDB, les affiches sont des affiches de remplacement et l’écran d’ajout
  dit que la recherche est indisponible. Avec un jeton dans `Config/Secrets.xcconfig`, relancer les captures.

