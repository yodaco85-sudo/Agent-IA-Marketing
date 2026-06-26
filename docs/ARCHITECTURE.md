# ARCHITECTURE

> Template Besmara. Décrit le **comment**, pas le **pourquoi** (ça, c'est le PRD).

## Vue d'ensemble

```
Sources d'information
        │
        ▼
Collecte automatique        ← RSS, Google News, sites, réseaux
        │
        ▼
Filtrage IA                 ← doublons, score d'intérêt, classement
        │
        ▼
Résumé des actualités
        │
        ▼
Proposition de 3 sujets
        │
        ▼
Validation humaine          ← mail ou Slack, 1 réponse
        │
        ▼
Rédaction                   ← dans la voix du client
        │
        ▼
Relecture IA                ← orthographe, style, CTA, longueur
        │
        ▼
Brouillon Brevo / Mailchimp ← jamais d'envoi auto sans validation
```

## Composants

| Brique             | Outil retenu                          | Pourquoi                          |
|--------------------|---------------------------------------|-----------------------------------|
| Orchestration      | n8n (auto-hébergé)                    | Modulaire, lisible, déjà maîtrisé |
| IA                 | Claude (rédaction) / GPT (filtrage)   | Voix + raisonnement               |
| Veille             | RSS + Google News + Scrapling au besoin | Gratuit, robuste                |
| Base de données    | Airtable ou Notion                    | Historique + interface humaine    |
| Historique         | Airtable                              | Anti-redite, suivi des sujets     |
| Envoi              | Brevo ou Mailchimp                    | Brouillon, pas d'envoi sec        |
| Mémoire du ton     | Markdown dans `clients/<client>/`     | Versionné, éditable à la main     |

## Modèle de données (Airtable)

- **Sources** : url, type (RSS/News/site), thème, actif (bool), client
- **Articles collectés** : titre, url, date, source, thème, score, statut (brut/retenu/écarté), hash anti-doublon
- **Sujets proposés** : semaine, articles liés, angle, score, statut (proposé/validé/refusé)
- **Contenus produits** : type (newsletter/blog/LinkedIn…), sujet, statut (brouillon/relu/publié), url Brevo
- **Clients** : nom, secteur, fréquence, ton (lien Markdown), services, canaux actifs

## Mémoire

Deux niveaux :
1. **Mémoire du ton** (statique, éditée à la main) → `clients/<client>/voice.md`
2. **Mémoire d'historique** (dynamique) → Airtable, pour ne pas reproposer un sujet déjà traité

## Gestion des erreurs

- Chaque exécution écrit un log (succès/échec par étape)
- Reprise possible à partir de la dernière étape validée
- Aucune publication automatique : le pire cas = un brouillon à jeter
