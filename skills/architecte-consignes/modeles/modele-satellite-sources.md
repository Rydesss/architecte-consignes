<!--
MODÈLE : fichier satellite « sources de vérité » (kit Architecte consignes, v1.1).
Pour Claude, au remplissage :
- Remplir avec les réponses validées du bloc C et les sources repérées à l'étape 1. Remplacer chaque [crochet] ; une valeur inconnue devient « à confirmer ». Supprimer toute section restée vide.
- Emplacement par défaut : `consignes/sources.md`, dans le dossier de consignes validé à l'étape 3. Mode par défaut : à la demande, avec dans le maître le pointeur « Avant de citer un chiffre, une date, un nom ou une référence, lire `consignes/sources.md` ». L'importer seulement s'il est court et utile à chaque session.
- Le tableau « Où trouver quoi » du CLAUDE.md maître garde les sources les plus consultées ; ici vivent la liste complète, la hiérarchie et la règle en cas de conflit (C2), que le maître ne reprend pas. Une règle sur une source n'est écrite qu'à un seul de ces deux endroits.
- Décrire des catégories et des emplacements, jamais une valeur confidentielle. Si un secret a été cité pendant l'entretien, ne pas l'écrire : indiquer où le ranger hors des consignes. Un fichier de secrets trouvé dans l'espace est un constat bloquant (une gravité, pas un arrêt) : sans l'ouvrir, proposer à l'utilisateur de l'en sortir lui-même ; s'il le garde, deny de lecture nommé (C4) et statut « risque accepté » (controle-qualite.md C21).
- Les données à ne jamais inventer (C3) et les fichiers à ne jamais ouvrir (C4) ont pour seul lieu la section « Interdits » du maître, avec le réglage deny et sa mention (questionnaire.md) : ici, un renvoi seulement. Un autre interdit écrit ici est une phrase négative complète, juste même hors de son titre ou traduite, et une consigne sans garantie.
- Avec plusieurs agents, les renvois au CLAUDE.md maître visent `AGENTS.md`, sous les mêmes titres de section.
- La hiérarchie ci-dessous porte sur les données. Entre fichiers de consignes, il n'y a aucune priorité : tout s'additionne (§2).
- Lu à la demande, ce fichier est ouvert par Claude, qui voit alors ses commentaires : retirer ce commentaire et les autres commentaires de consigne ; garder seulement le dernier.
-->

# Sources de vérité : [nom de l'espace de travail]

Rôle et moment de lecture : lu à la demande, avant de citer ou de reprendre une information officielle, chiffrée ou datée, et en cas de doute entre deux sources.

## Qui fait foi, sur quel sujet

| Sujet | Fichier qui fait foi | Tenu à jour par |
|---|---|---|
| [Identité, coordonnées officielles] | `[chemin]` | [rôle, ou « figé »] |
| [Chiffres, tarifs, référentiel] | `[chemin]` | [rôle] |
| [Modèles de documents] | `[chemin]` | [rôle] |
| [État des tâches et échéances] | `[chemin du suivi]` | [rôle, ou « Claude »] |

- Un document dérivé (export, copie, brouillon) ne fait pas foi : remonter au fichier du tableau.
- Modifier un fichier qui fait foi seulement s'il est tenu à jour par Claude dans ce tableau ; sinon, proposer la correction.

## En cas de conflit entre deux sources

1. [Source la plus fiable, par exemple document signé ou officiel.]
2. [Ensuite, par exemple registre tenu à jour.]
3. [En dernier, par exemple notes et échanges.]

- Signaler tout écart : les deux valeurs, leurs fichiers, la source retenue selon cet ordre.
- Une information donnée dans la conversation ne remplace pas une source : proposer de mettre à jour le fichier qui fait foi.

## Données confidentielles

- [Catégorie, par exemple données personnelles de tiers] : dans `[emplacement hors des consignes]`, lu seulement pour [tâche qui en a besoin].
- Fichiers à ne jamais ouvrir et données à ne jamais inventer : section « Interdits » du CLAUDE.md maître.
- Ne jamais recopier une donnée confidentielle dans une consigne, dans le suivi ni dans un document qui n'en a pas besoin.

## Observé, déclaré, supposé

- Observé : lu pendant la session dans un fichier ou une sortie d'outil ; citer le fichier.
- Déclaré : dit par l'utilisateur ou par un tiers, sans source vérifiée ; dire qui l'a dit.
- Supposé : déduit ; le présenter comme une hypothèse.
- Dans une réponse, marquer ce qui n'est pas observé. Dans un document pour un tiers, n'écrire comme un fait que l'observé, ou le déclaré confirmé par l'utilisateur.

<!-- Propriétaire : [nom ou rôle] · Créé avec le kit Architecte consignes v1.1 -->
