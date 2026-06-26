# DEMO — AI Marketing Agent (Tahiti Déménage Tout)

> Déroulé de démonstration. Objectif : montrer que l'agent **décide**, pas qu'il
> enchaîne des actions. Durée cible : 8–10 min. À répéter une fois avant le jour J.

## Le message à faire passer

Une seule veille validée → un contenu prêt à publier, dans la voix de l'entreprise,
avec l'humain qui garde la main aux deux moments qui comptent. Pas une usine à gaz :
une bécane qui tient la route, montable en quelques heures, ~20–60 €/mois.

## Avant de commencer (checklist technique)

- [ ] `.env` rempli (clé n8n) au bon chemin
- [ ] n8n joignable (workflow `wf-veille` actif)
- [ ] Une boîte mail / canal Slack ouvert pour montrer la validation
- [ ] Brevo ouvert sur l'écran (pour montrer le brouillon en fin)
- [ ] Le `voice.md` ouvert dans un onglet — c'est ton argument massue

## Déroulé (5 actes)

### Acte 1 — Le problème (1 min)
Pose le décor sans slide : une TPE n'a ni le temps de surveiller son secteur, ni
celui de rédiger chaque semaine dans un ton constant. Résultat : elle ne publie rien,
ou ça part dans tous les sens.

### Acte 2 — La veille qui trie (2 min)
Lance la collecte. Montre la sortie : une liste d'actus **scorées**.
Insiste sur le tri — l'agent écarte les doublons et les hors-sujet.

| Sujet                              | Score |
|------------------------------------|-------|
| Hausse des frais de fret           | 95    |
| Nouvelle aide au logement          | 92    |
| Conseils pour emballer les plantes | 88    |
| Actualité sans rapport             | 15    |

Phrase à dire : « Il ne ramasse pas tout. Il choisit. »

### Acte 3 — La validation humaine (2 min)
Montre le mail/Slack reçu : **3 sujets proposés**. Tu réponds en direct (« 2 »,
ou « mélange 1+3 »). C'est LE moment qui rassure un patron : rien ne part sans lui.
Phrase à dire : « L'humain garde la main. La machine propose, le patron tranche. »

### Acte 4 — La rédaction dans la voix (2 min)
L'agent rédige. Montre `voice.md` à côté : tutoiement, chaleureux et pro, on informe
avant de vendre. Compare le rendu au ton du fichier. Phrase à dire : « Ce n'est pas
une IA générique. C'est l'équipe marketing de l'entreprise. »

### Acte 5 — Le brouillon, pas l'envoi (1 min)
L'agent crée un **brouillon Brevo**. Jamais d'envoi automatique. Le patron relit,
ajuste, envoie quand il veut. Phrase à dire : « Le pire cas, c'est un brouillon à jeter.
Zéro risque d'envoyer une bêtise à toute la base. »

## La bascule (30 s) — pourquoi c'est un produit, pas un gadget
La même veille validée peut nourrir un article de blog, trois posts réseaux, un post
LinkedIn, une FAQ. Une recherche → tous les canaux. Et le tout se réadapte à une autre
entreprise en changeant 4 fichiers : nom, ton, sources, services.

## Questions probables + réponses courtes

- **« Et si l'IA invente un truc faux ? »** → Sources tracées, relecture qui chasse
  les hallucinations, et surtout : validation humaine avant tout envoi.
- **« Combien ça coûte ? »** → ~20–60 €/mois en stack légère. Rarement plus de 100 €.
- **« Combien de temps pour l'installer ? »** → 12–16 h de build, 20–25 h en version
  robuste avec logs et reprise sur erreur.
- **« C'est verrouillé à une seule entreprise ? »** → Non. C'est un template. On
  rebranche un autre client en changeant le ton, les sources et les services.

## Ce qu'il NE faut PAS faire en démo
- Promettre un délai chiffré au client final (« newsletter prête en 30 jours »)
- Montrer un envoi automatique sans validation (ça casse l'argument de confiance)
- Improviser sur des chiffres : si tu n'as pas la donnée, tu ne l'inventes pas
