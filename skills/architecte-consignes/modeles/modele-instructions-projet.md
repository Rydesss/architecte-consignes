<!--
MODÈLE : instructions d'un projet Cowork ou d'un projet claude.ai (kit Architecte consignes, v1.1). Pour Claude, au remplissage :
- Même logique que le maître (`modele-CLAUDE-projet.md`), en plus compact : partie 1 sous 60 lignes (repère du kit, pas une limite documentée). Supprimer toute section restée vide ; aucun crochet restant (« à confirmer »).
- Pourquoi ce rendu : une session Cowork sur le bureau charge `~/.claude/CLAUDE.md` et `~/.claude/rules/` (imports hors du dossier de la session et liens symboliques exclus), mais sa lecture d'un CLAUDE.md de projet n'est pas documentée, et un projet claude.ai se règle par ses instructions et ses fichiers de connaissance (mecanismes.md §12). Projet Cowork : ne pas recopier ici les préférences de `~/.claude/CLAUDE.md` (doublon), sauf si ce fichier est un lien symbolique ; projet claude.ai : les reporter.
- Claude Code et Cowork sur le même dossier : le maître fait foi. La partie 1 reprend ses sections « Demander mon accord avant de » et « Interdits », les accords et les interdits de chaque règle par chemin et de chaque CLAUDE.md de sous-dossier (une section « Dossier » par dossier, ou « Fichiers » pour une règle qui vise un type de fichier), et la ligne « Avant toute tâche, lire `CLAUDE.md` » (lecture non garantie ; routage.md section 7). Les skills importés (partie 3) gardent leurs propres garde-fous. Dans ce texte, « (bloqué par les réglages) » ne suit que l'interdit restreint aux outils de connecteur réglés sur Blocked dans Cowork (controle-qualite.md C14) ; de même, « demande confirmation » ne suit qu'un outil de connecteur réglé sur Needs approval (contrôlé aussi par C14). Une mention du maître due à `.claude/settings.json` tombe à la copie (effet dans Cowork non documenté, §6). Un réglage encore à faire, par une autre personne par exemple, ne donne aucune mention : la ligne reste une consigne jusqu'au réglage.
- Cowork ne lit pas `~/.claude` pour les skills et plugins. Réglages appliqués par l'outil : la permission d'un outil de connecteur, Blocked, ou Needs approval pour un accord (§12) ; dans Cowork, un deny de l'outil `Bash` ou `WebFetch` entier (réglage géré par l'organisation, §6 ; depuis les réglages utilisateur ou projet : non documenté, à vérifier dans l'application). La ligne concernée prend alors « (bloqué par les réglages) » ou « demande confirmation ». Interdit d'envoi ou de sortie de texte : outil de connecteur sur Blocked ; `WebFetch` et `WebSearch` restent une consigne, hors deny géré ci-dessus ; « (bloqué par les réglages) » suit seulement l'interdit restreint aux outils bloqués. Tout autre interdit reste une consigne, en phrase négative complète.
- Les lignes préremplies sont des propositions (blocs C, F et G), jamais une règle contre une réponse ; les deux premières de « Demander mon accord avant de » sont la valeur par défaut de F1. Chaque accord est une phrase complète, juste hors de son titre. « Mon accord » désigne l'utilisateur de la session ; dans un projet partagé, écrire « avec l'équipe » et nommer le rôle qui donne l'accord.
- Les satellites deviennent des fichiers de connaissance (claude.ai) ou des fichiers du dossier du projet (Cowork), cités par leur nom. Avant d'écarter un fichier sensible, avoir demandé quelles tâches en dépendent et dit la conséquence ; un fichier nécessaire reste, avec ses garde-fous dans « Interdits ».
- « Classement et nommage » : pour Cowork, ou si Claude nomme des fichiers. « Dossier [chemin du dossier] » : une section par dossier qui a ses propres règles ; pour une règle par chemin qui vise un type de fichier, une section « Fichiers [motif] » (routage.md section 7). « Commandes et pièges » reçoit G1 à G3, et une tâche programmée (G4) en une ligne par tâche : ce qu'elle suit, ce qu'elle ne touche pas et, pour chaque accord qu'elle rencontre, l'exception choisie en G4b (`modele-CLAUDE-projet.md`) ; un arrêt avec un compte rendu s'écrit dans sa procédure (`modele-skill-procedure.md`), et le fichier de ce compte rendu dans cette ligne, qui permet de le créer sans accord. « Entretien de ces instructions » vient du bloc H ; propriétaire (H5) et revue (H4) vont dans la ligne « Rôle ».
- Rendre les trois parties dans la conversation, la partie 1 en bloc de code prêt à copier ; parties 2 et 3 à l'infinitif, quel que soit le registre. Retirer ce commentaire.
-->

