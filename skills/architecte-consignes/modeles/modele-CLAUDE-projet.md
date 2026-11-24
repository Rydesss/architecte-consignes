<!--
MODÈLE : CLAUDE.md maître (kit Architecte consignes, v1.1). Destination : CLAUDE.md à la racine de l'espace.
Pour Claude, au remplissage :
- Remplacer chaque [crochet] par une réponse validée ; supprimer toute section restée vide ; aucun crochet dans le fichier final (écrire « à confirmer » et le signaler).
- Viser moins de 100 lignes, 200 au maximum. Règles stables seulement : ni état, ni historique, ni secret, ni description complète de l'arborescence.
- Un chemin entre accents graves est un pointeur à la demande ; tout `@chemin` hors accents graves, même en milieu de phrase, est un import, chargé à chaque session (mecanismes.md §3). Importer le contexte seulement s'il dépasse une quinzaine de lignes ; sinon l'écrire sous le titre. Remplacer `consignes/` par le dossier de consignes validé à l'étape 3, en chemin relatif à ce fichier (`@00-gestion/consignes/contexte.md`).
- Chaque règle n'a qu'un lieu : si un satellite la porte, la section du maître se réduit à un renvoi.
- « Mon accord » désigne l'utilisateur de la session. Dans un espace partagé, écrire « avec l'équipe » et nommer le rôle qui donne l'accord quand ce n'est pas lui (« l'accord de la gérante »). Une session programmée n'a pas d'utilisateur présent : les accords qu'elle rencontre suivent « Sessions sans surveillance » et sa procédure.
- Supprimer tous les commentaires de consigne ; garder seulement le dernier commentaire du fichier.
-->

# [Nom de l'espace de travail]

[Une à trois phrases : ce qu'est cet espace, qui l'utilise, ce qu'on y produit et pour qui.]

@consignes/contexte.md

## Avant d'agir

- L'état des travaux (tâches ouvertes, échéances, statuts) se lit dans `[chemin du suivi]`.
- [Vérification à faire au début de chaque tâche, seulement si elle vaut pour toutes.]

## Où trouver quoi

| Pour | Source qui fait foi |
|---|---|
| [Identité et coordonnées officielles] | `[chemin]` |
| [Chiffres, tarifs, référentiel] | `[chemin]` |
| [Modèles de documents] | `[chemin]` |
| [État des tâches et échéances] | `[chemin du suivi]` |

- Avant de citer un chiffre, une date, un nom ou une référence, lire `consignes/sources.md`. <!-- Seulement si ce satellite existe. -->

## Façon de travailler avec moi

- [Langue ; tutoiement ou vouvoiement ; longueur et forme des réponses.]
- [Consigne concrète et vérifiable, suivie de sa raison si elle n'est pas évidente.]

## Classement et nommage

- Un nouveau document va dans [emplacement], sauf [exception].
- Nommage : [règle], par exemple `[exemple réel]` ; date qui fait foi : [création, envoi ou réception (D2b)].

<!-- Section à garder seulement si des documents partent vers des tiers. Si une règle sans paths existante porte déjà le ton (refonte), supprimer la section : la règle se charge à chaque session. Si consignes/conventions.md le porte, réduire la section au pointeur « Avant de rédiger un document pour un tiers, lire `consignes/conventions.md` » (routage.md section 2). -->
## Documents destinés à des tiers

- Ton : [registre, tutoiement ou vouvoiement]. [Mentions obligatoires ; contenus interdits.]

<!-- Les deux premières lignes sont la valeur par défaut de la question F1 : les garder, les ajuster ou les retirer selon la réponse. Chaque accord est une phrase complète, juste même hors de ce titre ou traduite. Dans un dossier de code, écrire la deuxième ligne ainsi : « Demander mon accord avant de supprimer, de déplacer ou de renommer un fichier existant, ou d'en remplacer tout le contenu ; modifier le code pour la tâche demandée n'en demande pas. » -->
## Demander mon accord avant de

- Demander mon accord avant d'envoyer, de publier ou de partager quoi que ce soit hors de cet espace.
- Demander mon accord avant de supprimer, de déplacer, de renommer ou d'écraser un fichier existant.
- [Autre action engageante, en phrase complète : « Demander mon accord avant de payer, de signer, de modifier un compte ou de toucher à la production. »]

<!-- Chaque interdit est une phrase négative complète, juste même hors de ce titre ou traduite. Action retenue à la fois en accord (F1) et en interdit (F2), la suppression par exemple (pour l'envoi, voir ci-dessous) : aucune ligne ici ; la ligne d'accord et sa règle ask suffisent, sans deny (questionnaire.md, bloc F). Interdit d'envoi ou de sortie de texte : « (bloqué par les réglages) » suit seulement l'interdit restreint aux outils bloqués (« Ne jamais envoyer ni publier de texte par [les seuls outils bloqués, en mots : un connecteur, une recherche web, une récupération web, une page publiée sur claude.ai]. ») ; une commande réseau lancée par Bash ou PowerShell (`curl`, `Invoke-WebRequest`) échappe à ces deny (mecanismes.md §6 ; documenté pour `WebFetch` face à Bash, déduit pour le reste) : le reste de l'interdit s'écrit à part, en consigne seulement, sauf envoi aussi en accord (F1) : ce reste suit alors la ligne d'accord, avec une règle ask sur les commandes réseau si l'utilisateur l'accepte au plan, sans « Ne jamais lancer de commande qui envoie des données sur le réseau. » (questionnaire.md, bloc F) ; deny refusé : aucune mention « bloqué ». Les outils de l'application qui transmettent aux sessions ou aux appareils de l'utilisateur (relevé de l'étape 1) ne sont pas bloqués par défaut : tant qu'ils restent permis, écrire « les outils d'envoi vers l'extérieur », jamais « tous les outils d'envoi » ni « rien ne sort », et ne pas désigner les outils bloqués par une destination que ces outils atteignent aussi (« vers le cloud »). Mention d'un réglage sur une commande (`rm`, `curl`, `git push`), dans cette section ou la précédente : une règle `Bash(…)` ou `PowerShell(…)` ne vise pas un autre outil qui lance des commandes, comme `mcp__terminal__run_in_terminal` de l'application de bureau (déduction ; effet d'une règle sur son nom à vérifier dans l'application, mecanismes.md §6). Si un tel outil figure au relevé de l'étape 1 : deny sur son nom, mention inchangée ; ask sur son nom, « demande d'autorisation » pour une commande en ask, et « (bloqué par les réglages dans les outils Bash et PowerShell ; demande d'autorisation dans le terminal de l'application) » pour une commande en deny (SKILL.md, étape 5) ; aucune règle, ajouter « dans les outils Bash et PowerShell » à la mention. Push sur `main` (routage.md section 5) : option Oui, « demande d'autorisation », jamais « (bloqué par les réglages) » ; option Non, « (bloqué par les réglages) », ses limites étant dites une fois à l'utilisateur. -->
## Interdits

- Ne jamais inventer une information absente des sources ci-dessus : écrire « à confirmer ».
- [Ne jamais … : interdit propre à cet espace. S'il figure aussi dans .claude/settings.json, ajouter la mention de controle-qualite.md C14, en mots simples : « (bloqué par les réglages) » si le motif couvre tout l'objet, « (bloqué par les réglages dans ce dossier) » s'il vise aussi des fichiers hors du dossier de lancement, ou « demande d'autorisation » si une règle ask couvre la forme restante ; pour un interdit de contenu de F3 couvert par un ask `Edit(...)`, « demande d'autorisation, restreinte aux outils d'édition » ; pour une commande, la restreindre selon le commentaire ci-dessus.]

## Procédures

- Pour [tâche récurrente], utiliser `/[nom-du-skill]`.
- Avant de [tâche ponctuelle], lire `consignes/[fichier].md`.
- Les règles propres à `[dossier]` se chargent seules quand un fichier de ce dossier est lu ou modifié (`.claude/rules/[sujet].md`).

## Commandes et pièges

- [Commande à connaître, telle qu'elle se tape : construire, tester, lancer.]
- [Comportement inattendu d'un outil ou d'un fichier, et la bonne façon de faire.]
- [Si une commande qui exécute du code du dépôt est gardée en allow, statut « risque accepté » (controle-qualite.md C16 ; déduction de mecanismes.md §6) : « Un script du dépôt modifié puis lancé par `[commande]` échappe aux deny de lecture et aux règles Bash (risque accepté). » Cette ligne garde la section, même en version minimale.]

## Avant de dire « terminé »

- [Contrôle concret : comparer les chiffres à la source, vérifier les liens, citer les fichiers utilisés.]

<!-- Section à garder seulement s'il existe des tâches programmées ou des automatisations. Une tâche programmée créée sans l'option « Only on this computer » n'est pas locale et ne lit pas ce fichier (mecanismes.md §14). Pour chaque tâche, lister les accords de ce fichier qu'elle rencontre, valeurs par défaut de D1 et de F1 comprises, et ceux des règles par chemin et des CLAUDE.md de sous-dossier des dossiers où elle écrit (leur exception s'écrit aussi ici, avec sa portée). Pour chacun, appliquer le choix de G4b : l'exception ci-dessous (une ligne par tâche, verbe adapté à l'accord levé ; aucune ligne sans exception choisie), ou l'arrêt de la tâche à cette étape, avec un compte rendu, écrit dans sa procédure. Un arrêt laisse un compte rendu : citer son fichier dans la clause (« La session programmée [nom] écrit son compte rendu dans `[emplacement]` sans accord. »), sinon l'accord de D1 l'arrête aussi. Un interdit ne reçoit jamais d'exception. -->
## Sessions sans surveillance

- Une session programmée suit seulement son prompt et `[procédure]` ; elle ne modifie pas [fichiers protégés].
- La session programmée [nom] crée sans accord les fichiers que fixe sa procédure ; elle ne fait jamais [interdits].

## Entretien de ce fichier

- Une correction répétée deux fois devient une règle ici ; une règle devenue fausse est supprimée.
- Les dates d'événements et les statuts vont dans `[chemin du suivi]`, jamais ici. La prochaine revue de ces consignes y figure comme une tâche datée.

<!-- Propriétaire : [nom] · Revue : [fréquence] · Créé avec le kit Architecte consignes v1.1 -->
