# Architecte consignes

Un plugin pour Claude, en français, qui construit avec vous, au fil d'un entretien guidé, le `CLAUDE.md` de votre espace de travail : le fichier de consignes que Claude Code lit au lancement de chaque session. Il convient à un projet de code comme à un dossier d'entreprise ou à un dossier personnel.

Depuis la version 1.2.0, il peut aussi préparer l'environnement de base de ce dossier : Obsidian, copie de vos dossiers Google Drive ou OneDrive, messagerie en brouillons seulement, stockage en ligne connecté et Claude in Chrome.

Projet indépendant, non affilié à Anthropic.

## Où l'utiliser

Le plugin crée des dossiers et des fichiers. Il lui faut donc une session qui lit et écrit dans votre dossier :

- **Claude Code** : l'onglet Code de l'application de bureau Claude, un terminal ou un éditeur. C'est l'usage prévu ; l'entretien y a été essayé le 24/11/2026, dans l'onglet Code.
- **Cowork** : l'entretien devrait fonctionner, mais cet usage n'a pas encore été essayé.
- **Une conversation ou un projet claude.ai** : Claude n'y a pas accès à vos dossiers. Il ne peut ni les lire, ni créer vos fichiers ; il vous en donne seulement le texte à copier. Pour qu'il les crée lui-même, lancez-le dans Claude Code ou dans Cowork.

La préparation de l'environnement de base installe et copie sur votre ordinateur. Elle ne fonctionne que dans Claude Code (onglet Code ou terminal) : pas dans Cowork, ni sur claude.ai.

## Ce qu'il fait

### Deux skills, une seule entrée

Le plugin contient deux skills. Un skill est une procédure que Claude suit pas à pas.

- **`architecte-consignes`** mène l'entretien qui produit vos consignes. C'est l'entrée habituelle : `/architecte-consignes`.
- **`environnement-de-base`** prépare les outils autour de votre dossier. L'entretien vous le propose après avoir lu votre dossier : tout, une partie ou rien. Il se lance aussi seul : `/architecte-consignes:environnement-de-base`.

### L'entretien

- **Il commence par quatre questions de cadrage, puis lit votre dossier sans modifier vos fichiers.** Il ne pose ensuite que les questions auxquelles vos fichiers ne répondent pas, quatre au plus par message.
- **Il signale un dossier de travail qui semble synchronisé** par OneDrive, Google Drive ou iCloud. C'est un indice, qu'il vérifie avec vous.
- **Il n'écrit qu'après votre accord sur un plan de fichiers.** Seule exception : un brouillon `_entretien-claude-md.md`, qui garde vos réponses pour reprendre après une interruption. C'est une règle que Claude suit, pas un verrou de l'outil.
- **Il produit :**
  - un `CLAUDE.md` maître court ;
  - des fichiers satellites, que le `CLAUDE.md` maître cite et fait lire au bon moment ;
  - si besoin, des règles par dossier et des skills pour vos tâches récurrentes ;
  - avec Claude Code, des réglages `.claude/settings.json` qui font appliquer vos choix par l'outil lui-même (voir « Les trois niveaux ») ;
  - à votre demande, un plan d'arborescence.
- **Il contrôle le résultat** avec une grille, puis vous propose des questions de recette à poser dans une nouvelle session.
- **Il sait aussi auditer des consignes existantes** (mode « audit seulement ») : rapport d'abord, corrections ensuite, lot par lot et avec votre accord.
- **Deux versions** : complète (30 à 60 minutes) ou minimale (environ 15 minutes pour une création). Ces durées sont estimées, pas mesurées.

### L'environnement de base

Un connecteur relie Claude à l'un de vos comptes en ligne, par exemple votre messagerie. Vous choisissez les éléments voulus :