# Instructions du projet : [nom du projet]

Rôle et moment de lecture : texte qui remplace celui des instructions du projet [Cowork ou claude.ai], sans s'y ajouter (partie 1), fichiers à joindre ou à placer (partie 2), skills à importer (partie 3). Propriétaire : [nom ou rôle] ; revue : [fréquence du bloc H].

## 1. Texte à coller à la place des instructions actuelles du projet

```text
[Nom du projet] : [une à trois phrases : ce qu'on y fait, pour qui, ce qu'on y produit].

## Avant d'agir
- L'état des travaux (tâches ouvertes, échéances, statuts) se lit dans [fichier de suivi].

## Où trouver quoi
- [Sujet] : [fichier joint ou dossier qui fait foi].
- [Sujet] : [fichier].

## Façon de travailler avec moi
- [Langue ; tutoiement ou vouvoiement ; forme et longueur des réponses.]

## Classement et nommage
- [Règle courte avec un exemple réel et la date qui fait foi (D2b), ou renvoi au fichier de conventions joint.]

## Documents destinés à des tiers
- [Ton, mentions obligatoires, formules interdites, ou renvoi au fichier joint qui les définit.]

## Demander mon accord avant de
- Demander mon accord avant d'envoyer, de publier ou de partager quoi que ce soit hors du projet.
- Demander mon accord avant de supprimer, de déplacer, de renommer ou d'écraser un fichier existant.
- [Autre action engageante, en phrase complète : « Demander mon accord avant de payer, de signer, de modifier un compte ou de toucher à la production. »]

## Interdits
- Ne jamais inventer une information absente des sources : écrire « à confirmer ».
- [Ne jamais … : interdit propre au projet.]

## Dossier [chemin du dossier]
- [Règle propre à ce dossier (règle par chemin ou CLAUDE.md de sous-dossier) : accord en phrase complète, interdit « Ne jamais … ».]

## Procédures
- Pour [tâche récurrente], utiliser le skill [nom-du-skill].
- Avant de [tâche ponctuelle], lire [fichier joint].

## Commandes et pièges
- [Outil, commande ou piège que Claude ne devinerait pas, et la bonne façon de faire.]

## Avant de dire « terminé »
- [Contrôle concret], et citer les fichiers utilisés.

## Entretien de ces instructions
- Une correction répétée deux fois devient une règle ici ; une règle devenue fausse est supprimée.
- Les dates et les statuts vont dans [fichier de suivi], jamais ici ; la prochaine revue y figure comme une tâche datée.
```

## 2. Fichiers à joindre ou à placer dans le projet

| Fichier | Contenu | Pourquoi |
|---|---|---|
| `[nom du fichier]` | [source de vérité, modèle, conventions] | [ce qu'il évite de redemander] |

- claude.ai : joindre ces fichiers comme fichiers de connaissance du projet. Cowork : les placer dans le dossier du projet.
- Ne joindre ni placer dans le projet aucun secret ; des données personnelles de tiers seulement si une tâche validée en a besoin. Une consigne « ne pas lire » n'est pas une garantie.

## 3. Skills à importer

- [nom-du-skill] : [tâche récurrente couverte].
- Importer chaque skill sur le compte claude.ai : zipper le dossier au nom du skill, SKILL.md dedans, puis l'importer depuis la page Plugins de la barre latérale (avant : Personnaliser > Skills > « Upload a skill » ; chemin exact à vérifier dans l'application, `mecanismes.md` §12). Activer d'abord « Code execution and file creation » (« Create and edit files »), dans Réglages > Capacités ; si le réglage ou le bouton manque (Team ou Enterprise), demander au propriétaire de l'organisation. Cowork charge les skills activés sur le compte claude.ai, synchronisés au début de chaque session : après l'import, ouvrir une nouvelle session Cowork.
- Frontmatter : seulement `name` et `description` (choix du kit). claude.ai refuse tout champ hors des six de la spécification, dont `disable-model-invocation`, propre à Claude Code : l'import échoue (mecanismes.md §11).
- [Team ou Enterprise : chaque membre peut importer ses propres skills, sauf si un propriétaire a désactivé la création de skills ; en Enterprise, un propriétaire doit activer « Code execution and file creation » et « Skills ». Les propriétaires peuvent aussi mettre un skill à la disposition de tous.]
