# Questionnaire de l'entretien

Questions de l'étape 2 (« Interroger »), en huit blocs : ce qu'il faut détecter avant de demander, les options, la valeur par défaut et la destination de chaque réponse. Lire au début de l'étape 2 ; relire la section d'un bloc avant de le poser.

## Conduite de l'entretien

- Poser les blocs dans l'ordre, de A à H.
- Une question porte sur une seule décision, sans sous-question cachée. Ne pas poser ce que résolvent la demande initiale, le cadrage, l'étape 1 ou une réponse précédente : les réponses détectées d'un bloc se confirment ensemble, en une seule question (« Je retiens : X, Y et Z ; à corriger ? »). Ne jamais rouvrir une décision prise, sauf à l'initiative de l'utilisateur ou pour un écart constaté à la reprise (`SKILL.md`, règle 8) : une question par décision touchée, garder ou corriger.
- Au plus quatre questions par message ; la validation d'un résumé compte pour une question et peut partager le message avec les questions du bloc suivant. Viser 12 à 18 messages pour un entretien complet.
- Avec AskUserQuestion : deux à quatre options par question, choix multiple possible (`mecanismes.md` §13) ; sinon, en texte numéroté (« A1. … 1) … 2) … 3) autre, à préciser »).
- Chaque question admet une réponse libre ; les options suivent le registre de l'utilisateur (vouvoiement par défaut) et s'adaptent à ce que l'étape 1 a montré.
- Mots des réglages : les dire une fois, en mots simples, avant la première question qui propose un réglage (C4, sinon le bloc F ; en refonte, avant le tableau des constats de l'étape 1 s'il en propose un, `SKILL.md`, règle 6). « Bloqué » : Claude Code refuse l'action, même si vous la demandez ; vous la faites alors vous-même. « Confirmation » : Claude Code vous affiche une demande d'autorisation avant chaque action de ce type ; vous acceptez ou vous refusez. « Consigne » : Claude s'engage à la suivre, sans garantie. Ajouter (`mecanismes.md` §6) : selon le mode de permission, Claude Code demande déjà avant la plupart des actions (mode manuel) ou décide seul pour beaucoup d'entre elles (mode auto, par défaut en terminal et dans VS Code ; dans l'onglet Code, voir le sélecteur sous la zone de saisie) ; une règle de confirmation garde la demande d'autorisation pour les actions choisies, quel que soit le mode, mais seulement sous les formes et dans les outils qu'elle couvre. Cowork ou claude.ai : ces mots ne valent que pour l'outil d'un connecteur (Blocked, Needs approval, `mecanismes.md` §12) et, dans Cowork, pour un blocage par l'organisation de tout l'outil de commandes (`Bash`) ou de récupération web (`WebFetch`) (`mecanismes.md` §6). Dans les résumés, le plan et le récapitulatif, écrire « demande d'autorisation » ou « confirmation (demande d'autorisation) », jamais un nombre de « confirmations » sans explication.
- « Je ne sais pas » : valeur par défaut annoncée, ou « à confirmer » ; ne jamais choisir à la place de l'utilisateur sans le dire. Après deux « je ne sais pas » dans un bloc, proposer d'appliquer d'un coup les valeurs par défaut restantes, listées. Dans un fichier d'équipe, une valeur par défaut vaut pour tous : pour une question non essentielle, ne rien écrire. Les garde-fous de C3, C4, E4b, F1, F2 et G4b sont essentiels : leur valeur par défaut s'écrit, annoncée dans le résumé du bloc.
- Une consigne existante inexacte (étape 1 : commande introuvable, source absente) se traite dans son bloc (G, C ou D) : corriger, garder avec « à confirmer » ou retirer.
- Destinations (liste de `SKILL.md`, étape 3) : maître ; satellite importé ; satellite à la demande ; règle par chemin ; CLAUDE.md de sous-dossier ; skill ; réglage (ou hook, option avancée) ; suivi ; mémoire automatique ; préférences personnelles (`CLAUDE.local.md` ou `~/.claude/CLAUDE.md`) ; nulle part. Sections du maître : `modele-CLAUDE-projet.md` ; satellites : `consignes/` par défaut ; l'étape 3 confirme chaque destination (`routage.md`).
- Dossier de code : hors documents produits, D3 à D5 et D7 sont sans objet ; H2 et H3 aussi, si suivi extérieur et historique dans git.
- Clore chaque bloc par son résumé de trois lignes (modèle en fin de bloc), à valider puis à reporter dans `_entretien-claude-md.md` (« Résumés validés par bloc »). Un résumé corrigé, à l'initiative de l'utilisateur ou après un écart constaté à la reprise, se valide de nouveau et se note au brouillon avec la date ; vérifier alors ses effets sur les autres blocs (registre et langue des fichiers, partage et brouillon, réglages), et sur le plan, s'il est déjà validé : présenter les lignes changées, obtenir un nouvel accord, les reporter dans le tableau du plan du brouillon, puis noter « Plan validé : oui (ajusté après reprise, [date]) ». Sans accès aux fichiers, remettre le résumé cumulé et autonome, aux titres du brouillon. Jamais de secret. S'arrêter dès que les réponses suffisent.

## Rappel : le lot de cadrage (étape 0)

Ce lot, défini dans `SKILL.md`, se pose une seule fois ; ce que la demande initiale dit déjà s'y confirme en une question. La racine détectée et l'invitation à coller un résumé précédent sont des informations de l'annonce, pas des questions ; répondre au cadrage sans corriger la racine la confirme. Ses réponses orientent ce questionnaire :

| Question de l'étape 0 | Effet sur l'étape 2 |
|---|---|
| Objectif | Audit seulement : pas d'étape 2 (`controle-qualite.md` section 4). Préférences personnelles : blocs B, F et G, limités à ce qui vaut dans tous les projets |
| Outil | Cowork ou claude.ai : note ci-dessous ; avec Claude Code sur le même dossier, le maître fait foi (`routage.md` section 7). Plusieurs agents : une règle valable pour tous va dans `AGENTS.md` ; ce qui touche aux fonctions de Claude Code (skills, réglages, commandes `/…`), dans le CLAUDE.md voisin, qui importe `@AGENTS.md` |
| Partage | Équipe, git ou synchronisé : préférences dans `~/.claude/CLAUDE.md`, ou dans `CLAUDE.local.md` et `.claude/settings.local.json` exclus du partage ; pas de `CLAUDE.local.md` si le projet n'a qu'un `AGENTS.md` (`mecanismes.md` §9) ; rien de sensible dans un fichier partagé. Moi seul : pas de H5 |
| Arborescence | « Analyser l'existant » et « en proposer une » valent demande d'arborescence : le bloc D fixe les règles de la cible, validée avec le plan (étape 3), migration seulement sur accord. « Ne pas y toucher » : D règle seulement le classement des nouveaux fichiers |

Cowork ou projet claude.ai : le maître et ses imports deviennent les instructions du projet ; les références à la demande, des fichiers du dossier du projet (Cowork) ou de connaissance (projet claude.ai) ; une procédure récurrente, un skill importé sur le compte claude.ai. Aucune règle par chemin n'y est documentée. Seuls se règlent l'outil d'un connecteur (Blocked ou Needs approval, `mecanismes.md` §12) et, dans Cowork, l'outil `Bash` ou `WebFetch` entier (deny, `mecanismes.md` §6 ; réglage géré par l'organisation ; depuis les réglages utilisateur ou projet : non documenté, à vérifier dans l'application) : tout autre interdit reste une consigne non garantie. Skills dans Cowork : rien au-delà de `mecanismes.md` §12.

## A. Identité et finalité de l'espace

- Objectif : pouvoir écrire en une à trois phrases ce qu'est l'espace, ce qu'on y produit et pour qui.
- À détecter avant de demander : `README`, consignes existantes, nom du dossier, formats dominants (code, tableaux, textes longs, pièces administratives), modèles, destinataires visibles dans les en-têtes. Proposer : « D'après les fichiers, cet espace semble servir à [X] pour [Y]. Est-ce exact ? »

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| A1 | À quoi sert surtout cet espace ? | activité d'une entreprise ou d'un indépendant ; projet de code ; recherche ou rédaction ; vie administrative personnelle | la nature détectée, à confirmer | maître (phrase d'ouverture) |
| A2 | Pour qui sont les documents produits ? (choix multiple) | vous-même ; clients ou partenaires ; administrations et organismes ; lecteurs ou utilisateurs | vous-même | maître ; un destinataire tiers ouvre D7 |
| A3 | Que produisez-vous ici le plus souvent ? (choix multiple) | textes (courriers, rapports, articles) ; code ou scripts ; tableaux et chiffres ; classement et suivi de dossiers | les productions détectées | maître (une phrase) ; une production répétée alimente le bloc E |
| A4 | Quels termes, sigles ou noms Claude doit-il connaître ? | aucun ; quelques termes (les citer) ; un glossaire existe (indiquer le fichier) | aucun | maître ; au-delà d'une quinzaine de lignes de contexte, `consignes/contexte.md`, importé |
| A5 | Des dossiers sont-ils à ignorer ? | non ; oui (les citer) | non | maître (une ligne) ; un dossier à ne jamais ouvrir relève de C4 |

Résumé à valider :
```text
A. Espace : [nature] ; produit [productions] pour [destinataires].
Vocabulaire : [termes ou « aucun »] ; à ignorer : [dossiers ou « rien »].
Destination : maître [+ consignes/contexte.md] ; à confirmer : [liste ou « rien »].
```

## B. Communication avec l'utilisateur

- Objectif : fixer, en consignes vérifiables, la façon dont Claude répond, et la langue des fichiers produits.
- À détecter avant de demander : langue des fichiers et des consignes existantes (`AGENTS.md` partagé compris), registre de l'utilisateur, préférences déjà écrites dans `~/.claude/CLAUDE.md` ou un CLAUDE.md existant (ne pas les répéter). Proposer : « Je retiens : [langue], [registre], consignes en [langue] ; à corriger ? »

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| B1 | Quelle langue et quel registre pour vous répondre ? | français, vouvoiement ; français, tutoiement ; une autre langue (la citer) ; la langue de chaque message | langue et registre de la conversation | selon B5 |
| B2 | En quelle langue écrire les fichiers de consignes ? | celle de vos réponses (B1) ; celle des consignes existantes ou d'un `AGENTS.md` partagé ; une autre langue (la citer) | celle des consignes existantes ; sinon celle de la conversation | étape 5 : titres des modèles et dossier de consignes traduits ; aucune ligne |
| B3 | Quelle forme de réponse préférez-vous ? | le résultat d'abord, en quelques lignes ; une réponse détaillée, raisonnement compris ; listes et tableaux ; selon la tâche | le résultat d'abord, puis le détail utile | selon B5 |
| B4 | Quand une information manque, que doit faire Claude ? | écrire « à confirmer » et continuer ; s'arrêter et vous demander ; proposer une hypothèse signalée comme telle | écrire « à confirmer » et continuer | maître ; vaut aussi pour une entrée manquante d'un skill, sauf si la tâche ne peut pas se faire sans elle |
| B5 | Pour qui valent B1 et B3 ? | toute personne qui travaille dans cet espace ; vous seul, dans cet espace ; vous seul, dans tous vos projets | cet espace ; vous seul si le partage n'est pas « moi seul » | Claude en déduit le fichier au plan : maître (« Façon de travailler avec moi »), `CLAUDE.local.md` ou `~/.claude/CLAUDE.md` |

Résumé à valider :
```text
B. Réponses en [langue], [registre], [forme], valables pour [portée] ; fichiers de consignes en [langue].
Information manquante : [conduite].
Destination : [maître ou préférences personnelles] ; à confirmer : [liste].
```

## C. Sources de vérité et confidentialité

- Objectif : savoir quel fichier fait foi pour chaque information, et ce que Claude ne doit ni ouvrir ni recopier.
- À détecter avant de demander : fichiers qui semblent faire foi (fiche d'identité, référentiel, grille de prix, suivi), doublons et versions concurrentes, dossiers au nom sensible (`.env`, `secrets`, banque, santé, personnel), repérés sans les ouvrir, règles `deny` existantes. Dossier mêlant sources et données personnelles : n'ouvrir que la source désignée par son nom. Fichier de secrets dans l'espace : constat bloquant (une gravité, pas un arrêt), sans l'ouvrir ; proposer à l'utilisateur de le sortir lui-même. S'il le garde : deny de lecture nommé (C4), limites dites une fois (bloc F) et statut « risque accepté ». S'il annonce qu'il le sortira lui-même et que le fichier est encore là quand les réglages s'écrivent : même deny nommé, provisoire (C4), et statut « sortie annoncée, blocage provisoire ». Fichier d'environnement exigé par l'outillage d'un dossier de code : cas prévu par `controle-qualite.md` C21.
- Proposer en une question : « Ces fichiers semblent faire foi : [type → fichier]. Les confirmez-vous ? » ; C1 se pose par type seulement sans source détectée.

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| C1 | Pour [type d'information], quelle source fait foi ? | le fichier détecté ; un autre fichier (l'indiquer) ; un outil extérieur (logiciel, tableur en ligne, site) ; aucune, à créer | à confirmer : ne jamais désigner une source à la place de l'utilisateur | maître (« Où trouver quoi », lignes non évidentes) ; détail dans `consignes/sources.md` |
| C2 | Si deux sources se contredisent, que faire ? | la source désignée en C1 l'emporte ; la plus récente l'emporte ; signaler l'écart et demander | signaler l'écart et demander | un seul lieu : `consignes/sources.md` s'il existe, le maître n'y renvoyant que par « Où trouver quoi » ; sinon une ligne au maître |
| C3 | Que Claude ne doit-il jamais inventer ? (choix multiple) | chiffres et montants ; noms, coordonnées et identités ; dates et échéances ; références (citations, articles, numéros) | tout cela : écrire « à confirmer » | maître (« Interdits ») |
| C4 | Quels fichiers Claude ne doit-il jamais ouvrir ? (choix multiple) | secrets (`.env`, clés, mots de passe) ; un dossier confidentiel (le citer) ; données de tiers (santé, paie, dossiers personnels) ; aucun. Fichier de secrets trouvé dans l'espace : l'option « aucun » cède la place à « je sors moi-même [fichier] de l'espace » (quatre options au plus, `mecanismes.md` §13) ; la question dit que sa lecture sera bloquée par réglage dans les deux cas : durablement s'il reste (risque accepté), en attendant sa sortie sinon (blocage provisoire) | les fichiers de secrets usuels | `deny` (Claude Code), par exemple `Read(./.env)`, pour ce qu'un nom, une extension ou un dossier désigne ; le reste (« mots de passe, où qu'ils soient ») en consigne seulement ; sortie annoncée, fichier encore présent quand les réglages s'écrivent : deny nommé provisoire (`Read(./chemin/du/fichier)`), dit au plan et au récapitulatif (« à garder si le fichier revient, ou à retirer après sa sortie », avec sa ligne au maître), C21 « sortie annoncée, blocage provisoire » ; ligne du maître (« Interdits ») suivie de la mention d'un deny de lecture `Read(./…)`, selon la règle sur l'outil de terminal de l'application (`SKILL.md`, étape 5, « Mentions au maître ») ; un secret reste hors de l'espace (limites en F) |
| C5 | Une donnée sensible sert-elle à une tâche précise ? | non ; oui, lue dans un fichier par la seule procédure qui l'utilise ; oui, saisie par vous au moment voulu | non ; sinon saisie par vous | chemin du fichier cité dans le seul skill ou la seule procédure qui l'utilise, jamais la valeur ; rien au maître, en import ni au brouillon ; fichier fermé en C4 : saisie par vous |
| C6 | Cowork ou claude.ai : quelles tâches ont besoin de [fichier sensible du projet] ? | aucune, le sortir du projet ; [tâches citées], le garder | à confirmer : rien ne sort sans réponse | liste des fichiers du projet ; gardé, avec ses garde-fous de contenu (F3) ; avant de le sortir, dire ce que Claude ne pourra plus faire et adapter l'ouverture (A) |

Résumé à valider :
```text
C. Sources : [information → fichier] ; en cas d'écart : [règle].
Jamais inventé : [liste] ; jamais ouvert : [chemins] ; sortie annoncée : [fichier, lecture bloquée en attendant (blocage provisoire), ou « aucune »] ; donnée sensible : [usage ou « aucune »].
Destination : maître [+ consignes/sources.md, hors version minimale] + lecture bloquée par réglage (deny) ; à confirmer : [liste].
```

## D. Organisation et nommage

- Objectif : une règle courte pour ranger et nommer, avec ses exceptions, et les conventions des documents destinés à des tiers.
- À détecter avant de demander : motifs de nommage dominants (date en tête, numéros, préfixes), zone d'entrée (« à traiter », téléchargements), archives, modèles et leurs mentions, fichiers en vrac à la racine, `CLAUDE.md` dans des archives ou des modèles (le signaler : il reste actif, `mecanismes.md` §1). Proposer : « La plupart des fichiers sont nommés [motif] : en faire la règle ? »

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| D1 | Où va un nouveau document ? | dans le dossier de son sujet ; dans une zone d'entrée, classé ensuite ; Claude propose, vous validez | Claude propose l'emplacement et attend votre accord | maître (« Classement et nommage ») |
| D2 | Quelle règle de nommage ? | la convention détectée ; date en tête (`AAAA-MM-JJ-objet`) ; préfixe numéroté ; nom libre mais explicite | la convention détectée ; sinon date en tête | maître (règle et un exemple réel) ; exceptions dans `consignes/conventions.md` |
| D2b | Nom daté ou numéro : quelle date fait foi ? | la création du document ; l'envoi ; la réception | la création du document, annoncée | maître, avec la règle de nommage |
| D3 | Numérotez-vous ou versionnez-vous des documents ? | non ; numéro tenu dans un registre (le citer) ; suffixe de version (`v2`) ; ancienne version déplacée aux archives | version remplacée : aux archives ; numéro : à confirmer (pas de défaut) | `consignes/conventions.md` ; le compteur, dans un seul registre cité dans « Où trouver quoi », jamais dans une consigne |
| D3b | Si numéro : quand est-il attribué ? | à la création du document ; à l'émission ou à l'envoi ; à la réception | à confirmer | `consignes/conventions.md` |
| D4 | Comment archivez-vous ? | un dossier d'archives unique ; des archives dans chaque dossier ; pas d'archives | un dossier d'archives unique | maître (une ligne) ; étape 4 |
| D5 | Quels formats de sortie ? | Markdown ; documents bureautiques (texte, tableur) ; PDF ; celui du modèle existant | celui du modèle ; sans modèle, « à confirmer » jusqu'à la première production réelle | `consignes/conventions.md` |
| D6 | Un dossier ou un type de fichier a-t-il des règles propres ? | non ; oui (le dossier et la règle) | non | règle par chemin (`.claude/rules/<sujet>.md` avec `paths`) ou CLAUDE.md de sous-dossier |
| D7 | Documents destinés à des tiers (si A2 en cite) : quel ton, quelles mentions ? | vouvoiement formel ; ton direct et cordial ; selon le destinataire ; mentions obligatoires ou formules interdites (les citer) | vouvoiement formel | un seul lieu : en refonte, une règle sans `paths` existante qui le porte déjà (`routage.md` section 2) ; sinon `consignes/conventions.md` s'il existe, sinon le maître (« Documents destinés à des tiers ») ; l'autre lieu y renvoie sans reformuler |

Résumé à valider :
```text
D. Nouveau document : [emplacement] ; nommage : [règle], par exemple [exemple], date qui fait foi : [date] ; versions et numéros : [règle].
Archives : [règle] ; formats : [liste] ; règles propres : [dossiers ou « aucune »] ; tiers : [ton, mentions ou « sans objet »].
Destination : maître + consignes/conventions.md [+ règles par chemin] ; à confirmer : [liste].
```

## E. Tâches récurrentes

- Objectif : repérer les tâches qui reviennent, choisir pour chacune un skill, une procédure à la demande ou rien, et fixer le critère de « terminé ».
- À détecter avant de demander : modèles de documents, scripts, dossiers par période (mois, trimestre, année), listes de contrôle, procédures écrites, `.claude/skills/` et `.claude/commands/` existants, tâches programmées citées dans les consignes. Proposer : « Ces modèles suggèrent des tâches qui reviennent : [liste]. Lesquelles garder ? »

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| E1 | Quelles tâches reviennent régulièrement ? (choix multiple, cinq au plus) | les tâches détectées ; produire un document type ; mettre à jour un suivi ou un tableau ; faire un contrôle périodique | les tâches détectées, à confirmer | une fiche par tâche dans le brouillon |
| E2 | Qu'est-ce qui déclenche [tâche] ? | votre demande ; une date fixe (tâche programmée) ; l'arrivée d'un document | votre demande | skill (`/nom`) ; date fixe : G4 ; document : déclencheur dans le maître (« Procédures ») |
| E3 | Les étapes et les entrées de [tâche] sont-elles déjà écrites ? | oui, dans un fichier (l'indiquer) ; non, vous les décrivez maintenant ; non, Claude propose un déroulé à valider ; elles changent à chaque fois | à confirmer | pointer vers la procédure existante sans la recopier ; sinon la fiche |
| E3b | Que produit [tâche] ? | un texte dans la conversation ; un fichier (emplacement, nom, langue) ; la mise à jour d'un fichier existant (le citer) | un fichier rangé et nommé selon le bloc D | champ « Sortie » de la fiche |
| E4 | Quand [tâche] est-elle finie et réussie ? | un fichier attendu existe à un emplacement précis ; un contrôle passe (commande, comparaison à la source) ; vous relisez et validez | vous relisez et validez | dernière étape du skill ou de la procédure |
| E4b | Quand ne pas faire [tâche], ou que faire dans un cas limite ? (choix multiple) | une exception ou une condition (la citer) ; une échéance pas encore atteinte (laquelle) ; une donnée manquante (que faire) ; aucune exception connue | aucune exception connue : s'arrêter et demander en cas de doute | champ « Exceptions » de la fiche, repris dans le skill (`modele-skill-procedure.md`) ou la procédure |
| E5 | [Tâche] envoie, publie ou supprime-t-elle quelque chose ? | oui (préciser) ; non | oui en cas de doute | `disable-model-invocation: true` sur le skill (Claude Code seulement ; jamais dans un skill à importer sur claude.ai, `mecanismes.md` §11) ; l'action passe en F1 |
| E6 | Avant de dire « terminé », que doit faire Claude pour toute tâche ? (choix multiple) | lancer une commande de contrôle ; comparer à la source qui fait foi ; citer les fichiers créés, modifiés ou utilisés ; lister les points à confirmer | comparer à la source, citer les fichiers modifiés, lister les points à confirmer ; en code, lancer aussi les tests | maître (« Avant de dire “terminé” ») |

Poser E2 à E5 par tâche, en regroupant les tâches semblables ; des réponses détectées ou par défaut se confirment pour toutes dans un seul tableau (une question). Au-delà de trois tâches, détailler les trois plus fréquentes ; les autres restent « à confirmer ». Sauter E5 si l'utilisateur a déjà dit ce que la tâche envoie ou publie. E4 fixe le critère d'une tâche ; E6, posé une fois, le contrôle commun du maître. Pour E4b, proposer les exceptions que montrent les modèles et les sources lues (une échéance dans un contrat type, par exemple), à confirmer.

Si l'utilisateur ne sait pas décrire les étapes (E3), Claude propose un déroulé tiré de ses réponses, comme proposition à valider, jamais comme valeur par défaut ; validé, il vaut étapes connues et la tâche peut devenir un skill. Remplir la fiche de chaque tâche dans le brouillon ; une case vide reste « à confirmer » :

```text
Tâche : [verbe + objet, par exemple « préparer le point mensuel »]
Déclencheur : [votre demande, une date, l'arrivée d'un document]
Entrées : [fichiers, modèles, informations à demander]
Étapes : [trois à dix étapes, dans l'ordre, chacune avec un verbe]
Sortie : [texte, ou fichier : emplacement, nom, langue]
Fini quand : [contrôle observable : fichier présent, chiffres comparés à la source, relecture]
Exceptions : [quand ne pas la faire, cas limites]
Action engageante : [non, ou laquelle : envoi, publication, suppression, paiement]
```

Tâche dont le déclenchement dépend des données (liste à relancer, dossiers à traiter) : avant de rédiger son skill, appliquer son critère et ses exceptions à la source qui fait foi, en lecture seule. Montrer le résultat à l'utilisateur sans recopier de donnée personnelle (nombre de cas retenus et écartés, chacun désigné par sa ligne dans la source, `fichier:ligne`, jamais par un nom de dossier qui contient un nom de personne). Un écart corrige la fiche, validée de nouveau. Sans accès aux fichiers : demander à l'utilisateur d'appliquer lui-même le critère et ses exceptions à la source, et de donner le nombre de cas retenus et écartés ; sans réponse, noter le critère « non vérifié sur les données » dans « À confirmer ».

Choisir la forme d'après la fiche : un skill ne pèse que par son nom et sa description avant l'appel ; une procédure à la demande ne pèse rien, mais sa lecture n'est pas garantie (`mecanismes.md` §4).

| Si la fiche montre | Alors |
|---|---|
| une tâche fréquente, aux étapes stables | skill `.claude/skills/<nom>/SKILL.md` (`modele-skill-procedure.md`), appelé par `/nom` |
| une tâche qui envoie, publie ou supprime | skill avec `disable-model-invocation: true` (Claude Code seulement, voir E5), et l'action en F1 |
| une tâche rare, ou des étapes qui changent encore | procédure à la demande `consignes/<tache>.md` (`modele-satellite-procedure.md`), avec un déclencheur dans le maître |
| une ou deux étapes | une ligne dans le maître, ou rien |
| des règles liées à un dossier ou à un type de fichier | règle par chemin plutôt que skill |
| un déclencheur à date fixe | skill ou procédure, plus G4 ; le prompt de la tâche programmée renvoie à la procédure ; contrôler la présence de la sortie, car l'historique de la tâche ne prouve pas que le travail a été fait (`mecanismes.md` §14) |
| des étapes inconnues, sans déroulé validé | « à confirmer », pas de skill |

Résumé à valider :
```text
E. Tâches retenues : [tâche → déclencheur → sortie], une par tâche ; avant « terminé » : [contrôle commun].
Engageantes : [liste ou « aucune »] ; exceptions : [tâche → cas, ou « aucune connue »] ; étapes inconnues : [liste ou « aucune »].
Destination : skills [noms] + procédures [fichiers] + maître (« Avant de dire “terminé” ») ; à confirmer : [liste].
```

## F. Garde-fous : accord préalable et interdits

- Objectif : lister les actions soumises à accord et les interdits, puis décider lesquels l'outil applique.
- À détecter avant de demander : `.claude/settings.json` et `.claude/settings.local.json` (autorisations larges : `Bash(*)`, `python -c *`, commande nommée qui exécute du code du dépôt tant que ce code se modifie sans demande, `controle-qualite.md` C16), interdits déjà écrits, scripts d'envoi ou de publication, connecteurs et outils qui agissent au nom de l'utilisateur, font sortir du texte ou lancent des commandes hors de Bash et PowerShell (relevés à l'étape 1 ou à la dernière reprise dans la liste d'outils de Claude, `SKILL.md`), serveurs MCP déclarés dans `.mcp.json` (portée projet, partagés avec le dépôt, `mecanismes.md` §6), serveurs installés mais pas encore connectés (en attente d'authentification, ceux des plugins par exemple), relevés à l'étape 1 tels qu'ils apparaissent dans la session, liste parfois tronquée (« …and N more » : noms à demander à l'utilisateur, `SKILL.md`, étape 1), et notés « à confirmer » (§6), dossiers de production ou partagés. Proposer : « Ces actions semblent engageantes ici : [liste]. Faut-il votre accord pour chacune ? »

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| F1 | Pour quelles actions Claude doit-il demander votre accord à chaque fois ? (choix multiple) | envoyer, publier ou partager hors de l'espace ; supprimer, déplacer, renommer ou écraser un fichier ; payer, signer ou modifier un compte ; toucher à la production ou à des données partagées | les deux premières | maître (« Demander mon accord avant de », une phrase complète par action) ; confirmation (`ask`) si une commande ou un outil précis porte l'action, valeur par défaut pour supprimer, déplacer ou renommer par une commande, au lieu du blocage ; l'écrasement reste une consigne, dite au résumé F (aucune règle de `modele-settings.json` ne le vise) (Cowork ou claude.ai : outil de connecteur sur Needs approval) ; en équipe, nommer qui donne l'accord |
| F2 | Au-delà des fichiers fermés en C4, quels interdits n'admettent aucune exception ? (choix multiple) | lancer une commande précise (la citer) ; joindre un site précis ; un outil de connecteur (envoi de message, par exemple) ; supprimer des fichiers, impossible même si je le demande (bloqué ; vous le faites vous-même) | ceux de C4, repris sans les redemander | maître (« Interdits », avec la mention de `SKILL.md`, étape 5, « Mentions au maître ») et réglage `deny` ; Cowork ou claude.ai : outil de connecteur sur Blocked |
| F3 | Au-delà de C3, quels interdits portent sur le contenu ? (choix multiple) | prendre un engagement en votre nom (prix, délai, accord) ; modifier un document déjà envoyé ou signé ; aucun ; autre (le citer) | aucun au-delà de C3 | maître (« Interdits ») ; consigne seulement, sauf chemin reconnaissable (un dossier de factures, par exemple) : proposer au plan une confirmation sur l'édition de ce chemin (`Edit(./dossier/**)`, création comprise ; mention au maître : `SKILL.md`, étape 5, « Mentions au maître ») ; consigne seule choisie : C14 note « consigne choisie », pas « non conforme » |
| F4 | Quelles autorisations trop larges retirer ou restreindre ? (si l'étape 1 en a trouvé ; choix multiple) | une option par règle trouvée (« retirer `Bash(*)` », « restreindre … », « passer `Bash(npm run test)` en `ask` »), trois au plus par question, puis une question de plus ; aucune, les garder en connaissance de cause | aucune : rien n'est retiré ; « à confirmer », redemandé avec les différences à l'étape 5 | réglage concerné : chaque règle retirée ou restreinte sur accord explicite, différences montrées avant d'écrire ; règle gardée : statut « risque accepté » (`controle-qualite.md` C16), et mention au maître pour une commande qui exécute du code du dépôt (paragraphe « Autorisation gardée » ci-dessous) |

Même action en accord (F1) et en interdit (F2), la suppression par exemple : garder la confirmation, c'est-à-dire la seule ligne « Demander mon accord avant de … » au maître et la règle `ask`, sans ligne d'interdit ni `deny` pour cette action ; le dire dans le résumé F, où l'utilisateur peut corriger.

Classer chaque garde-fou ; ce qui n'entre dans aucune catégorie ne s'écrit pas :

| Catégorie | Sens | Où l'écrire | Effet |
|---|---|---|---|
| Demander mon accord | action qui engage hors de l'espace ou se défait mal, permise après un oui explicite pour elle | maître (« Demander mon accord avant de ») ; en plus `ask` si une commande ou un outil précis la porte (Cowork ou claude.ai : outil de connecteur sur Needs approval) | consigne seule : non garantie ; avec `ask`, Claude Code affiche une demande d'autorisation |
| Interdit écrit | action impossible même par erreur, que l'outil ne reconnaît pas : contenu, jugement, action mal délimitée | maître (« Interdits ») | Claude essaie de le respecter, sans garantie |
| Bloqué par l'outil | action impossible même par erreur, reconnaissable : chemin, commande, domaine, outil de connecteur (`mcp__<serveur>__<outil>`, nom canonique demandé à Claude, pas le libellé de la demande d'autorisation, `mecanismes.md` §6) | `deny` dans `.claude/settings.json` (ou hook, option avancée) ; Cowork ou claude.ai : outil de connecteur sur Blocked (`mecanismes.md` §12) ; au maître, la ligne suivie de la mention de `SKILL.md`, étape 5, « Mentions au maître » | appliqué par l'outil : dans Claude Code ; dans Cowork et claude.ai, pour l'outil d'un connecteur (et, dans Cowork, `Bash` ou `WebFetch` entier par réglage géré) ; un `deny` l'emporte sur tout `allow` (exception des mods, `mecanismes.md` §6) |

Chaque interdit est une phrase négative complète (« Ne jamais pousser sur `main`. »), et chaque accord préalable une phrase complète (« Demander mon accord avant de supprimer un fichier. »), justes hors de leur titre et une fois traduites. Plusieurs agents : l'interdit dans `AGENTS.md`, la mention du réglage dans le CLAUDE.md voisin. Lignes préremplies des modèles et règles de `modele-settings.json` : des propositions, gardées si elles répondent aux blocs C, F ou G, jamais contre une réponse.

Interdit d'envoi ou de sortie de texte (réponse à F2, ou exprimé ailleurs, demande initiale ou bloc C compris : « il n'envoie jamais rien lui-même », un accord de confidentialité). En Claude Code, proposer le deny de chaque outil relevé à l'étape 1 ou à la dernière reprise qui le permet, par exemple : outil de connecteur (nom canonique `mcp__<serveur>__<outil>`), `WebFetch`, `WebSearch`, `Artifact` (publication d'une page sur claude.ai). Un outil d'envoi apparu à la reprise repasse par cette proposition, même si le résumé F est validé. Serveur de `.mcp.json` qui envoie ou publie, sans ses noms d'outils dans la liste de Claude (serveur pas encore approuvé, déduction) : deny de tous ses outils, `mcp__<serveur>__*` ou `mcp__<serveur>`, noté « à vérifier », sans mention « bloqué » au maître, jusqu'à une session où le serveur est approuvé et ses outils absents ; pour écarter le serveur entier, proposer plutôt `disabledMcpjsonServers` (`mecanismes.md` §6 ; `routage.md` section 5). Serveur installé mais pas encore connecté (en attente d'authentification, celui d'un plugin par exemple), relevé à l'étape 1 tel qu'il apparaît dans la session : proposer aussi son blocage d'avance par préfixe, `mcp__plugin_<plugin>_<serveur>__*` pour un serveur de plugin, `mcp__<serveur>__*` sinon (formes documentées, §6), noté « à vérifier » : l'effet d'un deny écrit avant la connexion, une fois le serveur connecté, n'est pas documenté (§6). Ce service va dans « à confirmer » du récapitulatif, avec la question de recette à reposer après sa connexion (mention au maître : `SKILL.md`, étape 5, « Mentions au maître »). Dire ce que chaque deny retire : l'outil disparaît de la liste de Claude pour toutes les tâches (`mecanismes.md` §6). Un deny `WebFetch` n'arrête pas une commande réseau lancée par Bash (`curl`) ; il en va de même, par déduction, des autres deny et d'une commande PowerShell (`Invoke-WebRequest`) : la commande relève des règles Bash ou PowerShell et du mode de permission (`mecanismes.md` §6). Pour ces commandes, proposer au moins la protection d'un accord : une confirmation (demande d'autorisation) par défaut, ou un blocage si l'utilisateur le veut, sur `Bash(curl *)`, `Bash(wget *)`, `PowerShell(Invoke-WebRequest *)` et `PowerShell(Invoke-RestMethod *)`, en plus de la règle sur l'outil de terminal de l'application (paragraphe « Commandes lancées hors de Bash et PowerShell ») ; ces règles portent sur le texte : un autre programme (`curl.exe` lancé par PowerShell, par exemple), `bash -c` ou un script leur échappent (§6). Au maître, l'interdit se restreint aux services réellement bloqués (« Ne jamais envoyer ni publier de texte par [ces services, en mots simples]. »), et les commandes réseau couvertes ont leur ligne, restreinte à l'envoi (« Ne jamais envoyer de données sur le réseau par `curl`, `wget`, `Invoke-WebRequest` ou `Invoke-RestMethod`. ») ; leurs mentions : `SKILL.md`, étape 5, « Mentions au maître », lignes « Outils d'envoi vers l'extérieur bloqués » et « Commandes réseau ». Toute autre commande réseau reste une consigne, sur une ligne à part (« Ne jamais envoyer de données sur le réseau par une autre commande. » ; sans règle réseau acceptée : « Ne jamais lancer de commande qui envoie des données sur le réseau. »). Deny refusé : interdit écrit seulement, sans mention « bloqué », refus noté dans le résumé F, statut « risque accepté » (`controle-qualite.md` C14). Cowork ou claude.ai : outil de connecteur sur Blocked (`mecanismes.md` §12) ; `WebFetch` et `WebSearch` restent une consigne (dans Cowork, hors deny géré par l'organisation, `mecanismes.md` §6).

