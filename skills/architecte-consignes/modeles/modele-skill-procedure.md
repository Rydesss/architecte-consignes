---
name: [nom-de-la-tache]
description: "[Utiliser quand l'utilisateur demande … ou quand … Produit … Ne pas utiliser pour …]"
# disable-model-invocation: true
---

<!--
MODÈLE : SKILL.md d'une tâche récurrente (kit Architecte consignes, v1.1.2).
Pour Claude, au remplissage :
- La ligne `---` reste la première du fichier, sinon le frontmatter n'est pas lu (mecanismes.md §11).
- Créer un skill seulement pour une tâche récurrente validée au bloc E (déroulé proposé par Claude et validé compris). Emplacement : `.claude/skills/<nom>/SKILL.md` (ce projet) ou `~/.claude/skills/<nom>/SKILL.md` (tous les projets).
- name : 1 à 64 caractères (minuscules, chiffres, tirets, sans tiret au début, à la fin ni doublé), identique au nom du dossier, sans les mots `claude` ni `anthropic` (refusés à l'import sur claude.ai, §11). L'appel se fait par `/<nom>`.
- description : cas d'usage en premier (« Utiliser quand … »), puis ce que le skill produit, puis quand ne pas l'utiliser ; 1 024 caractères au plus. Claude s'en sert pour décider d'appeler le skill.
- disable-model-invocation, propre à Claude Code : pour un skill utilisé dans Claude Code dont la tâche envoie, publie ou supprime, retirer le # (appel par `/<nom>` seulement) et le crochet « ou quand Claude la juge utile… » de la ligne de rôle. Dans tous les autres cas, et pour tout skill à importer sur claude.ai (Cowork compris), supprimer la ligne : l'import refuse tout champ hors des six de la spécification (erreur « Unexpected key(s) », §11). L'accord repose alors sur le rappel en tête des règles essentielles et sur « Demander mon accord avant de » des instructions du projet.
- Règles essentielles en tête : après une compaction, seul le début d'un skill appelé peut revenir (§7). N'y recopier aucune règle générale du maître : seulement les garde-fous propres à la tâche et, au plus, un rappel d'une ligne du garde-fou le plus critique, marqué « (rappel du maître) ». Chaque interdit est une phrase négative complète.
- Entrée manquante : la ligne préremplie de « Entrées » applique la valeur par défaut de B4 ; l'adapter si B4 diffère, et retirer sa fin sans entrée indispensable.
- Exceptions : reprendre la ligne « Exceptions » de la fiche (E4b), un cas par ligne, chacun vérifiable dans la source qui fait foi. Sans exception connue, garder seulement la dernière ligne de la section, précédée de « Aucune exception connue. » En session programmée, « s'arrêter » vaut pour ce cas seul : il est cité dans le compte rendu. Déclenchement qui dépend des données (liste à relancer, dossiers à traiter) : avant de rédiger, appliquer le critère à la source en lecture seule, s'il ne l'a pas été (sans accès aux fichiers : par l'utilisateur, SKILL.md, étape 5), et montrer le résultat sans donnée personnelle : nombre de cas retenus et écartés, chacun désigné par `fichier:ligne` dans la source, jamais par un nom de dossier qui contient un nom de personne (questionnaire.md, bloc E) ; un écart corrige la fiche, puis ce skill.
- Vérification : le contrôle propre à la tâche (E4) s'écrit ici ; le contrôle commun (E6) se cite par renvoi, ligne supprimée si le maître (ou les instructions du projet) ne l'a pas.
- Remplacer `consignes/` par le dossier validé à l'étape 3 ; supprimer tout renvoi vers un satellite non créé (sans `consignes/conventions.md`, le ton renvoie à son lieu unique, fixé par `routage.md` section 2). Citer les fichiers de référence par leur chemin, sans les recopier ; un fichier annexe se range dans le dossier du skill et se cite d'ici, sans cascade.
- Une action qui ne doit jamais partir sans accord se double, dans Claude Code, d'une règle ask ou deny dans `.claude/settings.json` (`modele-settings.json`) ; dans Cowork ou claude.ai, d'un outil de connecteur réglé sur Needs approval ou Blocked, si l'action passe par lui (mecanismes.md §12).
- Session programmée : le prompt de la tâche renvoie à ce skill sans le recopier. Lister les accords du maître que la tâche rencontre (« Demander mon accord avant de », valeurs par défaut de D1 et de F1 comprises), et ceux des règles par chemin et des CLAUDE.md de sous-dossier des dossiers où elle écrit. Pour chacun, écrire dans « Points d'accord » le choix de G4b : l'exception écrite au maître (« Sessions sans surveillance »), ou l'arrêt de la tâche à cette étape, avec un compte rendu daté (ce qui est fait, ce qui attend l'accord), dont le fichier est cité dans la même clause du maître. Sans tâche programmée, supprimer la ligne « Session programmée » de « Points d'accord ». Un interdit ne reçoit jamais d'exception. Un accord doublé d'une règle ask fait en plus attendre l'exécution dans sa session, exception écrite ou non (déduction, §6 et §14).
- « Mon accord » désigne l'utilisateur de la session ; dans un espace partagé, nommer le rôle qui donne l'accord.
- Moins de 500 lignes. Supprimer toute section restée vide ; aucun crochet restant (« à confirmer »).
- Un commentaire HTML peut rester visible de Claude dans un skill (§5) : retirer les commentaires de consigne, garder seulement le dernier.
-->

