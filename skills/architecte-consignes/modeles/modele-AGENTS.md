<!--
MODÈLE : AGENTS.md, source commune des consignes de plusieurs agents (kit Architecte consignes, v1.1).
Destination : `AGENTS.md` à la racine, à côté du CLAUDE.md qui l'importe (`modele-CLAUDE-avec-AGENTS.md`), quand plusieurs agents (Claude, Codex, Cursor, etc.) travaillent dans l'espace.
Pour Claude, au remplissage :
- Remplacer chaque [crochet] par une réponse validée ; supprimer toute section restée vide ; aucun crochet dans le fichier final (« à confirmer », ajouté à la liste remise à l'utilisateur).
- Les lignes préremplies sont des propositions : ne garder que celles qui répondent aux blocs C, F et G, jamais une règle contre une réponse. La valeur par défaut de C3, C4, F1 et F2 s'écrit, même dans un fichier d'équipe (questionnaire.md, conduite de l'entretien).
- Source unique des règles valables pour tous les agents : il reçoit ce qui irait dans le maître, sans seconde copie tenue à la main.
- Rester neutre vis-à-vis de l'outil : ni skill, ni commande `/…`, ni dossier `.claude/`, ni réglage, ni nom de modèle ; cela va dans le CLAUDE.md voisin, qui dit aussi ce que bloquent les réglages et ce qui leur échappe (risque accepté de controle-qualite.md C16). Ce qui ne vaut que pour un autre agent va dans son fichier.
- Pas d'import @ ici, sa lecture par les autres agents n'étant pas vérifiée : citer les fichiers entre accents graves, avec un déclencheur (« Avant de [tâche], lire `chemin` »). Remplacer `consignes/` par le dossier de consignes validé à l'étape 3.
- Chargé à chaque session de Claude par l'import : même discipline que le maître (règles stables et pointeurs, moins de 100 lignes visées, 200 au maximum, ni état, ni historique, ni secret).
- « Mon accord » et « avec moi » désignent l'utilisateur de la session ; dans un espace partagé, écrire « avec l'équipe » et nommer le rôle qui donne l'accord.
- Un AGENTS.md existant n'est écrasé qu'avec accord, après un commit ou une copie `AGENTS.ancien-AAAA-MM-JJ.md` sans aucun secret, rangée hors de l'espace de travail, à l'emplacement validé au plan : un autre agent pourrait lire une copie laissée dans l'espace (ses règles de découverte ne sont pas dans mecanismes.md, §9). Prévenir que le modifier change les consignes de tous les agents.
- Découverte et limites de taille des autres agents : voir leur documentation (mecanismes.md §9). Le retrait des commentaires HTML n'est documenté que pour les CLAUDE.md (§5), pas pour AGENTS.md, même importé, ni pour les autres agents : garder seulement le dernier commentaire, sans consigne dedans.
-->

# [Nom de l'espace de travail]

[Une à trois phrases : ce qu'est cet espace, qui l'utilise, ce qu'on y produit et pour qui.]

## Avant d'agir

- L'état des travaux (tâches ouvertes, échéances, statuts) se lit dans `[chemin du suivi]`.
- Avant toute tâche, lire `consignes/contexte.md`. <!-- Seulement si ce satellite existe ; Claude le reçoit déjà par l'import du CLAUDE.md voisin. -->
- [Vérification valable pour toutes les tâches, quel que soit l'agent.]

## Où trouver quoi

| Pour | Source qui fait foi |
|---|---|
| [Information de référence] | `[chemin]` |
| [Modèles de documents] | `[chemin]` |
| [État des tâches et échéances] | `[chemin du suivi]` |

- Avant de citer un chiffre, une date, un nom ou une référence, lire `consignes/sources.md`. <!-- Seulement si ce satellite existe. -->

## Façon de travailler avec moi

- [Langue ; tutoiement ou vouvoiement ; longueur et forme des réponses.]
- [Consigne concrète et vérifiable, suivie de sa raison si elle n'est pas évidente.]

## Classement et nommage

- Un nouveau document va dans [emplacement], sauf [exception].
- Nommage : [règle], par exemple `[exemple réel]` ; date qui fait foi : [création, envoi ou réception (D2b)].

<!-- Section à garder seulement si des documents partent vers des tiers. Si consignes/conventions.md existe, la réduire à un renvoi. -->
## Documents destinés à des tiers

- Ton : [registre, tutoiement ou vouvoiement]. [Mentions obligatoires ; contenus interdits.]

<!-- Section à garder seulement si l'utilisateur a décrit pendant l'entretien un partage du travail entre agents ; sinon la supprimer, sans poser de question pour elle. -->
## Travail entre agents

- [Qui fait quoi ; comment un agent signale un travail en cours ; quel fichier fait foi en cas de doute.]

<!-- Les deux premières lignes sont la valeur par défaut de F1 : les garder, les ajuster ou les retirer selon la réponse. Chaque accord : une phrase complète, juste hors de ce titre et une fois traduite. Dans un dossier de code, écrire la deuxième ligne ainsi : « Demander mon accord avant de supprimer, de déplacer ou de renommer un fichier existant, ou d'en remplacer tout le contenu ; modifier le code pour la tâche demandée n'en demande pas. » -->
## Demander mon accord avant de

- Demander mon accord avant d'envoyer, de publier ou de partager quoi que ce soit hors de cet espace.
- Demander mon accord avant de supprimer, de déplacer, de renommer ou d'écraser un fichier existant.
- [Autre action engageante, en phrase complète : « Demander mon accord avant de payer, de signer, de modifier un compte ou de toucher à la production. »]

<!-- Chaque interdit : une phrase négative complète, juste hors de ce titre et une fois traduite (« Never push to `main`. »). « Bloqué par les réglages » se dit dans le CLAUDE.md voisin. Action retenue aussi en accord (F1), la suppression ou l'envoi par exemple : comme dans `modele-CLAUDE-projet.md` (Interdits), sans interdit qui contredise la ligne d'accord. -->
## Interdits

- Ne jamais inventer une information absente des sources ci-dessus : écrire « à confirmer ».
- [Ne jamais … : interdit propre à cet espace.]

## Procédures

- Avant de [tâche récurrente ou ponctuelle], lire `[chemin de la procédure]`.

<!-- Commandes d'un dossier de code, et pièges communs à tous les agents. Section à supprimer si vide. Les commandes retenues en G2 s'écrivent ici sans citer aussi leur fichier source (`package.json`) dans « Où trouver quoi » (controle-qualite.md C10). -->
## Commandes et pièges

- [Commande à connaître, telle qu'elle se tape : construire, tester, lancer.]
- [Piège commun à tous les agents : fichier trompeur, doublon, et la bonne façon de faire.]

## Avant de dire « terminé »

- [Contrôle concret : commande de test et sa sortie, comparaison à la source, fichiers cités.]

## Entretien de ce fichier

- Une règle valable pour tous les agents s'écrit ici, une seule fois ; une règle propre à un agent va dans son fichier.
- Les dates d'événements et les statuts vont dans `[chemin du suivi]`, jamais ici. La prochaine revue de ces consignes y figure comme une tâche datée.

<!-- Propriétaire : [nom ou rôle] · Agents concernés : [liste] · Revue : [fréquence] · Créé avec le kit Architecte consignes v1.1 -->
