# ai-marketing-agent

Agent éditorial IA réutilisable. Une seule veille validée → plusieurs canaux
(newsletter, blog SEO, réseaux sociaux, LinkedIn, FAQ).

Ce dépôt n'est **pas** une automatisation jetable. C'est un **template Besmara** :
on change le nom, la mission, les sources et le ton — le reste tient.

## Principe

Ce n'est pas un workflow qui enchaîne des actions. C'est un agent qui **décide** :
quels sujets valent le coup, lesquels sont redondants, quel angle prendre.

```
Sources → Veille → Filtrage IA → Résumé → Proposition de sujets
        → Validation humaine (1 clic) → Rédaction (voix client)
        → Relecture IA → Brouillon Brevo/Mailchimp
```

## Structure

| Dossier      | Rôle                                                        |
|--------------|-------------------------------------------------------------|
| `docs/`      | PRD, architecture, roadmap, décisions, playbook, prompts    |
| `prompts/`   | Prompts LLM de production (veille, rédaction, relecture)     |
| `workflows/` | Exports n8n (JSON)                                           |
| `clients/`   | Un dossier par client (ton, sources, services, historique)  |
| `knowledge/` | Bases de connaissances partagées                            |
| `assets/`    | Logos, images, gabarits                                     |
| `tests/`     | Jeux de test, cas limites                                   |

## Premier client

`clients/tahiti-demenage-tout/` — newsletter hebdo, démarrage MVP.

## Pour démarrer avec Claude Code

Lui dire : « Lis tout `docs/` avant d'écrire la moindre ligne. »
Tout le contexte est dans la doc, pas dans ta tête.
