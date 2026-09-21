# legal — pages légales de toutes les apps (GitHub Pages)

Un seul dépôt public, servi par GitHub Pages à `https://charlesven.github.io/legal/`, pour héberger les CGU (EULA
personnalisée) et les politiques de confidentialité de toutes les apps iOS. Plus aucune page légale dans un projet
Supabase ou un site React : une URL stable par document, HTTP 200 garanti, versionnée par git.

## Convention

```
<slug-app>/cgu.html               Conditions d'utilisation (champ « Contrat de licence » d'App Store Connect + description)
<slug-app>/confidentialite.html   Politique de confidentialité (champ dédié d'App Store Connect)
style.css                         feuille commune, index.html liste toutes les apps
```

- **Le texte vit dans l'app** (fichier `Legal.swift` ou équivalent), affiché dans l'app même hors ligne ; les pages HTML
  sont **générées** par un script du projet de l'app (`scripts/export_legal.sh` dans Carburant), jamais éditées ici à la main.
- Une édition = un slug (`carburant`, `carburant-pro`). Une langue = un suffixe si besoin (`cgu.en.html`).
- Dans l'app : `Legal.cguURL` / `Legal.privacyURL` pointent ici ; dans App Store Connect : mêmes URL, et la ligne
  « Conditions d'utilisation (EULA) : … » en fin de description (check-list `~/.claude/app-store-review-checklist.md`).
- Mise en ligne : `git add -A && git commit -m "carburant: CGU du 21 septembre 2026" && git push` ; GitHub Pages
  publie `main` à la racine en une minute. Vérifier `curl -I` → 200 avant toute soumission.

## Apps

| Slug | App | Source |
|---|---|---|
| `carburant` | Carburant (édition particulier) | `Developer/Carburant/Carburant/Views/Soutien/Legal.swift` |
| `carburant-pro` | Carburant Pro | idem, `Legal.cgu(.pro)` |

À migrer ici quand l'occasion se présente : Ceramist (`legal` Supabase), Predisport (site React), Résiste.
