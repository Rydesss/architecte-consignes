<!--
MODÈLE : fichier satellite « procédure », lu à la demande (kit Architecte consignes, v1.1.2).
Pour Claude, au remplissage :
- Pour une tâche ponctuelle ou rare, ou quand l'utilisateur ne veut pas de skill ; une tâche récurrente validée au bloc E devient plutôt un skill (`modele-skill-procedure.md`).
- Remplir avec les réponses validées du bloc E (déroulé proposé par Claude et validé compris). Remplacer chaque [crochet] ; une valeur inconnue devient « à confirmer ». Supprimer toute section restée vide. Ne recopier aucune règle générale du maître ; un interdit est une phrase négative complète.
- Remplacer `consignes/` par le dossier validé à l'étape 3 ; supprimer tout renvoi vers un satellite non créé (sans `consignes/conventions.md`, le ton renvoie à son lieu unique, fixé par `routage.md` section 2).
- Entrée manquante : la ligne préremplie de « Entrées » applique la valeur par défaut de B4 ; l'adapter si B4 diffère, et retirer sa fin sans entrée indispensable. Le contrôle commun (E6) se cite par renvoi, ligne supprimée si le maître ne l'a pas.
- Exceptions : reprendre la ligne « Exceptions » de la fiche (E4b), un cas par ligne, vérifiable dans la source ; sans exception connue, garder seulement la dernière ligne, précédée de « Aucune exception connue. » (`modele-skill-procedure.md`).
- Tâche programmée qui suit cette procédure : pour chaque accord du maître qu'elle rencontre (D1 et F1 compris), et chaque accord des règles par chemin et des CLAUDE.md de sous-dossier des dossiers où elle écrit, écrire dans « Points d'accord » le choix de G4b, exception écrite au maître ou arrêt avec un compte rendu daté, dont le fichier est cité dans la clause « Sessions sans surveillance » du maître (`modele-skill-procedure.md`). Sans tâche programmée, supprimer la ligne « Session programmée » de « Points d'accord ». Un interdit ne reçoit jamais d'exception.
- Emplacement par défaut : `consignes/[nom-de-la-tache].md`, nom sans espace. Pointeur dans la section « Procédures » du maître : « Avant de [tâche], lire `consignes/[nom-de-la-tache].md` ». Seul déclencheur, sans lecture garantie (mecanismes.md §4) : le formuler sur une situation précise.
- Une seule version en vigueur ; une version remplacée part aux archives sous un nom daté, sans étape barrée ni « ancienne méthode » ici.
- Citer sources et conventions par leur chemin, sans les recopier. Ni date d'événement ni statut : ils vont dans le suivi.
- Erreurs fréquentes : seulement des erreurs constatées ou signalées ; une correction répétée deux fois y devient une ligne.
- Une étape qui ne doit jamais partir sans accord se double, dans Claude Code, d'une règle ask ou deny dans `.claude/settings.json` (`modele-settings.json`) ; dans Cowork ou claude.ai, d'un outil de connecteur réglé sur Needs approval ou Blocked, si l'étape passe par lui (mecanismes.md §12). Le point d'accord écrit ici reste une consigne.
- « Mon accord » désigne l'utilisateur de la session ; dans un espace partagé, nommer le rôle qui donne l'accord.
- Claude voit les commentaires de ce fichier quand il l'ouvre : retirer les commentaires de consigne, garder seulement le dernier.
-->

# Procédure : [nom de la tâche]

Rôle et moment de lecture : lu à la demande, en entier, avant de [tâche]. Seule cette version est en vigueur ; les anciennes sont dans `[archives]` et ne se suivent pas.

## Déclencheur

- [Situation ou demande qui lance la procédure, par exemple « quand je demande … » ou « à réception de … ».]

## Entrées

- [Ce qu'il faut avoir avant de commencer, et où le trouver : `[chemin]`.]
- Entrée manquante : l'écrire « à confirmer » et continuer ; seule [entrée indispensable] se demande avant de commencer.

## Exceptions

- Ne pas [faire la tâche, ou retenir un élément] si [condition vérifiable dans la source].
- [Cas limite] : [que faire].
- En cas de doute : s'arrêter et demander.

## Étapes

1. [Action concrète et vérifiable.]
2. [Action ; nommage et ton selon `consignes/conventions.md`.]
3. [Action.]

## Points d'accord

- Avant l'étape [n] : présenter [ce qui va partir ou changer : destinataire, contenu, fichiers touchés] et attendre mon accord explicite.
- Session programmée, à l'étape [n] : [faire sans accord ce que permet l'exception « Sessions sans surveillance » du maître ; ou s'arrêter et laisser dans `[emplacement]` un compte rendu daté (`compte-rendu-AAAA-MM-JJ.md`) : ce qui est fait, ce qui attend mon accord ; ce seul fichier, cité dans la clause « Sessions sans surveillance » du maître, se crée sans accord].

## Sortie

- [Ce qui est produit, où, sous quel nom.]
- [Ce qui est mis à jour : suivi, registre.]

## Critère de « terminé »

- La tâche est terminée quand [résultat vérifiable : fichier présent, chiffres égaux à la source, liens valides].
- Puis appliquer le contrôle commun de la section « Avant de dire “terminé” » du maître, sans le recopier ici.

## Erreurs fréquentes

- [Erreur déjà constatée] : [comment l'éviter].

<!-- Propriétaire : [nom ou rôle] · Créé avec le kit Architecte consignes v1.1.2 -->
