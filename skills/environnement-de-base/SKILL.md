---
name: environnement-de-base
description: "Utiliser pour préparer l'environnement de base d'un dossier de travail avec Claude : Obsidian installé, avec ce dossier ouvert comme coffre et une note d'accueil ; dossiers récupérés depuis Google Drive ou OneDrive par copie, jamais par déplacement ; Gmail ou Outlook connecté en brouillons seulement ; Google Drive ou OneDrive connecté pour chercher et lire ; Claude in Chrome réglé prudemment. À lancer à la demande (commande /architecte-consignes:environnement-de-base) ou appelé par le skill architecte-consignes, entre ses étapes 5 et 6. Seulement dans une session locale de Claude Code (onglet Code de l'application de bureau, ou terminal) : pas dans Cowork ni sur claude.ai. Ne pas utiliser pour écrire un CLAUDE.md (skill architecte-consignes) ni pour une simple question sur ces outils."
---

# Environnement de base

Ce skill prépare, avec le participant, l'environnement de base d'un dossier de travail : le dossier lui-même, Obsidian et sa note d'accueil, la copie de dossiers depuis Google Drive ou OneDrive, la messagerie en brouillons seulement, le stockage en ligne connecté pour chercher et lire, et Claude in Chrome. Il agit sur l'ordinateur et touche à des comptes en ligne : il ne fonctionne que dans une session locale de Claude Code (onglet Code de l'application de bureau, ou terminal). Lire ce fichier en entier à l'appel, puis le relire avec le brouillon après une interruption ou une compaction (E8). Kit Architecte consignes, v1.2.0.

Dans Cowork (commandes par `mcp__workspace__bash`) ou sur claude.ai (aucun accès aux fichiers), dire seulement : « Ce skill installe et règle des outils sur votre ordinateur : relancez-le dans l'onglet Code de l'application de bureau Claude, ou dans un terminal. » Puis s'arrêter.

Faits sur les réglages, les connecteurs, Obsidian, Drive, OneDrive et Chrome : [../architecte-consignes/references/mecanismes.md](../architecte-consignes/references/mecanismes.md) §16, et §6 pour les permissions. Ce qui n'y figure pas se dit « non documenté, à vérifier dans l'application ».

## Lancement seul ou depuis architecte-consignes

- Seul : `/architecte-consignes:environnement-de-base` (plugin), `/environnement-de-base` (skill copié à la main dans `~/.claude/skills/`, ou dans le `.claude/skills/` du dossier), ou par son nom avec l'outil Skill. Avant ou après `architecte-consignes`.
- Depuis `architecte-consignes` : il charge ce skill entre son étape 5 (Rédiger) et son étape 6 (Contrôler et tester), si son brouillon `_entretien-claude-md.md` porte « Environnement de base : demandé » (choix fait à son étape 1). Dans ce cas :
  - reprendre de ce brouillon le cadrage, la racine, le plan validé, les chemins de l'arborescence et les éléments choisis s'ils y sont notés (sinon, les demander par la question 1 de l'étape 0), sans reposer ce qui y figure ;
  - son étape 5 a déjà écrit `.claude/settings.json` et le CLAUDE.md maître : l'étape 9 y fusionne les règles et les lignes, sans rien retirer ;
  - le dossier de travail ne change pas pendant l'appel (étape 3) ;
  - dès l'accord sur le plan (étape 2), tenir à jour dans ce brouillon, sous « Étape en cours », la ligne « Environnement de base : en cours (étape n) », puis « Environnement de base : fait » après les tests (étape 11). Après une interruption, `/architecte-consignes`, puis « reprendre », suffit : sa section « Entre l'étape 5 et l'étape 6 » recharge ce skill, qui reprend son propre brouillon (E8) ;
  - les tests de l'étape 10 rejoignent la recette de son étape 6, dans la même nouvelle session (geste : étape 10) ;
  - à la fin de l'étape 11, revenir à son étape 6.

## Règles de conduite, valables à chaque étape

- **E1. Lecture seule jusqu'au plan.** Rester en lecture seule jusqu'à l'accord sur le plan d'installation (étape 2). Le brouillon `_entretien-environnement.md` ne se crée qu'à cet accord : un participant qui change de dossier à l'étape 1 n'a donc rien d'écrit dans l'ancien. Si le plan prévoit un nouveau dossier de travail (étape 3), créer d'abord ce dossier, puis le brouillon dedans.
- **E2. Partage des gestes.** Claude prépare, vérifie et exécute dans le périmètre accepté : avec une demande d'autorisation pour chaque commande qui modifie, en mode manuel ; sinon, avec l'accord dans la conversation. Le participant fait lui-même :
  - choisir les dossiers, la destination et le compte ;
  - se connecter, saisir un mot de passe ou un code, accepter des conditions ;
  - les clics dans les applications (Obsidian, Chrome, page Connecteurs de claude.ai) ;
  - répondre à chaque demande d'autorisation : « Oui » pour cette fois, jamais « Oui, ne plus demander » sauf décision consciente. Pour une commande, ce choix écrit une autorisation permanente (`allow`) dans `.claude/settings.local.json` ; pour une modification de fichier, il vaut jusqu'à la fin de la session (mecanismes.md §6 ; libellé à l'écran : à vérifier, E7).

  Claude ne fait jamais ces gestes à la place du participant, même à sa demande : il ne saisit ni mot de passe ni code et n'accepte aucune condition, par aucun moyen (option, réponse envoyée à une invite, clic par Claude in Chrome). Un mot de passe ou un code collé dans la conversation n'est ni utilisé ni recopié, brouillon compris : dire au participant de le saisir lui-même et, s'il l'a collé, de le changer. Claude n'ajoute jamais `--accept-package-agreements`, `--accept-source-agreements` ni `sudo`, n'installe pas Homebrew et ne touche pas aux réglages de sécurité du système (Accès complet au disque, contrôle de compte).

  Recommander le mode manuel (onglet Code : sélecteur sous la zone de saisie ; terminal : `claude --permission-mode default`). Dans les autres modes, des actions passent sans demande d'autorisation (mecanismes.md §6) : en Accept edits, les modifications de fichiers et des commandes comme `mkdir`, `cp`, `mv` et, par PowerShell, `Remove-Item`, dans les dossiers de travail ; en auto, ce que le classifieur accepte ; en Bypass permissions, tout ce qu'aucune règle ask ou deny ne vise. Hors mode manuel, ou si le mode n'est pas connu, montrer chaque commande qui modifie en entier et obtenir l'accord dans la conversation avant de la lancer.
- **E3. Copier, jamais déplacer.** Google Drive et OneDrive : copier, jamais déplacer ni supprimer. La source reste en lecture seule : aucune commande n'y écrit, n'y renomme, n'y déplace ni n'y supprime, quel que soit l'outil ou l'alias (`Move-Item`, `mv`, `move`, `Rename-Item`, `ren`, `Remove-Item`, `rm`, `del`, `erase`, `rd`, `rmdir`, `cmd /c …`, `robocopy /MOV /MOVE /MIR /PURGE`). Ces commandes sont aussi interdites sur une destination existante. Ne jamais écraser un fichier de destination sans accord.
- **E4. Aucun envoi, même pour un test.** On teste par la liste d'outils, par un brouillon sans destinataire et par une page neutre (`https://example.com`).
- **E5. Les trois mots du kit, une limite par réglage.** Avant le plan, dire une fois (appelé par `architecte-consignes`, c'est déjà fait) :
  - « Bloqué » : Claude Code refuse l'action, même si vous la demandez ; vous la faites alors vous-même.
  - « Confirmation » : Claude Code vous affiche une demande d'autorisation avant chaque action de ce type ; vous acceptez ou vous refusez.
  - « Consigne » : Claude s'engage à la suivre, sans garantie.

  Chaque réglage se dit avec un de ces mots et sa limite. Aucun réglage, ni aucun « Blocked » réglé sur claude.ai, ne se présente comme une garantie. Une mention au CLAUDE.md seulement pour une règle posée, qui couvre ce qu'elle annonce : table « Mentions au maître » de [../architecte-consignes/SKILL.md](../architecte-consignes/SKILL.md), seul lieu de ces mentions.
- **E6. Nouvelle session.** Ce point est le seul lieu du geste d'ouverture et de la commande de recette ; les références y renvoient. Avant de demander au participant d'ouvrir une session :
  - noter l'avancement au brouillon (« Étape en cours ») ;
  - lui donner le geste exact : dans l'onglet Code, nouvelle session, même dossier, mode Manual (sélecteur sous la zone de saisie) ; en terminal, `cd "<chemin du dossier>"`, puis `claude --permission-mode default`, ou `claude --chrome --permission-mode default` si les tests comprennent Chrome ;
  - à l'étape 10, lui rappeler la question de la pièce, à poser en premier message, avant toute autre demande (étape 10) ;
  - lui donner la phrase exacte à taper ensuite : `/architecte-consignes:environnement-de-base`, puis « reprendre » (skill copié à la main : `/environnement-de-base`). Appelé par `architecte-consignes`, cette phrase se tape dans la session de sa recette, après la question de la pièce et les questions de recette (étape 10) ;
  - dans un autre dossier (étape 3), lui faire taper d'abord `/archi` : `architecte-consignes:environnement-de-base` doit être proposé ; sinon, le plugin n'y est pas activé (étape 3).

  Viser une seule nouvelle session, à l'étape 10, pour tous les tests. Seule exception : un changement de dossier de travail (étape 3, skill lancé seul).
- **E7. Langue et registre.** Langue et registre de l'utilisateur, vouvoiement par défaut. Les libellés d'interface s'écrivent en anglais tels que les sources les citent, suivis au besoin de « (libellé français : non documenté, à vérifier à l'écran) ».
- **E8. Brouillon.** `_entretien-environnement.md` à la racine. Titres : Cadrage ; Étape en cours ; Relevé de l'étape 1 ; Plan validé (oui ou non, avec le tableau) ; Obsidian (racine de la session, coffre retenu, chemin de l'accueil) ; Copies faites (lots, comptes, empreintes, journal) ; Réglages posés ; Tests ; À confirmer ; Statut (en cours ou terminé). Il ne contient ni secret ni donnée personnelle de tiers. S'il existe au lancement et porte « en cours », proposer la reprise ; s'il porte « terminé », proposer un nouveau passage. S'il porte « en cours (tests à faire à l'étape 6 de architecte-consignes) », reprendre directement à l'étape 10, dans la session ouverte, sans en faire ouvrir une autre, même si `_entretien-claude-md.md` manque ou porte « terminé » ; puis finir l'étape 11 (cas « appelé », session de recette). À la reprise, relire ce fichier et le brouillon, refaire en lecture seule le relevé de l'étape 1, puis présenter les écarts avant de continuer.
- **E9. Fichiers d'essai.** Un fichier ou un dossier créé pour un test (note d'essai, témoin, fichier dans `.obsidian`, dossier factice) porte un nom propre à la séance, avec la date et l'heure (`AAAAMMJJ-HHMM`). Vérifier qu'il n'existe pas juste avant de le créer ; s'il existe, changer l'heure. Dès la création, noter son chemin au brouillon, sous « Tests ». Au nettoyage, après une reprise comprise, ne proposer de supprimer que les éléments notés ainsi, et seulement si leur contenu est encore celui de l'essai. Un élément d'origine incertaine ne se supprime pas : le dire, et le noter à « À confirmer ». Le participant supprime lui-même (E3).