- **Obsidian** (recommandé) : un logiciel gratuit qui affiche les fichiers texte de votre dossier comme des notes reliées entre elles. Claude vous propose de l'installer (sur Mac, seulement si Homebrew est déjà présent) ; sinon, ou si l'installation échoue, vous le téléchargez vous-même sur obsidian.md/download. Vous ouvrez vous-même votre dossier dans Obsidian. Une note `Accueil.md` liste vos dossiers et leur rôle.
- **Vos dossiers Google Drive ou OneDrive**, copiés dans votre dossier de travail, jamais déplacés. Chaque fichier copié est vérifié.
- **Gmail ou Outlook en brouillons seulement** : Claude prépare des brouillons dans votre boîte. Dans les sessions Claude Code ouvertes sur ce dossier, l'envoi, la réponse et le transfert sont bloqués par les réglages pour le connecteur de messagerie. Essayé avec Gmail, dans l'onglet Code sous Windows ; Outlook, le terminal et le Mac ne le sont pas encore : Claude vérifie le blocage en séance, par la liste de ses outils. Dans le navigateur, l'interdiction d'envoyer reste une consigne.
- **Google Drive ou OneDrive connecté**, pour chercher et lire un document. La mise à la corbeille dans Google Drive est bloquée par les réglages pour le connecteur (essayé dans l'onglet Code sous Windows). Le partage, le déplacement et le renommage dans Drive, et la suppression, le déplacement et le renommage dans OneDrive, sont réglés de même, sans essai à ce jour : Claude les vérifie en séance.
- **Claude in Chrome** : l'extension d'Anthropic qui permet à Claude de lire et d'agir dans votre navigateur Google Chrome. Une extension est un petit module ajouté au navigateur. L'outil qui exécute du code dans une page est bloqué, pour cet outil seulement (essayé dans l'onglet Code sous Windows). Les outils qui remplissent un formulaire ou envoient un fichier reçoivent une règle de confirmation, pas encore essayée. Claude peut toujours cliquer et taper dans une page.

Rien ne change avant votre accord sur un plan d'installation : c'est une règle que Claude suit, pas un verrou de l'outil ; en mode Manual, chaque commande qui modifie vous est en plus soumise. Vous faites vous-même ce qui engage vos comptes : vous connecter, saisir vos mots de passe, accepter des conditions, régler les permissions sur claude.ai, installer l'extension. Le détail est dans le [mode d'emploi](MODE-EMPLOI.md), section 6.

## Les trois niveaux

Pour chaque action sensible, l'entretien vous propose l'un de ces trois niveaux et vous les explique avant la première question :

- **Bloqué** : Claude Code refuse l'action, même si vous la demandez. Si vous en avez besoin, vous la faites vous-même.
- **Confirmation** : Claude Code vous affiche une demande d'autorisation avant chaque action de ce type, et vous acceptez ou vous refusez. C'est la valeur proposée par défaut pour supprimer, déplacer ou renommer un fichier.
- **Consigne** : Claude s'engage à la suivre, mais sans garantie.

Pourquoi une confirmation, si Claude demande déjà ? Selon le mode de permission de la session, Claude Code demande avant la plupart des actions (mode manuel), ou décide seul pour beaucoup d'entre elles (mode auto, le mode par défaut dans un terminal). Une confirmation garde la demande d'autorisation pour les actions que vous avez choisies, quel que soit le mode. Ses limites sont dites pendant l'entretien. Par exemple, une règle sur les commandes ne couvre pas un script, et elle ne couvre pas d'office l'outil qui tape des commandes dans le terminal de l'application : l'entretien propose de le régler à part.

## Ce que contient le plugin

Uniquement des instructions et des modèles en Markdown, plus deux modèles de réglages en JSON. Le plugin ne contient ni hook, ni script, ni serveur MCP, ni programme.

Pour l'environnement de base, Claude lance des commandes de votre système : installation d'Obsidian, copie de dossiers. En mode de permission **Manual** (sélecteur sous la zone de saisie de l'onglet Code ; voir le mode d'emploi, section 4), chacune vous est soumise par une demande d'autorisation. En mode auto, une commande peut passer sans demande d'autorisation : Claude vous montre alors la commande et demande votre accord dans la conversation. C'est une consigne, pas un verrou.

```text
.claude-plugin/plugin.json        description du plugin
.claude-plugin/marketplace.json   permet d'ajouter ce dépôt comme marketplace
skills/architecte-consignes/      l'entretien : SKILL.md, references/, modeles/
skills/environnement-de-base/     l'environnement de base : SKILL.md, references/, modeles/
```

## Installer

Le pas à pas complet, pour Windows et pour Mac, est dans le **[mode d'emploi](MODE-EMPLOI.md)**. En bref :

**Depuis l'application** (Windows et Mac) :
1. Ouvrez **Customize**, puis **Plugins**, ou directement **Plugins** dans la barre latérale.
2. Cliquez sur **Add**, puis sur **Add marketplace**, et saisissez `Rydesss/architecte-consignes`.
3. Dans l'onglet **Discover**, choisissez **architecte-consignes**, puis cliquez sur **Add** (ou **Install**).

Le plugin est alors lié à votre compte. Cowork le charge à la tâche suivante. Dans l'onglet Code, il se télécharge au démarrage d'une nouvelle session ; il faut Claude Code 2.1.273 ou plus récent.

**Avec le terminal**, pour l'onglet Code et le terminal seulement :

```text
claude plugin marketplace add Rydesss/architecte-consignes
claude plugin install architecte-consignes@architecte-consignes
```

Les noms des menus peuvent changer d'une version à l'autre de l'application.

## Lancer l'entretien

1. Prenez un dossier de test, ou une copie sauvegardée de votre dossier. Retirez-en d'abord les fichiers de mots de passe, de banque et de données personnelles.
2. Ouvrez une session Claude Code à la racine de ce dossier.
3. Lancez le skill :
   - tapez `/architecte-consignes:architecte-consignes` ;
   - ou simplement `/architecte-consignes`, si aucune autre commande ne porte ce nom ;
   - ou demandez « crée le CLAUDE.md de ce dossier », ou « audite mes consignes ».
4. Répondez aux quatre questions de cadrage, puis suivez l'entretien.

Pour préparer seulement l'environnement de base, ouvrez de même une session Claude Code sur votre dossier, puis tapez `/architecte-consignes:environnement-de-base`.

Si vous aviez copié le skill seul dans `~/.claude/skills/architecte-consignes`, ou dans le dossier `.claude/skills/` d'un projet, supprimez cette copie une fois le plugin installé. Sinon, `/architecte-consignes` lance l'ancienne copie.

## Ce qu'il ne fait pas

- Une consigne n'est jamais une garantie : Claude peut ne pas la suivre. Seuls les réglages sont appliqués par l'outil, avec les limites que l'entretien vous détaille.
- Il n'envoie et ne publie rien, même pour un essai : plan, rapport et récapitulatif restent dans la conversation. L'essai de la messagerie crée un simple brouillon, que vous supprimez vous-même.
- Il ne se connecte à aucun de vos comptes, ne saisit aucun mot de passe et n'accepte aucune condition à votre place.
- Il ne déplace et ne supprime rien dans Google Drive ou OneDrive : il copie, et l'original reste en place.
- Il ne modifie pas les réglages de sécurité de votre ordinateur.
- Il n'ouvre pas vos fichiers de secrets. Il les signale et vous propose de les sortir du dossier.
- Il ne supprime aucun de vos fichiers. Un fichier inutile va aux archives, et la suppression reste votre décision. Il peut seulement supprimer, avec votre autorisation, ses brouillons et les fichiers de test qu'il a créés.

## Licence

MIT : voir le fichier `LICENSE`.

## Versions

- 1.2.0 (25/11/2026) : préparation de l'environnement de base.
  - Ajouté : un second skill, `environnement-de-base`, pour Obsidian, la copie de dossiers depuis Google Drive ou OneDrive, Gmail ou Outlook en brouillons seulement, Google Drive ou OneDrive connecté pour chercher et lire, et Claude in Chrome.
  - Une seule entrée : l'entretien `/architecte-consignes` propose de préparer l'environnement (tout, une partie ou rien). Le skill se lance aussi seul, par `/architecte-consignes:environnement-de-base`.
  - L'entretien signale un dossier de travail qui semble synchronisé (OneDrive, Google Drive, iCloud).
  - Trois mentions de plus pour le `CLAUDE.md` : messagerie en brouillons seulement, stockage en ligne, Claude in Chrome.
  - Mode d'emploi : nouvelle section « Préparer l'environnement de base ».
  - Essayé le 25/11/2026, dans l'onglet Code sous Windows : les règles de blocage du fichier `.claude/settings.json`. Dans une nouvelle session, Claude ne voyait plus l'envoi, la réponse ni le transfert de Gmail, ni la mise à la corbeille de Google Drive, ni l'outil de Claude in Chrome qui exécute du code dans une page. Les brouillons Gmail, la recherche et la copie dans Drive, et les autres outils de Chrome restaient disponibles.
  - Un second essai a retenu une écriture des règles qui ne retire pas, en plus, la messagerie entre vos propres sessions de Claude. Elle a été vérifiée sur un seul poste Windows. Elle vise tout service dont le nom technique contient au moins quatre tirets : ce n'est pas un contrôle du connecteur. Elle peut donc bloquer en trop un outil de même nom d'un autre service de ce type. Qu'elle vaille encore si l'application change le nom technique du connecteur est déduit, pas essayé.
  - Lu sans être appelé : la description des outils Drive qui déplacent, renomment, partagent ou demandent l'accès à un fichier.
  - Pas encore essayé : le Mac, Outlook et Microsoft 365, Cowork, l'effet d'une règle de confirmation, la création réelle d'un brouillon, et le déroulé complet du nouveau skill (installation d'Obsidian, copie, connexion des comptes).
- 1.1.2 (25/11/2026) : corrections issues du second essai réel, et mode d'emploi pour Windows et Mac (`MODE-EMPLOI.md`).
  - Les services pas encore connectés sont relevés ; le `CLAUDE.md` ne nomme que les services réellement bloqués.
  - Un fichier de secrets que vous sortirez plus tard reçoit un blocage de lecture provisoire.
  - Les commandes réseau reçoivent une demande d'autorisation, aussi quand l'envoi est interdit.
  - Les mentions écrites dans le `CLAUDE.md` tiennent dans une seule table.
- 1.1.1 (24/11/2026) : corrections issues de l'essai réel dans l'onglet Code.
  - L'accès aux fichiers est annoncé dès le départ.
  - Les trois niveaux (bloqué, confirmation, consigne) sont expliqués en mots simples.
  - La confirmation devient la valeur par défaut pour supprimer, déplacer ou renommer.
  - L'outil qui tape des commandes dans le terminal de l'application est pris en compte.
  - Les outils qui ne transmettent qu'à vos propres sessions ou appareils sont distingués des outils d'envoi vers l'extérieur.
- 1.1.0 (24/11/2026) : première version publiée sous forme de plugin.
  - La méthode a été vérifiée sur des scénarios fictifs simulés.
  - Les faits sur le fonctionnement de Claude ont été vérifiés dans la documentation officielle le 22/11/2026, et complétés le 24/11/2026 pour les réglages. Cette documentation évolue vite.
