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

- **Le texte vit dans le projet de l'app** (`Legal/*.md`, embarqués dans le bundle et affichés hors ligne) ; les pages
  HTML sont **générées** par `pk legal --root <projet> --out <ce dépôt>` (outil PlatformKit), jamais éditées ici à la
  main. Anciens projets : un `scripts/export_legal.sh` maison, à migrer vers `pk legal` à l'occasion.
- Une app = un slug (`carburant`). Une langue = un suffixe si besoin (`cgu.en.html`).
- Dans l'app : `Legal.cguURL` / `Legal.privacyURL` pointent ici ; dans App Store Connect : mêmes URL, et la ligne
  « Conditions d'utilisation (EULA) : … » en fin de description (check-list `~/.claude/app-store-review-checklist.md`).
- Mise en ligne : `git add -A && git commit -m "carburant: CGU du 21 septembre 2026" && git push` ; GitHub Pages
  publie `main` à la racine en une minute. Vérifier `curl -I` → 200 avant toute soumission.

## Apps

| Slug | App | Source |
|---|---|---|
| `carburant` | Je fais le plein ? (version particulier et version Pro, une seule app depuis la 1.1 ; le slug `carburant-pro` de l'ancienne app Pro a été retiré le 30/09/2026) | `Developer/Carburant/Legal/*.md` (`pk legal --root .`) |
| `antidepense` | Anti-Dépense (+ `index.html` : page de support, URL support d'App Store Connect ; fr + en) | `Developer/Resiste/Legal/*.md` (`pk legal --root .` ; l'ancien `Scripts/export_legal.sh` et `Legal.swift` ont disparu) |
| `envie` | Envies (fr + en) | `Developer/Envie/Legal/*.md` (`pk legal --root .` ; EULA ASC rejouée par `scripts/asc_eula.mjs --apply`) |

Hors de ce dépôt, en attendant une migration : **Ceramist** et **Puzzle Contest** servent leurs pages depuis la
fonction Supabase `legal` de leur projet (`https://mannxvoyxbfbnuyitmou.supabase.co/functions/v1/legal/cgu` et
`https://hukhymphvuyduftogcpz.supabase.co/functions/v1/legal/cgu`, `?lang=en` pour l'anglais, texte brut sur
`*.supabase.co`), source `supabase/functions/legal/index.ts` ; **Predisport** sur son site React.

## EULA personnalisée d'App Store Connect (état au 05/10/2026)

Les cinq apps ont une EULA personnalisée sur les 175 territoires, texte brut des CGU du jour (règle « si tu annules
pendant l'essai gratuit, l'accès s'arrête immédiatement », et pour Anti-Dépense l'achat « à vie ») : Envies,
Je fais le plein ?, Anti-Dépense (`Legal/cgu.md` → texte, mise en forme de `Envie/scripts/asc_eula.mjs`), Ceramist et
Puzzle Contest (texte français servi par la fonction `legal`). La ligne « Conditions d'utilisation (EULA) : … » en fin
de description pointe vers la page CGU de l'app, plus jamais vers la `stdeula` d'Apple. À rejouer après toute
retouche des CGU, sinon l'app, le web et App Store Connect se contredisent.
