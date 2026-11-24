<!--
MODÈLE : CLAUDE.md utilisateur, préférences valables dans tous les projets ; variante `CLAUDE.local.md`, préférences pour un seul projet (kit Architecte consignes, v1.1).
Destination : `~/.claude/CLAUDE.md` (sous Windows : `C:\Users\<nom>\.claude\CLAUDE.md`). À utiliser en mode « préférences personnelles », ou quand une réponse des blocs B, F ou G vaut pour tous les projets. Variante : `CLAUDE.local.md` à la racine du projet (point « Variante » ci-dessous).
Pour Claude, au remplissage :
- Remplacer chaque [crochet] par une réponse validée pendant l'entretien. Supprimer toute section restée vide.
- Ne laisser aucun crochet dans le fichier final : écrire « à confirmer » et l'ajouter à la liste remise à l'utilisateur.
- Moins de 50 lignes une fois rempli. Blocs B, F et G seulement, limités à ce qui vaut dans tous les projets : aucun nom de projet, de client, de dossier ni de source propre à un projet.
- Ce fichier est chargé au lancement de chaque session (mecanismes.md §1) et s'additionne aux CLAUDE.md des projets, sans priorité (§2). Ne rien y écrire qu'un projet devrait contredire : une préférence qui admet des exceptions va dans les projets concernés, ou s'écrit ici une seule fois avec sa portée et ses exceptions.
- Avant d'écrire, lire le `~/.claude/CLAUDE.md` existant s'il y en a un : fusionner sans rien écraser sans accord ; avec l'accord, garder d'abord une copie `CLAUDE.ancien-AAAA-MM-JJ.md`, sans aucun secret, à l'emplacement validé au plan. Signaler toute contradiction avec le maître en cours de rédaction.
- Le brouillon d'entretien reste dans le dossier de la session, jamais dans `~/.claude`.
- Écrire les préférences directement ici, sans import @ : un fichier de moins de 50 lignes n'en a pas besoin, et dans les sessions Cowork sur le bureau, un import qui sort du dossier de la session est sauté (§3).
- Cowork ne lit pas `~/.claude` pour les skills et plugins, mais une session Cowork sur le bureau charge ce fichier, sauf ses imports qui sortent du dossier de la session, et ne le charge pas s'il est lui-même un lien symbolique (§12). Ne pas recopier ces préférences dans les instructions d'un projet Cowork (doublon), sauf dans ce dernier cas ; pour un projet claude.ai, les y reporter.
- Variante `CLAUDE.local.md`, pour une préférence propre à un seul projet : chargé au lancement juste après le CLAUDE.md du même dossier, pour l'utilisateur seul (§1) ; noms propres au projet admis. Titre « Préférences personnelles pour ce projet » ; phrase de rôle « Préférences chargées au lancement de chaque session dans ce projet, pour moi seul ; les consignes du projet s'y ajoutent. » ; « Commandes et pièges de cette machine » limité à ce projet ; « Entretien de ce fichier » réduit à la seule ligne : « Une préférence qui vaut pour tous mes projets passe dans `~/.claude/CLAUDE.md`. » Lire le `CLAUDE.local.md` existant au lieu de `~/.claude/CLAUDE.md` ; sa copie se nomme `CLAUDE.local.ancien-AAAA-MM-JJ.md`. Réglages dans `.claude/settings.local.json`. En dossier versionné ou appelé à l'être, ligne `CLAUDE.local.*` dans `.gitignore`. Si ce projet n'a qu'un `AGENTS.md`, sans CLAUDE.md qui l'importe, éviter `CLAUDE.local.md`, qui en arrêterait la lecture, ou régler « Project instructions » sur `claude-md-and-agents-md` (§9).
- Ce que Claude apprend au fil des sessions relève de la mémoire automatique, pas de ce fichier.
- Claude Code seulement : les interdits sans aucune exception vont aussi dans `~/.claude/settings.json` (deny), qui vaut pour tous les projets ; y écrire les motifs de chemin en `//` ou `~/` (§6). Le deny d'un outil d'envoi (par exemple `WebFetch`, `WebSearch`, `Artifact`, `mcp__…`) retire donc l'outil dans tous les projets : le dire avant de le proposer. Un deny l'emporte sur tout allow (exception des mods, §6). Ses allow valent aussi pour les tâches programmées locales (§14) : n'y ajouter aucune autorisation large.
- Ne jamais écrire de secret ici : mot de passe, clé, identifiant bancaire ou fiscal.
- Aucune consigne ne déclenche une action à une date : la fréquence de revue du commentaire final ne déclenche rien. Une revue voulue se note comme une tâche datée là où l'utilisateur suit ses tâches. Le mode « préférences personnelles » ne pose pas le bloc H : sans fréquence donnée par l'utilisateur, retirer « Revue » du commentaire final.
- Les commentaires HTML de bloc, comme celui-ci, sont retirés avant l'envoi à Claude : garder seulement le dernier commentaire du fichier.
-->

# Préférences valables dans tous les projets

Préférences chargées au lancement de chaque session, dans tous les projets ; les consignes de chaque projet s'y ajoutent.

## Communication

- Répondre en [langue] ; [tutoiement ou vouvoiement].
- [Longueur et forme des réponses : par exemple, la réponse courte d'abord, le détail sur demande.]
- [Mise en forme : listes ou paragraphes, tableaux, titres.]

## Façon de travailler

- [Habitude générale : par exemple, annoncer le plan avant une tâche de plus de trois étapes.]
- [Quand poser une question plutôt que supposer.]
- [Preuve attendue avant « terminé » : par exemple, citer les fichiers lus et les commandes lancées.]

## Demander mon accord avant de

- [Action engageante, quel que soit le projet, en phrase complète : « Demander mon accord avant d'envoyer, de publier, de supprimer ou de payer quoi que ce soit. »]

## Interdits

- [Ne jamais … : interdit personnel valable dans tous les projets, en phrase négative complète. S'il figure aussi dans `~/.claude/settings.json`, ajouter la mention de `controle-qualite.md` C14 : « (bloqué par les réglages) » si le motif couvre tout l'objet, sinon « demande confirmation » si une règle ask couvre la forme restante. Interdit d'envoi : la mention suit seulement l'interdit restreint aux outils bloqués, une commande réseau lancée par Bash ou PowerShell leur échappant (mecanismes.md §6, en partie par déduction) ; le reste s'écrit à part, en consigne seulement ; deny refusé : aucune mention « bloqué ».]

<!-- Noter seulement ce que Claude ne détecterait pas seul. Aucun chemin propre à un projet. -->
## Commandes et pièges de cette machine

- [Commande ou syntaxe qui réserve un piège sur ce système ou ce terminal, et la bonne façon de faire.]
- [Outil installé, ou absent, qui change la façon de faire.]

## Entretien de ce fichier

- Une préférence répétée dans deux projets différents devient une ligne ici ; une ligne qui ne vaut que pour un projet en sort.
- Une ligne qu'un projet contredit est reformulée avec sa portée, ou déplacée dans les projets concernés.

<!-- Propriétaire : [nom ou rôle] · Revue : [fréquence] · Créé avec le kit Architecte consignes v1.1 -->
