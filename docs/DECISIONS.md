# DECISIONS

> Journal des choix structurants. Append-only, daté. On ne réécrit pas le passé.

## [2026-06-26] Agent éditorial, pas workflow Make
On construit un mini agent qui **décide** (tri, redites, angle), pas un simple
enchaînement d'actions. Orchestration sur **n8n** (auto-hébergé), pas Make :
cohérent avec la stack Besmara, modulaire, pas de coût par opération.

## [2026-06-26] Validation humaine obligatoire
Aucune rédaction sans validation des sujets. Aucun envoi sans relecture d'un
brouillon. Évite l'essentiel des erreurs. Le pire cas reste un brouillon à jeter.

## [2026-06-26] Produit réutilisable, pas projet client unique
Le dépôt est un **template Besmara**. Tahiti Déménage Tout est le premier client,
pas la cible du dépôt. Une veille validée doit pouvoir nourrir plusieurs canaux.