## Déroulé

Utiliser l'outil AskUserQuestion s'il est disponible ; sinon, des questions numérotées en texte. Au plus quatre questions par message, et quatre options par question (mecanismes.md §13).

### Étape 0. Cadrer

Annoncer en deux phrases, dans le registre de l'utilisateur : « Je vais préparer avec vous l'environnement de base de ce dossier : Obsidian, vos dossiers en ligne, votre messagerie, votre stockage en ligne et Chrome, selon vos choix. Je ne modifie rien avant votre accord sur le plan d'installation ; c'est une règle que je suis, pas un verrou de l'outil. » Ajouter le dossier détecté : « Je travaille dans [dossier] ; dites-le si ce n'est pas le bon. »

- Détecter le système (Windows ou macOS) d'après la session, sans question. Autre système : le dire ; ce skill ne décrit que Windows et macOS.
- Chercher `_entretien-environnement.md` (E8) et `_entretien-claude-md.md` : un brouillon « en cours » de `architecte-consignes` qui porte « Environnement de base : demandé » signale un appel par ce skill.
- Poser, en un seul message, les questions qui restent (appelé par `architecte-consignes`, reprendre ce que son brouillon dit déjà) :
  1. éléments voulus, à choix multiple : dossiers à récupérer depuis Google Drive ou OneDrive ; Gmail ou Outlook en brouillons seulement ; Google Drive ou OneDrive connecté pour chercher et lire ; Claude in Chrome. Obsidian est prévu par défaut, et l'intitulé le dit : « Obsidian est prévu (recommandé) : répondez « sans Obsidian » dans la réponse libre si vous n'en voulez pas. » ;
  2. compte personnel ou professionnel ;
  3. en entreprise, copie locale et connecteurs : une seule question, à quatre options, « Compte personnel : sans objet » ; « Copie locale et connecteurs permis » ; « L'un des deux n'est pas permis (précisez lequel) » ; « Je ne sais pas » (vaut « à confirmer ») ;
  4. services, à choix multiple : Gmail ; Outlook ; Google Drive ; OneDrive. L'intitulé dit : « Seulement si vous avez choisi des dossiers à récupérer, la messagerie ou le stockage en ligne ; sinon, répondez « aucun » dans la réponse libre. »
