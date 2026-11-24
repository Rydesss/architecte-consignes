---
paths:
  - "[motif 1]"
  - "[motif 2]"
---

<!--
MODÈLE : règle par chemin, fichier `.claude/rules/<sujet>.md` (kit Architecte consignes, v1.1).
Destination : `.claude/rules/[sujet].md` dans le dossier du projet, nom court sans espace. À utiliser pour des règles qui ne valent que pour un dossier ou un type de fichier.
Pour Claude, au remplissage :
- La ligne `---` du frontmatter reste la première ligne du fichier : ne rien écrire au-dessus.
- Seul le champ `paths` est lu dans le frontmatter (mecanismes.md §4) : n'y ajouter ni description ni autre champ.
- Sans `paths`, la règle se charge à chaque session, comme le maître (§1). Avec `paths`, elle se charge quand Claude lit, écrit ou modifie un fichier visé ; après une compaction, elle revient seulement quand Claude retouche un tel fichier (§7).
- Une règle qui doit guider Claude avant qu'il touche un fichier visé (par exemple : où créer un nouveau document) va donc dans le maître.
- Motifs : liste YAML, relatifs au dossier qui contient `.claude` (§4). Mettre chaque motif entre guillemets : en YAML, une valeur qui commence par `*` ou par `{` se lit mal sans eux. Un `[` littéral dans un nom de dossier s'échappe entre guillemets simples (`'photos \[2024/**'`). Si le YAML ne se lit pas, la règle se charge à chaque session, sans signal (erreur visible avec `claude --debug`, §4). Exemples génériques :
  - un dossier et tout son contenu : `"rapports/**/*"` ;
  - un type de fichier, partout : `"**/*.csv"` ;
  - plusieurs extensions : `"**/*.{docx,xlsx}"` ;
  - un type de fichier dans un dossier : `"src/**/*.ts"`.
- N'écrire que les règles propres aux fichiers visés ; ne répéter aucune règle du maître. Tout s'additionne sans priorité (§2) : une exception au maître s'écrit dans le maître, avec sa portée. De même, l'exception qu'une tâche programmée reçoit pour un accord d'ici (G4b) s'écrit dans la clause « Sessions sans surveillance » du maître, avec sa portée.
- Un fichier par sujet ; des sous-dossiers de `.claude/rules/` sont possibles (§1). Tout fichier `.md` de ce dossier est chargé, quel que soit son nom : la copie de sauvegarde d'une règle remplacée se range hors de `.claude/rules/` et de `~/.claude/rules/` (§1). Rester court : au-delà d'une limite de caractères, seul le début est lu (§5).
- Pour tous les projets, `~/.claude/rules/` existe aussi (§1) ; dans ce dossier, les motifs `paths` partent du dossier de lancement de la session (§4).
- Remplacer chaque [crochet] par une réponse validée ; supprimer toute section restée vide ; aucun crochet dans le fichier final (« à confirmer », ajouté à la liste remise à l'utilisateur).
- Signaler la règle dans la section « Procédures » du maître (avec plusieurs agents, dans le CLAUDE.md voisin d'AGENTS.md), par cette ligne : « Les règles propres à `[dossier]` se chargent seules quand un fichier de ce dossier est lu ou modifié (`.claude/rules/[sujet].md`). »
- Dans une règle, un commentaire HTML peut rester visible de Claude (§5) : retirer ce commentaire et les autres commentaires de consigne ; garder seulement le dernier.
-->

# Règles pour [fichiers visés]

[Une phrase : à quels fichiers ces règles s'appliquent, et pourquoi elles ne valent pas ailleurs.]

## Contenu et format

- [Règle concrète et vérifiable sur ces fichiers, suivie de sa raison si elle n'est pas évidente.]

## Sources propres

- [Référence à consulter pour ces fichiers] : `[chemin]`.

## Avant de modifier

- [Précaution propre à ces fichiers : copie préalable, accord, contrôle. Un interdit s'écrit en phrase négative complète : « Ne jamais … ».]

## Avant de dire « terminé »

- [Contrôle propre à ces fichiers : commande, comparaison à la source, relecture.]

<!-- Propriétaire : [nom ou rôle] · Revue : [fréquence] · Créé avec le kit Architecte consignes v1.1 -->
