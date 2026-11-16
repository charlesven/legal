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
| `predisport` | Pêche en mer – Predisport, app **Android** : `cgu-android`, `confidentialite`, `suppression-compte` (page exigée par Google Play), fr + en/de/es/it (suppression : fr + en). L'iOS garde ses pages sur www.predisport.com | `~/Code/android/predisport-android` : `python3 scripts/export_legal.py <ce dépôt>` (texte de `ui/legal/LegalContent.kt` + `strings_legal.xml`, et `docs/DELETE_ACCOUNT_PAGE.md`) |
| `envie` | Envies (fr + en) | `Developer/Envie/Legal/*.md` (`pk legal --root .` ; EULA ASC rejouée par `scripts/asc_eula.mjs --apply`) |

**Apps retirées de la vente le 14/11/2026, pages conservées** (les apps installées y renvoient ; l'abonné d'Anti-Dépense
garde l'app jusqu'au 04/10/2027 : ne rien supprimer ici) : `antidepense` (Anti-Dépense, support + CGU + confidentialité)
et `carburant` (Je fais le plein ?). Puzzle Contest n'a pas de page dans ce dépôt : ses pages étaient servies par la
fonction Supabase `legal` de son projet, supprimé le 15/11/2026.

Hors de ce dépôt, en attendant une migration : **Ceramist** sert ses pages depuis la
fonction Supabase `legal` de son projet (`https://mannxvoyxbfbnuyitmou.supabase.co/functions/v1/legal/cgu`, `?lang=en` pour l'anglais, texte brut sur
`*.supabase.co`), source `supabase/functions/legal/index.ts` ; **Predisport** sur son site React.

## EULA personnalisée d'App Store Connect (état au 05/10/2026)

Les cinq apps ont une EULA personnalisée sur les 175 territoires, texte brut des CGU du jour (règle « si tu annules
pendant l'essai gratuit, l'accès s'arrête immédiatement », et pour Anti-Dépense l'achat « à vie ») : Envies,
Je fais le plein ?, Anti-Dépense (`Legal/cgu.md` → texte, mise en forme de `Envie/scripts/asc_eula.mjs`), Ceramist et
Puzzle Contest (texte français servi par la fonction `legal`). La ligne « Conditions d'utilisation (EULA) : … » en fin
de description pointe vers la page CGU de l'app, plus jamais vers la `stdeula` d'Apple. À rejouer après toute
retouche des CGU, sinon l'app, le web et App Store Connect se contredisent.
