# PRD — AI Marketing Agent
### Premier client : Tahiti Déménage Tout — Newsletter hebdomadaire

> Document de référence. Répond à **« qu'est-ce qu'on construit ? »**, pas au « comment ».
> Pensé pour qu'un agent de dev (Claude Code) puisse construire sans poser 40 questions.
> Statut : v0 — à valider avec Yoann avant développement.

---

## 1. Vision du produit

Un agent éditorial IA qui transforme une **veille d'information** en **contenus
prêts à publier**, dans la voix de l'entreprise cliente, avec un humain qui valide
aux deux points clés (choix des sujets, validation du brouillon).

Ce n'est pas une automatisation dédiée à une newsletter. C'est un **socle réutilisable** :
une seule veille validée peut nourrir newsletter, blog SEO, posts réseaux, LinkedIn, FAQ.
Tahiti Déménage Tout est le premier cas d'usage, pas la finalité.

## 2. Problème résolu

Une TPE/PME n'a ni le temps ni les compétences pour :
- surveiller en continu son secteur,
- trier ce qui mérite d'être dit,
- rédiger régulièrement dans un ton cohérent,
- alimenter plusieurs canaux sans tout refaire à chaque fois.

Résultat habituel : communication irrégulière, ton qui dérive, ou rien du tout.

## 3. Objectifs métier

- Publier **une newsletter hebdomadaire** sans y passer plus de **15 min/semaine** côté client.
- Garder un **ton constant** (celui de l'entreprise, pas celui d'une IA générique).
- **Zéro contenu inventé** : pas de statistique non vérifiée, pas d'hallucination.
- Poser les bases d'un **produit réutilisable** pour d'autres clients Besmara.

## 4. Personas

| Persona            | Besoin                                              | Interaction              |
|--------------------|-----------------------------------------------------|--------------------------|
| Administrateur     | Installer, configurer sources/ton, surveiller       | n8n, Airtable            |
| Responsable marketing (client) | Choisir les sujets, valider le brouillon | 1 mail ou message Slack  |
| Lecteur final      | Recevoir une newsletter utile et cohérente          | Email                    |

## 5. Cas d'usage (v0.2 — newsletter)

1. Lundi 8 h : l'agent collecte l'actualité du secteur.
2. Il déduplique, score, classe.
3. Il envoie **3 propositions de sujets** au client.
4. Le client répond (ex. « 2 » ou « mélange 1+3 »).
5. L'agent rédige la newsletter dans la voix Tahiti Déménage Tout.
6. Relecture IA (style, CTA, longueur, orthographe).
7. Création d'un **brouillon Brevo** — pas d'envoi automatique.
8. Le client relit, ajuste si besoin, envoie.

## 6. Fonctionnalités

### Veille
Sources : déménagement, transport, logement, immobilier, mutation professionnelle,
aides au logement, vie à Tahiti / Polynésie, conseils pratiques, événements locaux.
Collecte RSS + Google News + scraping ciblé si nécessaire.

### Filtrage / scoring
Score d'intérêt par sujet (0–100), suppression des doublons, écart des hors-sujet.
Exemple de logique :

| Sujet                              | Score |
|------------------------------------|-------|
| Hausse des frais de fret           | 95    |
| Nouvelle aide au logement          | 92    |
| Conseils pour emballer les plantes | 88    |
| Actualité sans rapport             | 15    |

### Proposition + validation humaine
3 sujets max envoyés par mail/Slack. Réponse libre (numéro ou mélange).
**Indispensable** : la rédaction ne démarre qu'après validation.

### Rédaction
Prompt enrichi du contexte client : ton, expressions, structure, CTA, services, longueur cible.

### Relecture
Second passage IA : redites, hallucinations, CTA présent, longueur, fluidité, orthographe.

### Publication
Brouillon Brevo (préféré). Jamais d'envoi sec automatique.

## 7. Architecture des workflows n8n

Voir `ARCHITECTURE.md`. Workflows attendus :
- `wf-veille` (collecte + dedup + score)
- `wf-proposition` (3 sujets → validation)
- `wf-redaction` (rédaction + relecture → brouillon Brevo)

Modulaires, lisibles, sans duplication.

## 8. Modèle de données

Voir `ARCHITECTURE.md` (Sources, Articles collectés, Sujets proposés, Contenus produits, Clients).

## 9. Mémoire

- **Ton** : `clients/tahiti-demenage-tout/voice.md` (statique, édité à la main).
- **Historique** : Airtable, pour ne pas reproposer un sujet déjà traité.

## 10. Prompts LLM

Stockés dans `prompts/` : `scoring.md`, `redaction.md`, `relecture.md`.
Versionnés. Un prompt = un commit.

## 11. Validation humaine

Deux points de contrôle non négociables :
1. Choix des sujets (avant rédaction).
2. Brouillon (avant envoi).

## 12. Journalisation et erreurs

Log par exécution et par étape. Reprise depuis la dernière étape valide.
Aucune publication automatique → tolérance aux pannes élevée.

## 13. Critères d'acceptation (v0.2)

- [ ] Le lundi, 3 sujets pertinents et non redondants arrivent au client.
- [ ] Une réponse simple déclenche la rédaction.
- [ ] La newsletter respecte le ton défini dans `voice.md` (jugé par le client).
- [ ] Aucune statistique inventée ; sources traçables.
- [ ] Un brouillon Brevo est créé, jamais un envoi direct.
- [ ] Le client passe ≤ 15 min/semaine.

## 14. Hors périmètre (v0.2)

- Envoi automatique sans validation.
- Génération multicanal (repoussée v0.3+).
- Gestion de la base d'abonnés (reste côté Brevo).

## 15. Budget & effort (estimation)

**Développement** (qqn qui connaît n8n) :

| Étape              | Temps      |
|--------------------|------------|
| Veille             | 2–3 h      |
| Résumé IA          | 1 h        |
| Choix des sujets   | 1 h        |
| Prompt rédaction   | 2–3 h      |
| Mémoire du ton     | 2 h        |
| Publication Brevo  | 1 h        |
| Tests              | 2–3 h      |
| **Total**          | **12–16 h** |

Version robuste (logs, reprise, gestion fine des erreurs) : **20–25 h**.

**Coût mensuel** (stack légère) :

| Service  | Prix       |
|----------|------------|
| n8n      | 0 € (auto-hébergé) ou 20 € cloud |
| LLM      | 10–30 € selon volume |
| Airtable | 0–20 €     |
| Brevo    | 0–25 €     |
| RSS      | 0 €        |
| **Total**| **~20–60 €/mois** |

Peu probable de dépasser 100 €/mois même avec plusieurs newsletters.

## 16. Roadmap

Voir `ROADMAP.md` (v0.1 veille → v1.0 template Besmara).
