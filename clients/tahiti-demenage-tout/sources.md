# Sources de veille — Tahiti Déménage Tout

> **Statut : cas d'école (démo alternance).**
> Moteur principal = Google News RSS (gratuit, fiable, ciblé Polynésie française).
> Les flux natifs sont des **candidats à confirmer** au moment du build (Claude Code
> teste l'URL RSS réelle avant de la câbler). On ne câble pas une URL non vérifiée.

---

## 1. Moteur principal — Google News RSS

Format d'URL (stable) :
`https://news.google.com/rss/search?q=REQUÊTE&hl=fr&gl=PF&ceid=PF:fr`

- `gl=PF` = géolocalisation Polynésie française
- `hl=fr` / `ceid=PF:fr` = langue + édition française
- Encoder la requête (espaces → `%20`, ou `+`)

### Requêtes par thème

| Thème                  | Requête `q=`                                  |
|------------------------|-----------------------------------------------|
| Déménagement local     | `déménagement Tahiti`                          |
| Inter-îles / transport | `fret inter-îles Polynésie`                    |
| Fret / coût transport  | `coût fret Polynésie`                          |
| Logement               | `logement Polynésie française`                 |
| Immobilier             | `immobilier Tahiti`                            |
| Aides au logement      | `aide logement Polynésie`                      |
| Mutation pro           | `mutation professionnelle Polynésie`           |
| Vie locale / fenua     | `vie quotidienne Tahiti`                       |
| Événements locaux      | `événement Papeete`                            |

> Exemple complet :
> `https://news.google.com/rss/search?q=d%C3%A9m%C3%A9nagement%20Tahiti&hl=fr&gl=PF&ceid=PF:fr`

## 2. Flux natifs — à CONFIRMER au build

Sites d'actu polynésiens vérifiés comme existants. L'URL RSS exacte doit être
testée avant câblage (beaucoup de CMS exposent `/rss`, `/feed` ou `/xml/syndication.rss`).

| Source              | Site                                  | RSS         |
|---------------------|---------------------------------------|-------------|
| Tahiti Infos        | https://www.tahiti-infos.com/         | À confirmer |
| Polynésie La 1ère   | https://la1ere.franceinfo.fr/polynesie/ | À confirmer |
| Tahiti News         | https://www.tahitinews.co/            | À confirmer |
| Tahiti Pratique     | https://en.tahiti-pratique.com/       | À confirmer |

## 3. Conseils pratiques (contenu evergreen)

Pour la rubrique « conseil pratique » de la newsletter, pas besoin de veille temps réel :
banque de sujets intemporels (emballer la vaisselle, protéger les plantes en transport
maritime, débrancher le frigo, checklist J-7…). À stocker dans `knowledge/` plutôt que
dans les sources d'actu.

## Règle anti-redite
Chaque article retenu est haché (url + titre) et stocké dans Airtable.
Un sujet déjà traité n'est jamais reproposé (voir ARCHITECTURE.md › Mémoire).
