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

---

## Hygiène MCP (règle Besmara)

> Principe : **un projet ne charge que les MCP qu'il lui faut. Jamais de global permanent.**
> Deux couches distinctes — ne pas les confondre.

### Couche 1 — Claude Code (terminal)
Chaque dépôt est autonome :

1. **`.mcp.json` à la racine** déclare uniquement les serveurs utiles au projet.
2. **`.claude/settings.json`** (committé) → `"enabledMcpjsonServers": ["...]"` liste ces serveurs.
3. **Aucun serveur en scope `user`** (`claude mcp add -s user`) → sinon il se charge partout.
4. **Secrets toujours en variable d'env**, jamais en clair dans `.mcp.json` :
   ```json
   "env": { "MON_API_KEY": "${MON_API_KEY}" }
   ```
   La vraie valeur va dans `.env` (gitignoré). Fournir un `.env.example`.

Vérifier avant chaque push qu'aucune clé ne part au commit :
```bash
git grep -nI "eyJhbG\|API_KEY=ey" -- . ':!*.example'   # doit ne rien retourner
git check-ignore .env                                   # doit afficher .env
```

### Couche 2 — Connecteurs Claude desktop (Cowork)
Ce sont les connecteurs de l'app (Notion, Gmail, Airtable…), **pas** des MCP Claude Code.
Ils sont globaux et **non scopables par fichier**. Les désactiver à la main dans
**Réglages → Connecteurs** quand on ne s'en sert pas. À faire régulièrement.

### Checklist nouveau projet
- [ ] `.mcp.json` = strict nécessaire
- [ ] `.claude/settings.json` aligné
- [ ] secrets en `${VAR}` + `.env.example`
- [ ] `.env` et `.claude/settings.local.json` dans `.gitignore`
- [ ] scan secrets OK avant le premier push
