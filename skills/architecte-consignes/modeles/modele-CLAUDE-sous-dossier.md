<!--
MODÈLE : CLAUDE.md d'un sous-dossier ou d'un sous-projet (kit Architecte consignes, v1.1).
Destination : `[sous-dossier]/CLAUDE.md`. À utiliser quand un sous-dossier a des règles propres, ou quand il peut être ouvert seul comme dossier de travail.
Pour Claude, au remplissage :
- Remplacer chaque [crochet] par une réponse validée. Supprimer toute section restée vide. Aucun crochet dans le fichier final : écrire « à confirmer » et l'ajouter à la liste remise à l'utilisateur.
- N'écrire que ce qui diffère du parent ou s'y ajoute. Ne jamais répéter une règle du maître, déjà chargée, ni celle d'un CLAUDE.md de dossier intermédiaire : un lieu par information.
- Ce fichier ne remplace rien : tout s'additionne, sans priorité (mecanismes.md §2). Une exception à une règle du parent s'écrit dans la règle du parent, avec sa portée ; écrite ici, elle créerait une contradiction. L'exception qu'une tâche programmée reçoit pour un accord d'ici (G4b) s'écrit dans la clause « Sessions sans surveillance » du maître, avec sa portée.
- Chargement : à la demande, dès que Claude lit, écrit ou modifie un fichier de ce sous-dossier, ou en lit un par une commande comme `cat` ou `head` ; une commande shell quelconque ne suffit pas (§1). Après une compaction, il revient seulement quand Claude retouche un fichier du sous-dossier (§7). Une règle utile avant d'y entrer (par exemple : ce qu'on y range) va donc dans le maître.
- Rester court et mettre l'essentiel en tête : au-delà d'une limite de caractères, seul le début d'un fichier chargé à la demande est lu (§5).
- Si la règle vise un type de fichier présent dans plusieurs dossiers plutôt qu'un dossier, préférer une règle par chemin (`modele-regle-chemin.md`).
- « Mon accord » désigne l'utilisateur de la session ; dans un espace partagé, nommer le rôle qui donne l'accord.
- Si ce sous-dossier peut être ouvert seul : Claude Code charge quand même les CLAUDE.md et CLAUDE.local.md des dossiers parents (§1). En revanche, hors dépôt git, la mémoire automatique est celle du sous-dossier, pas celle du parent (§8). Toute règle nécessaire ici s'écrit donc dans un CLAUDE.md, jamais dans la mémoire.
- Dans ce même cas, la session ne reçoit pas le `.claude/settings.json` du parent, lu depuis le dossier de travail (§6) : recommander de lancer Claude à la racine, ou répéter les deny nécessaires dans `.claude/settings.json` de ce sous-dossier en réécrivant chaque motif `./`, qui part du dossier de lancement (`Read(./clients/rh/**)` devient `Read(./rh/**)` dans `clients/`), ou en chemin absolu (`//c/…`). Tester ensuite chaque deny sur un fichier factice, dans une session ouverte ici (pour un outil bloqué, vérifier plutôt que Claude ne le voit plus, §6 ; serveur de `.mcp.json` pas encore approuvé : controle-qualite.md section 3) : en terminal, `/status` et `/permissions` montrent les réglages chargés, pas le chemin visé ; dans l'onglet Code, `/permissions` est indisponible. Le chargement des règles par chemin et des skills du parent n'est pas décrit dans mecanismes.md : non documenté, à vérifier dans l'application.
- Un autre agent ouvert dans ce sous-dossier suit ses propres règles de découverte des dossiers parents (§9). Si ce sous-dossier a aussi un AGENTS.md, Claude Code ne le lit pas dès qu'un CLAUDE.md, `.claude/CLAUDE.md` ou CLAUDE.local.md existe ici, dans le dossier de travail ou au-dessus (`~/.claude/CLAUDE.md` et le CLAUDE.md géré ne comptent pas), sauf réglage « Project instructions » sur `claude-md-and-agents-md` (§9) : commencer ce fichier par `@AGENTS.md` et n'y écrire que ce qui est propre à Claude.
- Les commentaires HTML de bloc sont retirés avant l'envoi à Claude : garder seulement le dernier commentaire du fichier.
-->

# [Nom du sous-dossier]

[Une phrase : ce qu'on fait ici et en quoi cela diffère du reste de l'espace.] Les règles générales viennent de `[chemin du maître]`, déjà chargé.

## En plus des règles générales

- [Règle propre à ce sous-dossier, concrète et vérifiable, avec sa raison si elle n'est pas évidente.]

## Sources propres à ce dossier

<!-- Ne lister que les sources absentes du maître. -->
| Pour | Source qui fait foi |
|---|---|
| [Information propre au sous-projet] | `[chemin]` |
| [État des tâches du sous-projet, s'il a son propre suivi] | `[chemin du suivi]` |

## Classement et nommage propres

- [Règle qui s'ajoute à celle du maître : par exemple, un préfixe ou un sous-dossier obligatoire ici.]

<!-- Chaque interdit est une phrase négative complète, juste même hors de ce titre ou traduite. Claude Code seulement : un interdit sans exception se double d'une règle deny dans le .claude/settings.json de la racine et, si ce sous-dossier peut être ouvert seul, dans le sien, motifs réécrits (ci-dessus). Ajouter alors à l'interdit la mention de controle-qualite.md C14 : « (bloqué par les réglages) », « (bloqué par les réglages dans ce dossier) » ou « demande confirmation ». -->
## Accord préalable et interdits propres

- Demander mon accord avant de [action engageante propre à ce dossier].
- Ne jamais [interdit propre à ce dossier].

## Procédures propres

- Pour [tâche propre à ce dossier], utiliser `/[nom-du-skill]`.
- Avant de [tâche ponctuelle], lire `[chemin de la procédure]`.

## Commandes et pièges propres

- [Commande propre à ce sous-projet, telle qu'elle se tape, ou comportement inattendu d'un fichier d'ici, et la bonne façon de faire.]

<!-- Section à garder seulement si ce sous-dossier peut être ouvert seul. -->
## Ouvert seul comme dossier de travail

- Les règles générales restent celles de `[chemin du maître]`, chargé avec ce fichier : ne pas les recopier ici.
- [Ce qui change quand on travaille ici seul : suivi à lire en premier, dossiers voisins à ne pas toucher.]

## Entretien de ce fichier

- Une règle qui finit par valoir pour tout l'espace remonte dans le maître et sort d'ici.

<!-- Propriétaire : [nom ou rôle] · Revue : [fréquence] · Créé avec le kit Architecte consignes v1.1 -->
