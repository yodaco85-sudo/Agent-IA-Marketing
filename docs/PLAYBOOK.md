# PLAYBOOK

> Méthode de travail du projet. À lire avant toute modif.

## Ajouter un nouveau client
1. `cp -r clients/_template clients/<nouveau-client>` (ou copier tahiti-demenage-tout)
2. Remplir `voice.md` (ton, expressions, structure, CTA, services, longueur)
3. Remplir `sources.md` (RSS, Google News, sites)
4. Ajouter le client dans la table Airtable « Clients »
5. Dupliquer le workflow n8n et changer les paramètres (sources, ton, canal)

## Ajouter une source de veille
1. L'ajouter dans `clients/<client>/sources.md`
2. L'ajouter dans la table Airtable « Sources » (thème + actif)
3. Relancer une veille de test

## Créer une nouvelle compétence (newsletter, SEO, LinkedIn…)
1. Nouveau prompt dans `prompts/`
2. Nouveau bout de workflow qui consomme la **même veille validée**
3. Documenter dans `DECISIONS.md`

## Modifier un prompt
- Toujours versionner (git). Un prompt = un commit.
- Tester sur un cas réel avant de pousser.

## Tester un workflow
- Jeu de test dans `tests/`
- Vérifier : doublons écartés, score cohérent, ton respecté, CTA présent

## Déployer une nouvelle version
- Tagger (`v0.2`), noter dans `DECISIONS.md`, mettre à jour `ROADMAP.md`