Outils de l'application qui transmettent seulement à l'utilisateur lui-même, relevés à part à l'étape 1 sous leur nom dans la liste d'outils (messagerie entre ses sessions, envoi d'un fichier à ses appareils, notification, lancement ou transfert de session, Remote Control, qui relie la session au compte claude.ai pour la suivre et la piloter depuis claude.ai ou l'application mobile ; écriture dans son seul compte claude.ai, `SendToProject` ou `SendToProjectContext` par exemple, sauf s'ils publient pour des tiers, dans un projet partagé par exemple) : d'après leur description, ils ne transmettent pas à des tiers (non documenté, à vérifier dans l'application). Ils n'entrent pas dans le deny proposé pour un interdit d'envoi, sauf si l'interdit vise tout texte qui sort de l'ordinateur, ou si l'utilisateur le demande ; le dire à l'utilisateur, en mots simples (« écrire dans vos projets claude.ai », par exemple), en précisant que, s'il partage un de ces projets avec d'autres personnes, les outils qui y écrivent vont avec les outils d'envoi vers l'extérieur. S'ils restent, le maître et le récapitulatif écrivent « les outils d'envoi vers l'extérieur », jamais « tous les outils d'envoi » ni « rien ne sort ». Envoi en accord (F1) et outils d'envoi bloqués (F2) : une seule ligne au résumé F, « outils d'envoi vers l'extérieur : bloqués ; autres moyens, par exemple une commande qui envoie des données sur Internet : demande d'autorisation, ou consigne ». Le maître garde alors pour ces autres moyens l'accord de F1 (« Demander mon accord avant d'envoyer… »), avec une demande d'autorisation sur les commandes réseau (règles du paragraphe précédent) si l'utilisateur l'accepte au plan, et n'écrit aucune ligne d'interdit sur les commandes réseau.

Commandes lancées hors de Bash et PowerShell : un outil relevé à l'étape 1 qui lance des commandes autrement, par exemple `mcp__terminal__run_in_terminal` dans l'application de bureau (il tape une commande dans un onglet de terminal de l'utilisateur), n'est visé ni par une règle `Bash(...)` ni par une règle `PowerShell(...)` (déduction : la documentation n'étend les règles Bash qu'à `Monitor`, `mecanismes.md` §6). Dès qu'une commande est bloquée ou soumise à confirmation (suppression, déplacement, réseau), proposer dans le résumé F, puis au plan, une confirmation sur cet outil entier : règle `ask` sur son nom complet, de forme `mcp__<serveur>__<outil>` (`modele-settings.json` la propose pour `mcp__terminal__run_in_terminal` ; §6 ; effet à vérifier dans l'application), ou son blocage (`deny`) si l'utilisateur le veut. Mention au maître d'une commande, selon les règles de ces outils : `SKILL.md`, étape 5, « Mentions au maître » (la ligne qui correspond). À l'utilisateur, dire « mes outils de commandes habituels (Bash et PowerShell) » et « mon outil qui tape des commandes dans le terminal de l'application ». Même proposition pour chaque autre outil relevé de cette liste, par exemple `mcp__Claude_Browser__preview_start` (« mon outil qui lance un serveur de développement »).

Autorisation gardée (F4, ou `controle-qualite.md` C16) sur une commande qui exécute du code du dépôt (script npm ou make, lanceur de tests), ce code se modifiant sans demande (mode Accept edits ou auto, `Edit` en allow) : statut « risque accepté ». Par déduction (`mecanismes.md` §6), un script du dépôt modifié puis lancé échappe aux deny de lecture et aux règles Bash ou PowerShell, deny comme ask. Le maître le dit dans « Commandes et pièges » (avec plusieurs agents, dans le CLAUDE.md voisin) : « Un script du dépôt modifié puis lancé par `[commande]` échappe aux deny de lecture et aux règles Bash (risque accepté). »

Limites à dire à l'utilisateur, en mots simples, les noms techniques entre parenthèses (`mecanismes.md` §6) :
- `.claude/settings.json` ne vaut que pour Claude Code (tous les utilisateurs ; `.claude/settings.local.json` : l'utilisateur seul) et se lit depuis le dossier de travail : lancer Claude à la racine, ou répéter les deny dans un sous-dossier ouvert seul, motifs `./` réécrits depuis ce sous-dossier et testés sur un fichier factice (`routage.md` section 2, Réglage).
- Un deny de lecture en `./` vaut dans ce dossier ; il couvre Read, Grep et Glob (au mieux), les commandes Bash `cat`, `head`, `tail`, `sed`, `tee` et les redirections, mais ni `grep -r` ni un script. Par l'outil de terminal de l'application en confirmation, la lecture ne fait que demander une autorisation (déduction, §6) ; par PowerShell (`Get-Content`), l'effet n'est pas documenté : la recette le teste sur un fichier factice. Mention au maître : `SKILL.md`, étape 5, « Mentions au maître ». Un secret reste hors de l'espace de travail.
- Une règle Bash porte sur le texte : `Bash(rm *)` ne bloque pas `bash -c 'rm …'`. Une règle PowerShell couvre les alias courants de la cmdlet (liste exacte non documentée). Par déduction, un joker sur un interpréteur (`python -c *`) laisse tout passer. Une règle Bash ou PowerShell ne vise pas non plus un autre outil qui lance des commandes, comme l'outil de terminal de l'application de bureau (déduction, paragraphe « Commandes lancées hors de Bash et PowerShell »).
- Un interdit de branche : demander si une confirmation suffit pour les formes que les motifs ne couvrent pas (un `git push` qui ne nomme pas `main`, lancé depuis `main`, par exemple). Oui : deny sur les formes nommées, avec `Bash(git push *)` en `ask` comme filet ; au maître, la mention d'un ask, jamais celle d'un deny. Non : deny de `Bash(git push *)`, qui refuse toute commande commençant par `git push`, quelle que soit la branche ; au maître, la mention d'un deny (mentions : `SKILL.md`, étape 5, « Mentions au maître »). Dans les deux cas, `git -C . push`, `git -c … push`, `bash -c` et un script restent hors d'atteinte de ces règles (`routage.md` section 5). En mode auto, le classifieur laisse passer par défaut un push vers toute branche du dépôt de travail, branche par défaut comprise, hors branche de déploiement comme `production` (`mecanismes.md` §6). La protection complète relève de l'hébergeur git, hors de ce kit. Une règle `Edit(...)` couvre aussi la création et l'écrasement d'un fichier.
- « Oui, ne plus demander » à une commande ou à un domaine web ajoute un `allow` dans `.claude/settings.local.json` : relire cette liste à chaque revue (bloc H).

Résumé à valider :
```text
F. Accord préalable : [actions, chacune « demande d'autorisation » ou « consigne »] ; interdits écrits (consigne) : [liste].
Bloqué : [actions, en mots simples] ; outils d'envoi vers l'extérieur sans blocage : [outils et refus, ou « aucun »] ; services pas encore connectés : [bloqués d'avance, à vérifier après leur connexion, ou sans règle, ou « aucun »] ; commandes qui peuvent envoyer des données sur Internet (`curl`, `Invoke-WebRequest`…) : [demande d'autorisation, bloquées, ou consigne] ; outils vers vos propres sessions ou appareils : [gardés ou bloqués] ; outils qui lancent des commandes autrement (terminal de l'application, serveur de développement) : [pour chacun : demande d'autorisation, bloqué, sans règle ; ou « sans objet »] ; autorisations larges : [sort décidé ou « aucune »].
Destination : maître + .claude/settings.json (blocages, demandes d'autorisation) ; à confirmer : [liste].
```

## G. Environnement et outils

- Objectif : noter seulement les outils et les pièges que Claude ne devinerait pas, et le périmètre des sessions sans surveillance.
- À détecter avant de demander : fichiers de projet de code (`package.json`, `Makefile`, `pyproject.toml`, scripts), formats qui supposent un logiciel (`.docx`, `.xlsx`), chemins avec espaces, hooks et réglages existants, tâches programmées et automatisations. Proposer : « Les commandes semblent être [liste] : les confirmez-vous ? »

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| G1 | Quels outils Claude utilise-t-il ici, au-delà des fichiers ? (choix multiple) | aucun ; bureautique (texte, tableur, PDF) ; navigateur, messagerie ou agenda connectés ; outils de développement | aucun | maître (« Commandes et pièges », une ligne par outil non évident) ; un outil qui agit en votre nom ouvre F1, et F2 s'il faut le bloquer |
| G2 | Quelles commandes faut-il connaître ? | les commandes détectées (construire, tester, lancer) ; des scripts maison (les citer) ; aucune | les commandes détectées, à confirmer | maître (« Commandes et pièges ») ; règle par chemin si propres à un dossier |
| G3 | Un piège a-t-il déjà fait perdre du temps ? | oui, un outil ou une commande, avec la bonne façon de faire ; oui, un fichier trompeur ou un doublon, avec la conduite à tenir ; non | non | maître (« Commandes et pièges ») ou règle par chemin ; sans conduite à tenir, reformuler (« Reformuler une réponse vague ») ou noter « à confirmer » |
| G4 | Que peut faire une session sans surveillance ? (si date fixe en E2 ou automatisation trouvée) | lire et préparer des brouillons ; écrire dans un dossier précis ; envoyer ou publier | lire et préparer des brouillons | maître (« Sessions sans surveillance » : ce qu'elle suit et ne touche pas) ; `allow` limité aux commandes nécessaires, nommément ; une commande qui exécute du code du dépôt que la tâche modifie vaut un joker (déduction, `controle-qualite.md` C16) : la laisser hors de l'`allow`, sinon statut « risque accepté » et mention au maître (bloc F, « Autorisation gardée ») ; tâche créée avec l'option « Only on this computer », sans laquelle elle ne lit pas le CLAUDE.md local ; première exécution testée à la main (`mecanismes.md` §14) |
| G4b | La tâche [nom] rencontre l'accord « [accord rencontré] » : que faire sans vous ? (une question par accord) | exception écrite au maître : la session programmée le fait sans accord, dans les limites de sa procédure ; arrêt de la tâche à cette étape, avec un compte rendu (si l'accord porte sur la sortie de la tâche, bloc E, elle ne produit plus que ce compte rendu : le dire dans la question) | arrêt, avec un compte rendu | exception : clause « Sessions sans surveillance » du maître, par exemple « La session programmée [nom] crée sans accord les fichiers que fixe sa procédure ; elle ne fait jamais [interdits]. » ; arrêt : étape du skill (`modele-skill-procedure.md`), et compte rendu daté (`compte-rendu-AAAA-MM-JJ.md`), seul fichier créé sans accord, cité dans cette clause (« La session programmée [nom] écrit son compte rendu dans `[emplacement]` sans accord. ») |

Avant G4b, lister pour chaque tâche programmée les accords préalables du maître qu'elle rencontre (« Demander mon accord avant de … »), valeurs par défaut de D1 et de F1 comprises, et ceux des règles par chemin et des CLAUDE.md de sous-dossier des dossiers où elle écrit (l'exception s'écrit dans la clause du maître, avec sa portée, `modele-regle-chemin.md`) : « mon accord » vise l'utilisateur de la session, absent pendant l'exécution. Les interdits ne reçoivent jamais d'exception. Un accord doublé d'une règle `ask` fait en plus attendre l'exécution dans sa session, exception écrite ou non (déduction, `mecanismes.md` §6 et §14) : le dire. Dans un script `claude -p`, les serveurs de `.mcp.json` se connectent sans accord (`mecanismes.md` §6) : leurs outils d'envoi relèvent des deny du bloc F.

Résumé à valider :
```text
G. Outils : [liste ou « fichiers seulement »] ; commandes : [liste ou « aucune »] ; pièges : [piège → conduite, ou « aucun »].
Sessions sans surveillance : [périmètre et réglages, ou « sans objet »] ; accords rencontrés : [accord → exception, ou arrêt et sortie non produite, ou « aucun »].
Destination : maître (« Commandes et pièges » [+ « Sessions sans surveillance »]) [+ règles par chemin] ; à confirmer : [liste].
```

## H. Entretien et suivi

- Objectif : séparer l'état des règles, et fixer qui entretient les consignes et à quel rythme.
- À détecter avant de demander : fichiers de suivi (liste de tâches, tableau, journal), suivis concurrents, dates d'événements et statuts dans les consignes existantes (« depuis le », « actuellement », « en cours » ; chercher les dates, même sans année), historique mêlé aux règles. Proposer : « Les tâches semblent suivies dans [fichier] : en faire le suivi qui fait foi ? »
- Hors questionnaire : ce que Claude apprend va dans la mémoire automatique (`mecanismes.md` §8).

| N° | Question | Options proposées | Par défaut | Destination |
|---|---|---|---|---|
| H1 | Où vit l'état des travaux (tâches ouvertes, échéances, statuts) ? | le fichier détecté ; un nouveau suivi court (`modele-suivi.md`) ; un outil extérieur (le citer) ; nulle part | un nouveau suivi court si aucun n'existe | suivi, pointé à la demande depuis « Avant d'agir », jamais importé |
| H2 | Qui met le suivi à jour ? | Claude, à la fin de chaque tâche qui change un état ; Claude, sur demande ; vous seul | Claude, à la fin de chaque tâche qui change un état | le suivi lui-même (règles de tenue, `modele-suivi.md`) ; le maître y renvoie |
| H3 | Voulez-vous un historique de ce qui a été fait ? | non ; oui, un journal séparé lu à la demande | non | fichier séparé, à la demande ; jamais le maître ni le suivi |
| H4 | À quelle fréquence relire les consignes ? | chaque mois ; chaque trimestre ; après chaque série de corrections | chaque mois | commentaire final du maître ; prochaine revue : tâche datée du suivi, citée par « Entretien de ce fichier » (aucune consigne ne déclenche une action à une date) |
| H5 | Qui est propriétaire des consignes ? (si le partage n'est pas « moi seul ») | vous ; une personne désignée (la citer) | vous | commentaire final du maître |

Cowork ou claude.ai : H4 et H5 vont dans la ligne « Rôle » de `modele-instructions-projet.md` et au récapitulatif de l'étape 7. Projet claude.ai : la mise à jour d'un fichier de connaissance par Claude n'est pas documentée (`mecanismes.md` §12) ; H2 vaut alors par défaut « vous seul » : Claude rédige la nouvelle version, que l'utilisateur recharge. Seuil d'archivage du suivi : 100 lignes ou 15 Ko par défaut, annoncé dans le résumé, ajustable.

Résumé à valider :
```text
H. Suivi : [fichier ou outil], tenu par [qui], archivé au-delà de [seuil] vers [fichier] ; historique : [oui ou non, où].
Revue : [fréquence], prochaine revue datée dans le suivi ; propriétaire : [nom ou rôle].
Destination : suivi + maître (« Avant d'agir », « Entretien de ce fichier ») ; à confirmer : [liste].
```

## Version minimale (A, C, F)

Le choix se fait à la validation de la restitution (étape 1, `SKILL.md`) ; recommander la minimale sous 30 minutes disponibles. Sans choix exprimé : minimale si l'utilisateur a dit disposer de moins de 30 minutes, même avec une demande d'arborescence ; sinon complète si l'arborescence est demandée, minimale sinon ; l'annoncer.

- Premier message : A1, A3 et C1, détectés à l'étape 1, en une seule confirmation (« Je retiens : [nature de l'espace], [productions] ; ces fichiers font foi : [liste détectée]. À corriger ? », `SKILL.md`, règle 4) ; une réponse non détectée devient une question à part ; puis C3.
- Second message : les mots des réglages (« Conduite de l'entretien »), puis validation du résumé A, C4 (avec, si un fichier de secrets est dans l'espace, la proposition que l'utilisateur le sorte lui-même), F1 et F2 ; les options de F2 nomment les outils d'envoi relevés à l'étape 1 ou à la dernière reprise, serveurs pas encore connectés compris, et ce que leur deny retire (bloc F, paragraphe « Interdit d'envoi ou de sortie de texte ») ; ces outils prennent la place de l'option « un outil de connecteur », en une seule option s'il le faut (« bloquer [outils] : chacun disparaît de ma liste pour toutes les tâches ; bloquer d'avance [services pas encore connectés] : effet à vérifier après leur connexion »), la réponse libre servant à en garder un ; les outils qui transmettent seulement à l'utilisateur lui-même restent à part (bloc F). Un interdit d'envoi exprimé hors de F2 se propose au troisième message, en question à part ; la validation du résumé F passe alors du troisième message au suivant.
- Troisième message : validation du résumé C, puis validation du résumé F (deux questions) ; F4, si l'étape 1 a trouvé des autorisations larges ; D1 et D2, si l'arborescence est demandée au cadrage. D4 prend alors sa valeur par défaut (un dossier d'archives unique, créé au premier document), annoncée dans le résumé D, validé avec le plan. Jamais plus de quatre questions par message : reporter au message suivant ce qui dépasse.
- Les autres questions des blocs A, C et F prennent leur valeur par défaut, annoncée dans le résumé du bloc.
- Le plan de l'étape 3 se réduit au maître (ouverture, « Où trouver quoi », « Demander mon accord avant de », « Interdits », « Classement et nommage » si D1 et D2 ont été posés, et « Commandes et pièges » si une commande qui exécute du code du dépôt est gardée en « risque accepté », bloc F), plus « Entretien de ce fichier » réduit à la ligne « Relancer `/architecte-consignes` en mode audit pour revoir ces consignes ; une règle devenue fausse est supprimée. » (Cowork ou claude.ai : `modele-instructions-projet.md`), et aux réglages de C4, F1 (`ask`), F2, F4, de l'interdit d'envoi (deny des outils d'envoi acceptés, serveurs pas encore connectés compris, et règles sur les commandes réseau) et de l'outil qui lance des commandes hors de Bash et PowerShell (bloc F). Il garde aussi la section qui porte une demande explicite de la demande initiale (le ton envers les clients : « Documents destinés à des tiers », par exemple). Un registre ou une langue de réponse exprimés dans la demande initiale ou au cadrage s'écrivent en une ligne dans « Façon de travailler avec moi ». Partage en équipe, git ou synchronisé : cette ligne va dans les préférences personnelles prévues au cadrage (`~/.claude/CLAUDE.md`, ou `CLAUDE.local.md` exclu du partage), annoncées au plan. Retirer du maître les autres sections qui dépendent des blocs non posés. Avec le plan, poser en une question celle de `controle-qualite.md` C18 : « Des tâches programmées ou des automatisations travaillent-elles dans cet espace ? ».
- En refonte, les consignes existantes des blocs non posés gardent la destination que leur donne `routage.md` : elles viennent d'un fichier lu (`SKILL.md`, règle 1). Seules les sections de modèle sans contenu sont retirées. Avec plusieurs agents, le maître réduit est `AGENTS.md` et son CLAUDE.md voisin (`routage.md` section 6).
- Noter les blocs non posés « à confirmer : bloc non traité » dans le brouillon, sans valeur par défaut, sauf la langue des fichiers (B2), annoncée dans le plan, et la fréquence de revue (H4), proposée « chaque mois » et notée « à confirmer ». Ce que la demande initiale tranche déjà s'écrit à sa destination. Proposer de reprendre les blocs non posés plus tard.

## Questions à ne jamais poser

- Ce que la demande initiale, les fichiers ou le cadrage disent déjà (dossiers, langages, dépendances, formats, commandes visibles) : proposer la réponse détectée à confirmer. Avant chaque question, vérifier que la réponse manque et changerait une consigne.
- Les préférences invérifiables (« Voulez-vous des réponses claires et rigoureuses ? ») : tout le monde répond oui et rien ne change. Si l'utilisateur en exprime une, la reformuler (section suivante).
- Les informations sensibles elles-mêmes (mots de passe, clés, coordonnées bancaires, numéros d'identité ou fiscaux, santé, données de tiers) : demander seulement où elles sont rangées, pour les bloquer (C4) ou les réserver à une procédure (C5). Une valeur donnée par l'utilisateur ne s'écrit ni dans les consignes ni dans le brouillon ; lui indiquer de la ranger ailleurs.
- L'état du moment (« Sur quoi travaillez-vous cette semaine ? ») : il relève du suivi, pas des consignes.
- Les choix de mécanisme (« import ou pointeur ? », « skill ou règle ? », « quel fichier de préférences ? ») : Claude les propose et les explique à l'étape 3 ; l'utilisateur décide sur le plan.

## Reformuler une réponse vague

Demander un exemple réel où le résultat a déçu et en tirer une action observable (verbe, objet, seuil ou emplacement) ; à défaut d'exemple, proposer directement une formulation vérifiable. Faire valider la phrase. Si aucune action observable n'en sort, ne rien écrire.

| Réponse vague | Consigne vérifiable |
|---|---|
| « Soyez clair. » | « Commencer chaque réponse par le résultat en une phrase, puis cinq puces au plus. » |
| « Rangez bien les fichiers. » | « Enregistrer tout nouveau document dans le dossier de son sujet, nommé `AAAA-MM-JJ-objet` ; en cas de doute, proposer l'emplacement avant d'écrire. » |
| « Faites attention aux chiffres. » | « Recopier chaque montant depuis [source qui fait foi] et citer cette source ; écrire “à confirmer” pour tout montant absent. » |