- Dire les coûts au moment du choix : Obsidian est gratuit, son service Sync est payant et facultatif ; l'onglet Code et Claude in Chrome demandent une offre payante (mecanismes.md §15 ; references/chrome.md).

### Étape 1. Relever, en lecture seule

Relever, sans rien modifier et sans appeler aucun outil de connecteur :

- **Système et racine.** Windows : `(Get-Location).Path` ; macOS : `pwd`. Indice de dossier synchronisé : chemin qui contient `OneDrive`, `Google Drive`, `GoogleDrive`, `My Drive`, `Mon Drive`, `CloudStorage`, `iCloud` ou `Mobile Documents`, ou lecteur `G:` sous Windows. C'est un indice, jamais une preuve : demander au participant.
- **Obsidian.** Installé ou non (commandes déduites, non documentées par Obsidian : references/obsidian.md, pas 3) : Windows, `winget list --id Obsidian.Obsidian -e --source winget` (si winget manque ou demande d'accepter des conditions, ne pas répondre (E2) et demander au participant s'il voit Obsidian dans le menu Démarrer) ; macOS, `ls -d /Applications/Obsidian.app ~/Applications/Obsidian.app`. Un dossier `.obsidian/` dans la racine, dans un dossier parent ou dans un sous-dossier signale un coffre existant (recherches « ici ou au-dessus » et « en dessous », references/obsidian.md, pas 3).
- **Outils de connecteur présents**, noms exacts recopiés depuis sa propre liste d'outils : messagerie (`send_message`, `reply`, `forward`, `create_draft`, `update_draft`, `outlook_…`, `teams_…`), Microsoft 365 (`sharepoint_…`), Drive (`trash_file`, `share_file`, `request_access`, `update_file`, `create_file`, `copy_file`, `search_files`), `mcp__claude-in-chrome__*`. Noter aussi si `mcp__ccd_session_mgmt__send_message` (messagerie entre les sessions de l'utilisateur) est présent : l'étape 10 le vérifie.
- **Réglages.** `.claude/settings.json` : règles existantes, blocage entier d'un serveur de messagerie ou de stockage (`mcp__<serveur>__*` ou `mcp__<serveur>`), et tout deny sur des outils Chrome (`mcp__claude-in-chrome__*`) ou de stockage. `.claude/settings.local.json` : règles `allow` qui visent ces outils. De ces fichiers, ne relever que la clé `permissions` et le nom des autres clés, jamais leurs valeurs : une clé `env` ou `apiKeyHelper` peut porter un secret, et ce qui s'affiche reste dans la transcription, enregistrée en clair sur l'ordinateur (references/stockage.md, partie C, pas 5).
  - Windows : `$s = Get-Content -Raw -LiteralPath '<fichier>' | ConvertFrom-Json; $s.permissions | ConvertTo-Json -Depth 10; $s.enabledPlugins | ConvertTo-Json; $s.PSObject.Properties.Name -join ', '`
  - macOS (déduit, non testé) : `plutil -extract permissions json -o - '<fichier>'`, `plutil -extract enabledPlugins json -o - '<fichier>'`, puis `grep -cE '"(env|apiKeyHelper)"' '<fichier>'`, qui ne donne qu'un nombre.
  - `enabledPlugins` qui nomme `architecte-consignes@…` dans l'un de ces deux fichiers : le plugin est activé pour ce dossier (portée projet ou locale, mecanismes.md §16) ; il peut manquer dans un autre dossier (étape 3).
  - Une clé `env`, `apiKeyHelper` ou dont le nom évoque un secret se signale par son nom, sans sa valeur (règle 3 de `architecte-consignes`).