# [Nom lisible de la tâche]

Rôle et moment de lecture : procédure de [tâche], lue en entier à l'appel `/[nom-de-la-tache]` [ou quand Claude la juge utile d'après sa description].

## Règles essentielles

1. [Au plus un rappel, par exemple : Ne rien envoyer ni publier sans mon accord explicite (rappel du maître).]
2. [Garde-fou propre à la tâche, par exemple : Ne jamais modifier le fichier source, seulement sa copie.]
3. [Autre règle propre à la tâche.]

## Entrées

- [Ce que l'utilisateur fournit ou désigne en lançant le skill.]
- Sources : `consignes/sources.md` ; [fichier propre à la tâche] : `[chemin]`.
- Entrée manquante : l'écrire « à confirmer » et continuer ; seule [entrée indispensable] se demande avant de commencer.

## Exceptions

- Ne pas [faire la tâche, ou retenir un élément] si [condition vérifiable dans la source, par exemple : échéance pas encore atteinte].
- [Cas limite, par exemple une donnée absente de la source] : [que faire].
- En cas de doute : s'arrêter et demander.

## Étapes

1. [Action concrète et vérifiable.]
2. [Action ; nommage et ton selon `consignes/conventions.md`.]
3. [Action.]

## Points d'accord

- Avant l'étape [n] : présenter [destinataire, contenu, fichiers touchés] et attendre mon accord explicite.
- Session programmée, à l'étape [n] : [faire sans accord ce que permet l'exception « Sessions sans surveillance » du maître ; ou s'arrêter et laisser dans `[emplacement]` un compte rendu daté (`compte-rendu-AAAA-MM-JJ.md`) : ce qui est fait, ce qui attend mon accord ; ce seul fichier, cité dans la clause « Sessions sans surveillance » du maître, se crée sans accord].

## Sortie

- [Fichier ou message produit : emplacement, nom, langue.]
- [Mise à jour de `[chemin du suivi]`, si la tâche y figure.]

## Vérification

- Avant de dire « terminé » : [contrôle propre à cette tâche, par exemple comparer les chiffres à la source].
- Puis le contrôle commun de « Avant de dire “terminé” » [du maître ou des instructions du projet].

## Ce que ce skill ne fait pas

- [Tâche voisine hors périmètre] : [ce qu'il faut faire à la place].

<!-- Propriétaire : [nom ou rôle] · Créé avec le kit Architecte consignes v1.1.2 -->
