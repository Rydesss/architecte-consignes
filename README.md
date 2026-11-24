# Architecte consignes

Un plugin pour Claude, en français, qui construit avec vous, au fil d'un entretien guidé, le `CLAUDE.md` de votre espace de travail : le fichier de consignes que Claude Code lit au lancement de chaque session. Il convient à un projet de code comme à un dossier d'entreprise ou à un dossier personnel.

Projet indépendant, non affilié à Anthropic.

## Où l'utiliser

Le plugin crée des dossiers et des fichiers. Il lui faut donc une session qui lit et écrit dans votre dossier :

- **Claude Code** : l'onglet Code de l'application de bureau Claude, un terminal ou un éditeur. C'est l'usage prévu ; il a été essayé le 24/11/2026 dans l'onglet Code.
- **Cowork** : il doit fonctionner, mais cet usage n'a pas encore été essayé.
- **Une conversation ou un projet claude.ai** : Claude n'y a pas accès à vos dossiers. Il ne peut ni les lire, ni créer vos fichiers ; il vous en donne seulement le texte à copier. Pour qu'il les crée lui-même, lancez-le dans Claude Code ou dans Cowork.

## Ce qu'il fait

- **Il commence par quatre questions de cadrage, puis lit votre dossier sans modifier vos fichiers.** Il ne pose ensuite que les questions auxquelles vos fichiers ne répondent pas, quatre au plus par message.
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

## Les trois niveaux

Pour chaque action sensible, l'entretien vous propose l'un de ces trois niveaux et vous les explique avant la première question :

- **Bloqué** : Claude Code refuse l'action, même si vous la demandez. Si vous en avez besoin, vous la faites vous-même.
- **Confirmation** : Claude Code vous affiche une demande d'autorisation avant chaque action de ce type, et vous acceptez ou vous refusez. C'est la valeur proposée par défaut pour supprimer, déplacer ou renommer un fichier.
- **Consigne** : Claude s'engage à la suivre, mais sans garantie.

Pourquoi une confirmation, si Claude demande déjà ? Selon le mode de permission de la session, Claude Code demande avant la plupart des actions (mode manuel), ou décide seul pour beaucoup d'entre elles (mode auto, le mode par défaut dans un terminal). Une confirmation garde la demande d'autorisation pour les actions que vous avez choisies, quel que soit le mode. Ses limites sont dites pendant l'entretien. Par exemple, une règle sur les commandes ne couvre pas un script, et elle ne couvre pas d'office l'outil qui tape des commandes dans le terminal de l'application : l'entretien propose de le régler à part.

## Ce que contient le plugin

Uniquement des instructions et des modèles en Markdown, plus un modèle de réglages en JSON. Le plugin ne contient ni hook, ni script, ni serveur MCP, ni programme.

```text
.claude-plugin/plugin.json        description du plugin
.claude-plugin/marketplace.json   permet d'ajouter ce dépôt comme marketplace
skills/architecte-consignes/      le skill : SKILL.md, references/, modeles/
```

## Installer

**Claude Code** (terminal) :

```text
claude plugin marketplace add Rydesss/architecte-consignes
claude plugin install architecte-consignes@architecte-consignes
```

**Application de bureau, onglet Code** (session locale ou SSH) :
1. Ajoutez d'abord la marketplace avec la première commande ci-dessus. Le terminal et les sessions locales de l'application lisent les mêmes réglages.
2. Cliquez ensuite sur « + », puis « Add plugins » (ou « Plugins », puis « Browse plugins »).
3. Installez `architecte-consignes`.

**Cowork, et claude.ai en repli** :
1. Ouvrez « Plugins » dans la barre latérale. Sur les versions précédentes, c'est « Customize », puis « Plugins ».
2. Cliquez sur « Add ».
3. Choisissez :
   - « Add marketplace », avec `Rydesss/architecte-consignes` ;
   - ou « Upload plugin », avec l'archive `architecte-consignes-<version>.zip` de la page « Releases » du dépôt.

Les skills y demandent l'exécution de code : activez « Code execution and file creation » dans les réglages (Settings, puis Capabilities). Sur Team et Enterprise, c'est le propriétaire de l'organisation qui l'active. La disponibilité des plugins selon l'offre évolue en ce moment : vérifiez-la dans l'aide de Claude.

Les noms des menus peuvent changer d'une version à l'autre de l'application.

## Lancer l'entretien

1. Prenez un dossier de test, ou une copie sauvegardée de votre dossier. Retirez-en d'abord les fichiers de mots de passe, de banque et de données personnelles.
2. Ouvrez une session Claude Code à la racine de ce dossier.
3. Lancez le skill :
   - tapez `/architecte-consignes:architecte-consignes` ;
   - ou simplement `/architecte-consignes`, si aucune autre commande ne porte ce nom ;
   - ou demandez « crée le CLAUDE.md de ce dossier », ou « audite mes consignes ».
4. Répondez aux quatre questions de cadrage, puis suivez l'entretien.

Si vous aviez copié le skill seul dans `~/.claude/skills/architecte-consignes`, ou dans le dossier `.claude/skills/` d'un projet, supprimez cette copie une fois le plugin installé. Sinon, `/architecte-consignes` lance l'ancienne copie.

## Ce qu'il ne fait pas

- Une consigne n'est jamais une garantie : Claude peut ne pas la suivre. Seuls les réglages sont appliqués par l'outil, avec les limites que l'entretien vous détaille.
- Il n'envoie et ne publie rien : plan, rapport et récapitulatif restent dans la conversation.
- Il n'ouvre pas vos fichiers de secrets. Il les signale et vous propose de les sortir du dossier.
- Il ne supprime aucun de vos fichiers. Un fichier inutile va aux archives, et la suppression reste votre décision. Il peut seulement supprimer, avec votre autorisation, son brouillon et le fichier de test qu'il a créés.

## Licence

MIT : voir le fichier `LICENSE`.

## Versions

- 1.1.1 (24/11/2026) : corrections issues de l'essai réel dans l'onglet Code.
  - L'accès aux fichiers est annoncé dès le départ.
  - Les trois niveaux (bloqué, confirmation, consigne) sont expliqués en mots simples.
  - La confirmation devient la valeur par défaut pour supprimer, déplacer ou renommer.
  - L'outil qui tape des commandes dans le terminal de l'application est pris en compte.
  - Les outils qui ne transmettent qu'à vos propres sessions ou appareils sont distingués des outils d'envoi vers l'extérieur.
- 1.1.0 (24/11/2026) : première version publiée sous forme de plugin.
  - La méthode a été vérifiée sur des scénarios fictifs simulés.
  - Les faits sur le fonctionnement de Claude ont été vérifiés dans la documentation officielle le 22/11/2026, et complétés le 24/11/2026 pour les réglages. Cette documentation évolue vite.