- **Fichiers.** `CLAUDE.md`, `Accueil.md`, `_entretien-claude-md.md` (plan validé, chemins de l'arborescence), `_entretien-environnement.md`.

Restituer en dix lignes au plus : ce qui est déjà en place, ce qui manque, et, s'il y en a un, l'indice de synchronisation sous forme de question (« Votre dossier semble synchronisé par [service] : est-ce le cas ? »). Le relevé ira au brouillon, sous « Relevé de l'étape 1 », dès sa création.

### Étape 2. Plan d'installation

Dire d'abord les trois mots (E5). Présenter un tableau, une ligne par action retenue, dans l'ordre des étapes 3 à 10 :

| Action | Qui la fait | Réglage posé et son effet | Test |
|---|---|---|---|
| [action] | Claude ou vous | [règle, en mots simples : bloqué, confirmation ou consigne, avec sa limite] | [test de l'étape 10] |

- Si `.claude/settings.json` bloque déjà tout le serveur de messagerie, ne pas le débloquer sans accord explicite : le choix est entre garder le blocage total et passer en brouillons seulement, en disant quels outils redeviennent disponibles (references/messagerie.md, « Réglages », dernier point). De même, un deny existant sur Chrome ou le stockage se garde, ou se remplace par les règles du volet, au choix du participant.
- Un connecteur de messagerie ou de stockage, ou Claude in Chrome, relevé à l'étape 1 mais non choisi : le signaler dans le plan, avec ses outils d'envoi, de suppression, de déplacement et de partage (Chrome : règles de l'étape 8), et proposer quand même leurs deny ; le participant décide.
- En entreprise, si la copie locale n'est pas permise ou si un connecteur n'est pas approuvé, garder un parcours qui marche avec un dossier local, et noter le reste « à confirmer ».
- Obtenir l'accord, puis créer le brouillon (E8) avec « Plan validé : oui », le tableau et le relevé de l'étape 1. Si le plan prévoit un nouveau dossier de travail, le brouillon se crée dans ce dossier, à l'étape 3 (E1). Ajuster et présenter de nouveau autant que nécessaire.
- Appelé par `architecte-consignes`, dire aussi : « Si la séance s'interrompt, ouvrez une session dans ce dossier et tapez /architecte-consignes, puis « reprendre ». »

### Étape 3. Dossier de travail

Seulement si le skill est lancé seul, ou si l'indice de synchronisation est confirmé. Suivre [references/stockage.md](references/stockage.md), partie A.

- Appelé par `architecte-consignes` : ne pas changer de dossier pendant l'appel, car le CLAUDE.md maître, `.claude/settings.json` et son brouillon resteraient dans le dossier actuel. Le passage à un dossier local se décide à l'étape 1 de `architecte-consignes`, avant toute autre écriture que son brouillon d'entretien, créé à la fin de son étape 0. Ici, suivre le pas 3 de la partie A (message, note « À confirmer »), puis son pas 7 (dossier gardé, disponible hors connexion), sans passage au mode miroir de Google Drive, qui change le chemin du dossier.
- Lancé seul : suivre le pas 3 de la partie A. Le participant choisit un dossier local (pas 4 à 6) ou garde le dossier actuel (pas 7 s'il est synchronisé) ; Claude crée le dossier local, après accord.
- Si le dossier change :
  - si `.claude/skills/environnement-de-base/` existe dans le dossier actuel, les skills y sont copiés pour ce seul dossier : ils manqueront au nouveau, et la phrase de E6 n'y marchera pas. Le dire, et proposer de copier `architecte-consignes` et `environnement-de-base` dans `~/.claude/skills/` ou dans le `.claude/skills/` du nouveau dossier, après accord dans la conversation (E2), sans rien écraser ;
  - plugin activé pour ce seul dossier (relevé de l'étape 1, `enabledPlugins`) : il manquera au nouveau. Dire : « Avant de changer de dossier, installez le plugin pour votre compte utilisateur : bouton + à côté de la zone de saisie, Add plugins (ou Plugins, puis Manage plugins), et la portée « your user account » ; en terminal, `claude plugin install architecte-consignes@architecte-consignes`, dont la portée par défaut est l'utilisateur. » Ne jamais copier les réglages `.claude/` de l'ancien dossier pour l'activer ;
  - dans tous les cas, la nouvelle session commence par la vérification de E6 (`/archi`) : si `architecte-consignes:environnement-de-base` n'est pas proposé, installer le plugin pour le compte, comme ci-dessus, puis ouvrir encore une nouvelle session dans le nouveau dossier ;
  - y créer le brouillon (E1), ou l'y copier sans écraser s'il existe déjà (partie A, pas 5), puis faire ouvrir une nouvelle session dans ce dossier (E6) ; la suite se fait dans cette session.

### Étape 4. Obsidian

Suivre [references/obsidian.md](references/obsidian.md) : vérifier, installer après accord, ouvrir le gestionnaire de coffres, faire cliquer le participant (« Open folder as vault »), guider ses réglages, créer la note d'essai (E9).

- Un seul coffre. Un coffre existant au-dessus ou en dessous de la racine se signale, et le participant choisit (references/obsidian.md, pas 3). Noter au brouillon la racine de la session et le coffre retenu, qui peuvent différer. L'accueil s'écrit là où ce coffre le montre (references/obsidian.md, pas 8) ; son chemin se note au brouillon, sous « Obsidian ».

- Note d'accueil, d'après [modeles/modele-accueil.md](modeles/modele-accueil.md) : créer `Accueil.md` à l'emplacement noté (racine de la session, ou racine d'un coffre de sous-dossier gardé), ou le compléter s'il existe, en montrant l'ajout et après accord.
- Elle liste les dossiers validés au plan (brouillon de `architecte-consignes`), chacun avec son rôle et son chemin relatif, écrit en texte. Lancé seul, sans plan validé : les dossiers de premier niveau, validés par le participant. Les lots copiés s'y ajoutent à la fin de l'étape 5.
- Règle retenue pour l'étape 9, seulement si le coffre retenu est la racine de la session : confirmation `Edit(./.obsidian/**)`. Coffre au-dessus ou de sous-dossier : aucune règle sur `.obsidian`, la ligne reste une consigne et les points 1 à 5 du test sont sautés (references/obsidian.md, pas 3).

### Étape 5. Récupérer des dossiers

Suivre [references/stockage.md](references/stockage.md), partie B. E3 s'applique à chaque commande.

- Avant la copie : confirmer la vraie racine de la source et la destination, distincte de la source et non imbriquée ; vérifier que les fichiers sont disponibles hors connexion, que l'espace libre suffit et, en entreprise, que la copie locale est permise.
- Repérer les fichiers Google natifs (`.gdoc`, `.gsheet`, `.gslides`) : ce sont des liens ; les signaler, le participant les exporte depuis Drive sur le web. Ne suivre aucun raccourci sans choix du participant.
- Exclure, avant toute empreinte (elle lit le contenu) et toute copie, les fichiers de secrets ou sensibles écartés avec le participant, et les réglages, extensions et consignes de la source (`.claude/`, `.obsidian/`, dont `.obsidian/plugins/`, `CLAUDE.md`, `CLAUDE.local.md`, `AGENTS.md`, autres fichiers de consignes) : jamais copiés sans son choix. Dire : « Un CLAUDE.md copié ici deviendrait une consigne que je suivrais. » Repérage, liste et commandes : partie B, pas 4 et 6. Noter chaque exclusion au brouillon : l'élément exclu manque à la copie.
- Copier par lots, avec accord sur chaque lot, par une commande qui n'écrase jamais et se relance (commandes exactes : partie B). Le journal va hors de la source. La destination de chaque lot est un dossier neuf, noté au brouillon avant la copie : un dossier qui existait déjà ne reçoit rien (partie B, pas 3).
- Vérifier chaque lot par empreinte SHA-256, fichier par fichier, par chemin relatif, sans les exclus. Le compte, la taille et un code robocopy inférieur à 8 ne suffisent pas : seule la comparaison des empreintes du lot autorisé établit que la copie est complète (partie B, pas 6 et 7 ; commandes : [references/empreintes.md](references/empreintes.md)). Toute erreur de lecture arrête ce contrôle, et les listes de référence ne s'enregistrent qu'après un contrôle sans écart : sinon, le lot reste « non vérifié », jamais « empreintes identiques ». Un fichier « différent » ou « manquant » se recopie, avec accord, seulement dans la destination. Un fichier « en plus » ne se supprime pas : il s'écarte de la comparaison (partie B, pas 8). L'original reste en place.
- Noter chaque lot au brouillon, sous « Copies faites ».
- Après le dernier lot validé, si l'accueil existe (étape 4, chemin noté au brouillon) : y ajouter une ligne par lot copié qui n'y figure pas encore (nom, rôle validé ou « à confirmer », chemin relatif), d'après [modeles/modele-accueil.md](modeles/modele-accueil.md). Montrer l'ajout, puis l'écrire après accord. Sans cet ajout, le test de l'accueil (étape 10) ne prouverait rien.
- Règle retenue pour l'étape 9, en option (si le participant veut que Claude lise l'original) : deny `Edit(<chemin de l'original>/**)`, avec sa règle d'essai (partie B, pas 11, et son Test). La noter au brouillon dès l'accord.

### Étape 6. Messagerie en brouillons seulement

Suivre [references/messagerie.md](references/messagerie.md).

- Le participant connecte Gmail ou Outlook sur claude.ai et y règle les outils d'envoi sur « Blocked » (Gmail : envoi, réponse, transfert ; Outlook : envoi, transfert, envoi d'un brouillon, réponse automatique, règle de boîte, et Teams ; liste : references/messagerie.md, pas à pas, point 6). Claude guide, sans agir.
- Règles retenues pour l'étape 9 : un deny pour chaque outil d'envoi, sous trois formes (section « Réglages proposés »).
- Sans outil de brouillon pour ce compte, écrire le texte dans un fichier local et dire que le dépôt dans la boîte n'est pas disponible.
- Dans le navigateur (webmail ouvert par Claude in Chrome), l'envoi reste une consigne ; Cowork n'est pas couvert.
- Avec Microsoft 365, l'agenda arrive avec la messagerie. Créer un événement avec des invités ou répondre à une invitation peut prévenir d'autres personnes. Aucune règle du dossier ne vise l'agenda : réglage sur claude.ai, puis consigne (references/messagerie.md, pas à pas, point 7). Le dire au récapitulatif.

### Étape 7. Stockage en ligne connecté

Suivre [references/stockage.md](references/stockage.md), partie C.

- Le participant connecte Google Drive ou Microsoft 365 et règle ses outils sur claude.ai.
- Le connecteur sert à chercher et lire un document précis ; un dossier entier se récupère par copie (étape 5).
- Règles retenues pour l'étape 9 : deny sur la corbeille, la suppression, le déplacement, le renommage, la modification en ligne, le partage et la demande d'accès ; confirmation sur la création, la copie et le dépôt (détail : section « Réglages proposés »). Un outil de partage relevé à l'étape 1 sous un autre nom s'ajoute en deny, sous son nom exact.

### Étape 8. Claude in Chrome

Suivre [references/chrome.md](references/chrome.md).

- Le participant installe l'extension, s'y connecte, choisit les droits par site et active Chrome pour Claude : aucun réglage de projet ne peut l'activer.
- Tester dans un profil de démonstration, sur une page neutre.
- Règles retenues pour l'étape 9 : deny `mcp__claude-in-chrome__javascript_tool` ; confirmation sur `form_input`, `file_upload`, `upload_image` et `browser_batch` ; aucun outil Chrome en allow.
- Ne décrire que l'effet vérifié : le deny de `javascript_tool` ne bloque pas toute action dans le navigateur.

### Étape 9. Réglages et CLAUDE.md

- Fusionner dans `.claude/settings.json` les règles retenues de [modeles/modele-settings-environnement.json](modeles/modele-settings-environnement.json), plus les noms exacts relevés à l'étape 1, sans rien retirer sans accord. Garder les règles des éléments installés et des connecteurs relevés à l'étape 1 (étape 2), sauf refus du participant ; retirer les autres.
- Si le fichier existe, garder d'abord une copie `settings.ancien-AAAA-MM-JJ.json` hors de `.claude/` ; si ce nom existe déjà, ajouter `-2`, `-3`.
- Fichier qui porte une clé `env`, `apiKeyHelper` ou dont le nom évoque un secret (étape 1) : ne pas l'ouvrir avec l'outil de lecture, ni le modifier avec l'outil d'édition, qui exige cette lecture.
  - Faire la copie, la fusion et la relecture par un script, montré en entier avant d'être lancé, qui ne change que `permissions` et n'affiche aucune autre valeur. Windows : `ConvertTo-Json -Depth 20`, écriture en UTF-8 sans BOM ; macOS : déduit, non testé.
  - Dans la copie, les valeurs de ces clés deviennent « [retiré] », avec accord, comme pour toute copie `.ancien` (étape 5 de `architecte-consignes`) : aucun secret ne part dans le dossier de travail.
- S'il n'existe pas, créer `.claude/settings.json` avec la clé `$schema`.
- `.claude/` est un chemin protégé, pour la création comme pour la fusion : en mode manuel ou Accept edits, Claude Code demande l'autorisation ; en mode auto, le classifieur décide ; en Bypass permissions, l'écriture passe sans demande (mecanismes.md §6 ; references/obsidian.md, « Limites et points à confirmer »). Montrer donc le contenu à écrire et obtenir l'accord dans la conversation avant l'écriture (E2) ; à la demande d'autorisation, ne pas choisir l'option qui autorise `.claude` pour toute la session.
- Relire le fichier écrit : JSON valide, aucune règle existante retirée. Noter les règles posées au brouillon, sous « Réglages posés ».
- Montrer au participant les lignes à ajouter au `CLAUDE.md`, avec les mentions de la table « Mentions au maître » ([../architecte-consignes/SKILL.md](../architecte-consignes/SKILL.md)), et écrire après son accord les consignes sans mention. Toute ligne avec mention de ce skill (messagerie, stockage, Chrome, `.obsidian`) attend son test : elle s'écrit à l'étape 10, après ce test et l'accord ; la noter au brouillon, sous « Tests ». Une mention de blocage demande en plus que l'outil ait été vu sous son nom complet dans la liste avant la règle. Un outil déjà absent (retiré par l'organisation, ou réglé sur « Blocked » sur claude.ai) : ligne sans mention, capacité observée notée au brouillon, effet de la règle du dossier « à confirmer ». Ne jamais retirer une protection existante pour tester. Sans `CLAUDE.md`, les garder pour le récapitulatif et les noter au brouillon, sous « À confirmer », après la ligne « CLAUDE.md maître à créer avec /architecte-consignes ; lignes à y reprendre : ». Chaque ligne y figure avec sa mention et l'état de son test (à faire, réussi, échoué), mis à jour à l'étape 10 : sans le brouillon, ces lignes seraient perdues pour `architecte-consignes`, qui n'invente rien.
- Appelé par `architecte-consignes` : son étape 5 a déjà écrit les réglages ; fusionner de même. Au maître, la ligne de messagerie en brouillons seulement remplace la mention de ce service dans la ligne « Outils d'envoi vers l'extérieur bloqués » déjà écrite, avec l'accord du participant ; rien d'autre ne se retire.

### Étape 10. Tester dans une nouvelle session

Avant de faire ouvrir la session :
- appliquer les préalables des sections « Test » des références retenues (chrome.md, point 1 : redémarrer Chrome puis l'application si les outils Chrome manquaient) ;
- préparer avec le participant la question de la pièce, si l'accueil existe (chemin noté au brouillon) et que le dossier contient des pièces. Il choisit une pièce réelle, de préférence une pièce qui existe en plusieurs versions (un devis et la version qui fait foi, par exemple), et la formule sans chemin, numéro ni montant : « Où est la version qui fait foi du devis [objet] ? Donnez le fichier, puis le chemin suivi pour le trouver. » Sans `CLAUDE.md` qui renvoie à l'accueil, la question ajoute « en partant de [chemin de l'accueil noté au brouillon, sous « Obsidian »] » (`Accueil.md`, ou `<sous-dossier>/Accueil.md`). La pièce ne s'écrit nulle part, ni au brouillon ni dans un fichier : la nouvelle session pourrait la lire. Dossier encore vide : test reporté, « à confirmer ».

Faire ouvrir une nouvelle session (E6). Dans cette session :
1. (U) Premier message, avant la phrase de reprise et toute autre demande : la question de la pièce. (U) contrôle la réponse : bonne pièce, bonne version, et un chemin qui part de l'accueil. Posée avant toute lecture du brouillon, elle montre si un nouvel assistant se repère par l'accueil.
2. (U) Puis la phrase de reprise (E6). (C) reprend le brouillon (E8) et note sous « Tests » le résultat du point 1, que le participant lui donne.
3. (C) Suivre pour chaque élément installé la section « Test » de sa référence (obsidian.md, « Tests à l'étape 10 » ; stockage.md ; messagerie.md ; chrome.md), puis noter chaque résultat au brouillon, sous « Tests ». En résumé :

- liste d'outils : outils d'envoi absents (Gmail : envoi, réponse, transfert ; Outlook : ceux du tableau de messagerie.md) ; `create_draft` (Gmail) ou `outlook_create_draft` (Outlook) présent ; `mcp__ccd_session_mgmt__send_message` présent s'il existait avant. Mêmes contrôles pour le stockage (corbeille, partage, déplacement absents ; recherche présente) et pour Chrome (`javascript_tool` absent). Si l'outil de brouillon ou de recherche manque aussi, le connecteur n'est pas chargé : l'absence des autres ne prouve rien ;
- un brouillon réel, sans destinataire si le connecteur l'accepte (Outlook : à vérifier, references/messagerie.md, Test, point 6), objet « Essai Claude — à supprimer », que le participant vérifie puis supprime lui-même ;
- une recherche Drive ou OneDrive d'un document précis ;
- Chrome : ouvrir `https://example.com` dans un nouvel onglet du groupe de Claude ;
- Obsidian : la note d'essai est visible dans le coffre retenu (la recherche de la pièce est faite au point 1). Si la confirmation `Edit(./.obsidian/**)` est posée (coffre retenu à la racine de la session) : test en mode Accept edits, avec un fichier témoin (E9), par l'outil Write et jamais par une commande (en mode manuel, toute écriture demande une autorisation : le test ne prouverait rien) ; la demande d'autorisation doit s'afficher pour le fichier d'essai de `.obsidian` (E9), le participant la refuse, puis revient au mode manuel (protocole : [references/obsidian.md](references/obsidian.md), « Tests à l'étape 10 »). Ce test passe avant le test du blocage `Edit` sur l'original et avant l'ajout de l'original à la session (references/stockage.md, partie B, pas 11) ;
- empreintes de la copie, si elle a été faite.

Un test qui échoue : corriger la règle avec accord, et retirer la mention du CLAUDE.md tant que le test n'a pas réussi. Un test reporté va dans « À confirmer ».

Appelé par `architecte-consignes`, ne pas ouvrir d'autre session : les tests se font dans la nouvelle session de sa recette (son étape 6).
- Avant de revenir à son étape 6, noter dans `_entretien-environnement.md` : sous « Étape en cours », « 10, tests dans la session de recette » ; sous « Tests », les tests retenus et chaque ligne du `CLAUDE.md` qui attend son test.
- Préparer avec le participant la question de la pièce (début de cette étape), sans l'écrire nulle part.
- Inscrire dans `_entretien-claude-md.md`, sous « Étape en cours » et, tant que les tests ne sont pas faits, sous « À confirmer » : « Tests de l'environnement de base : dans la session de recette, poser d'abord la question de la pièce préparée avec le participant, puis les questions de recette, puis taper `/architecte-consignes:environnement-de-base`, et « reprendre ». » Si les tests comprennent Chrome, ajouter : « En terminal, ouvrir cette session par `claude --chrome --permission-mode default`. »
- Dans cette session, ce skill reprend son brouillon (E8), fait l'étape 10 avec les sections « Test » des références, écrit les lignes en attente après leur test et l'accord, puis finit l'étape 11. Il dit enfin : « Revenez dans la session précédente et donnez-y ces résultats pour la suite de l'étape 6. »

### Étape 11. Remettre

- Récapitulatif :
  - ce qui est bloqué par les réglages de Claude Code ;
  - ce qui demande une confirmation (règles ask posées : `.obsidian` si le coffre est la racine de la session, création et copie sur le stockage, outils de formulaire de Chrome), avec sa limite et l'état de son test ;
  - Obsidian : le coffre retenu, le chemin de l'accueil (brouillon, « Obsidian ») et, pour un coffre de sous-dossier, ce qu'il ne montre pas ;
  - ce qui est réglé par le participant sur claude.ai ;
  - ce qui reste une consigne (navigateur, agenda, Cowork) ;
  - ce qui est « à confirmer », écrit en entier.
- Lancé seul : inscrire le statut « terminé » au brouillon, puis proposer de le supprimer, de le ranger aux archives ou de le garder ; ne rien faire sans réponse. Sans `CLAUDE.md` maître, recommander de le garder jusqu'au passage de `/architecte-consignes` : il porte les lignes à reprendre (étape 9).
- Sans `CLAUDE.md` maître, proposer `/architecte-consignes` pour le classement, et dire : « Au lancement, demandez-lui de reprendre les lignes notées dans `_entretien-environnement.md`, sous « À confirmer ». »
- Appelé par `architecte-consignes` :
  - dans sa session : récapitulatif, tests notés « à faire dans la session de recette » ; statut « en cours (tests à faire à l'étape 6 de architecte-consignes) » ; puis revenir à son étape 6 ;
  - dans la session de recette, après les tests : statut « terminé » ; dans `_entretien-claude-md.md`, « Environnement de base : fait », et la ligne des tests retirée de « À confirmer ». Ne pas proposer le sort de `_entretien-environnement.md` : son étape 6 y lit les résultats, et son étape 7 ses points « à confirmer ». Dire : « Le sort de ce brouillon se décidera à l'étape 7 de architecte-consignes, après le récapitulatif. »

## Réglages proposés

Le modèle [modeles/modele-settings-environnement.json](modeles/modele-settings-environnement.json) contient toutes les règles proposées. Ne garder que celles des éléments installés et des connecteurs relevés (étape 9).

- **Trois formes par outil de connecteur.** Le nom exact relevé à l'étape 1 (`mcp__<identifiant>__<outil>`, à ajouter en séance), le motif en forme d'identifiant `mcp__*-*-*-*-*__<outil>`, et la forme du terminal `mcp__claude_ai_*__<outil>`. Le motif en forme d'identifiant vise tout nom de serveur qui contient au moins quatre tirets, pas seulement un identifiant de connecteur : ne jamais le présenter comme un contrôle d'identifiant. Vérifié par l'essai 2 sur un poste Windows ; couverture d'un identifiant renouvelé : déduite, non testée. Ces motifs visent le nom complet : `reply` ne vise pas `reply_to_board_thread`.
- **Ne jamais écrire `mcp__*__<outil>`** : ce motif retire aussi `mcp__ccd_session_mgmt__send_message`, la messagerie entre les sessions de l'utilisateur.
- **Messagerie, en deny.** Gmail : `send_message`, `reply`, `forward`. Microsoft 365 : `outlook_send_mail`, `outlook_forward_mail`, `outlook_send_draft`, `outlook_set_vacation`, `outlook_create_filter`, et les outils d'envoi de Teams.
- **Stockage.** Drive, en deny : `trash_file`, `share_file`, `request_access`, `update_file`, qui déplace et renomme (une modification en ligne, le participant la fait lui-même) ; en confirmation : `create_file`, `copy_file`. Microsoft 365 (outils `sharepoint_…`, valables aussi pour OneDrive) : suppression, déplacement, renommage et remplacement du contenu en deny ; création d'un fichier ou d'un dossier, copie et dépôt en confirmation.
- **Chrome et Obsidian.** Étapes 8 et 4 ci-dessus. Une règle `Write(...)` n'est pas appliquée : `Edit` couvre la création.
- **Limites à dire.** Les noms Microsoft 365 sont publiés par Anthropic mais non observés : les comparer au relevé. Un motif peut aussi bloquer un outil de même nom d'un autre service, par exemple sur un autre serveur à quatre tirets ou plus pour le motif en forme d'identifiant : cet effet de bord bloque en trop. Un outil dont le nom n'a pas la forme de ces motifs (autre forme d'identifiant, serveur de plugin ou serveur local, autre préfixe Chrome, nom Microsoft 365 différent) n'est couvert que par son nom exact relevé : seul le test de l'étape 10 montre qu'un outil est couvert. Ces règles valent pour Claude Code, dans une session ouverte dans ce dossier ; ni le navigateur ni Cowork ne sont couverts. Effet d'une confirmation sur un outil de connecteur ou de Chrome : documenté, mais non testé lors des essais du 25/11/2026 ; le dire ainsi.

## Fichiers de ce skill

- [references/obsidian.md](references/obsidian.md) : installer Obsidian, ouvrir le dossier comme coffre, accueil et note d'essai (étape 4).
- [references/stockage.md](references/stockage.md) : partie A, dossier de travail (étape 3) ; partie B, récupérer des dossiers (étape 5) ; partie C, stockage en ligne connecté (étape 7).
- [references/empreintes.md](references/empreintes.md) : commandes du contrôle des copies par empreintes (étapes 5 et 10).
- [references/messagerie.md](references/messagerie.md) : Gmail et Outlook en brouillons seulement (étape 6).
- [references/chrome.md](references/chrome.md) : Claude in Chrome (étape 8).
- [modeles/modele-settings-environnement.json](modeles/modele-settings-environnement.json) : règles proposées pour `.claude/settings.json` (étape 9).
- [modeles/modele-accueil.md](modeles/modele-accueil.md) : modèle de la note `Accueil.md` (étape 4).
- Skill voisin : [../architecte-consignes/SKILL.md](../architecte-consignes/SKILL.md), table « Mentions au maître » ; [../architecte-consignes/references/mecanismes.md](../architecte-consignes/references/mecanismes.md) §16, faits vérifiés.

Dans les références, un chemin `modeles/…` part du dossier de ce skill ; un renvoi « mecanismes.md §n » vise `../architecte-consignes/references/mecanismes.md`.
