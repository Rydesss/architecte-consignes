<!--
MODÈLE : fichier de suivi (kit Architecte consignes, v1.1.2).
Pour Claude, au remplissage :
- Ce fichier est l'état, pas une consigne : tâches ouvertes, prochaines actions, échéances. Une règle repérée va dans le maître ou un satellite ; l'état ne va pas dans la mémoire automatique.
- Emplacement et nom : ceux validés au plan (étape 3). Le maître y pointe depuis « Avant d'agir » sans rien en recopier. Ne jamais l'importer avec @ : il serait chargé à chaque session.
- Aucune consigne ne déclenche une action à une date : la prochaine revue des consignes (fréquence du bloc H) est une ligne datée du tableau. Seuil d'archivage : 100 lignes ou 15 Ko par défaut, ajustable au bloc H ; annoncer la valeur retenue.
- Les règles de tenue s'écrivent seulement ici ; le maître ne les recopie pas.
- Une ligne par tâche ouverte ; « Prochaine action » sans historique. Ajouter une colonne « Qui » si l'espace est partagé.
- Pas de date « dernière mise à jour » tenue à la main. Une date ne s'estime jamais : elle vient d'un document, de l'utilisateur ou d'une commande qui l'affiche ; en cas de doute, la demander.
- Qui met ce fichier à jour (H2) : la première ligne de « Tenue de ce fichier », réduite à l'option retenue (par défaut, la première ; projet claude.ai : la troisième, questionnaire.md bloc H).
- Historique (H3). Par défaut (non) : garder la ligne « … aucun historique n'est tenu », supprimer les passages « si H3 = oui ». Avec un journal : l'inverse ; une ligne par tâche faite (date, tâche, résultat, lien).
- Retirer ce commentaire ; garder seulement le dernier.
-->

# Suivi : [nom de l'espace de travail]

Rôle et moment de lecture : état des tâches ouvertes, lu au début de chaque tâche sur le pointeur de la section « Avant d'agir » du CLAUDE.md maître ; mis à jour selon « Tenue de ce fichier ». Il fait foi pour l'état et ne contient aucune règle de travail.

## Tâches ouvertes

| Tâche | Prochaine action | Échéance | Lien |
|---|---|---|---|
| [Tâche, en quelques mots] | [Une action concrète] | [date, ou « aucune »] | `[dossier ou document]` |
| [Tâche] | [Attendre la réponse de [rôle], puis …] | [date] | `[chemin]` |
| Revue des consignes | Relire les consignes en mode audit et retirer ce qui est devenu faux | [date de la prochaine revue] | `[chemin du maître]` |

## Tenue de ce fichier

- [Selon H2 : « Claude met ce fichier à jour à la fin de chaque tâche qui change un état. », « Claude le met à jour sur demande. » ou « Je le modifie seul : Claude propose la ligne sans l'écrire. »]
- Une tâche terminée sort aussitôt du tableau ; aucun historique n'est tenu.
- [Si H3 = oui : une tâche terminée sort aussitôt du tableau, avec une ligne datée dans `[journal d'archives]`, lu seulement pour une question sur le passé.]
- La revue des consignes faite, sa ligne est remplacée par la suivante, datée selon [fréquence du bloc H].
- À chaque revue : retirer les tâches abandonnées [vers le journal, si H3 = oui], raccourcir les cellules trop longues, vérifier les liens.
- Au-delà de [100] lignes ou [15] Ko, faire la revue sans attendre.

<!-- Propriétaire : [nom ou rôle] · Créé avec le kit Architecte consignes v1.1.2 -->
