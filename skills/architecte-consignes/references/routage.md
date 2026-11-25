# Routage : quelle information va où

Table de décision de l'étape 3 (Proposer le plan de fichiers). Lire ce fichier pour classer chaque information recueillie, construire le plan de fichiers et annoncer ce qui sera chargé à chaque session. Les mécanismes cités renvoient à [mecanismes.md](mecanismes.md) (section entre parenthèses, par exemple « §6 ») ; ce qui n'y figure pas est dit « non vérifié ».

## 1. Principes

- Une information, un seul lieu. Les autres fichiers y renvoient par un pointeur, sans la reformuler.
- Choisir le lieu chargé le plus tard possible qui garantit encore la lecture au moment utile.
- Les lignes préremplies des modèles et les règles de `modeles/modele-settings.json` sont des propositions : n'en garder que celles qui répondent aux blocs C, F et G, jamais une règle contre une réponse.
- Un interdit appliqué par un réglage reste défini dans le réglage ; le maître le signale en une ligne de sa section « Interdits », phrase négative complète suivie de la mention que fixe SKILL.md, étape 5, « Mentions au maître » ; motif qui ne couvre pas tout l'objet : restreindre l'interdit, ou prendre la mention d'un ask si une règle `ask` couvre la forme restante (même table). Avec plusieurs agents, le CLAUDE.md voisin le dit dans sa section « Réglages appliqués par l'outil », réservée à ce que l'outil applique (`modeles/modele-CLAUDE-avec-AGENTS.md`).
- En refonte, chaque bloc de l'ancien fichier (`fichier:lignes`) reçoit une destination de la section 2, « archives », ou « écarté » avec sa raison ; une règle sans `paths` existante et conforme peut rester en place (section 2, Règle par chemin). Avec accord, l'ancien fichier de consignes se garde en copie `<NOM>.ancien-AAAA-MM-JJ.md`, nom jamais chargé, sauf sous `.claude/rules/` ou `~/.claude/rules/` : la copie d'une règle va hors de ce dossier (§1). Dans un dépôt git, un commit en tient lieu. La copie ne garde jamais la valeur d'un secret.
- Ne rien écrire hors du brouillon d'entretien avant qu'il porte « Plan validé : oui » (SKILL.md, règles 7 et 8).

## 2. Les destinations

Onze destinations, les mêmes dans tout le kit : maître ; satellite importé ; satellite à la demande ; règle par chemin ; CLAUDE.md de sous-dossier ; skill ; réglage (ou hook, option avancée) ; suivi ; mémoire automatique ; préférences personnelles (`CLAUDE.local.md` ou `~/.claude/CLAUDE.md`) ; nulle part.

### CLAUDE.md maître
- Y va, dans les sections de `modeles/modele-CLAUDE-projet.md` : identité de l'espace en une à trois phrases ; pointeur vers le suivi (« Avant d'agir ») ; pointeurs vers les sources de vérité (« Où trouver quoi ») ; façon de travailler ; règles courtes de classement et de nommage ; ton et mentions des documents destinés à des tiers (bloc D) ; accords préalables (« Demander mon accord avant de ») et interdits (« Interdits ») ; déclencheurs des procédures ; « Commandes et pièges », soit ce que Claude ne devinerait pas (bloc G) ; contrôle avant « terminé » (bloc E) ; clause des sessions sans surveillance, avec ses exceptions aux accords préalables (bloc G, G4b) ; règle d'entretien. Plusieurs agents : section 6.
- Documents destinés à des tiers : un seul lieu : en refonte, une règle sans `paths` existante qui le porte déjà (ci-dessous) ; sinon `consignes/conventions.md` s'il existe ; sinon la section du maître. L'autre lieu renvoie, sans reformuler.
- N'y va pas : état, historique, secret, description de l'arborescence, procédure détaillée, règle propre à un dossier.
- Chargement : au lancement de chaque session ; relu sur le disque et réinjecté après une compaction (§1, §7). Les sous-agents intégrés Explore, Plan et web-fetch, et ceux réglés avec `omitClaudeMd: true`, ne le reçoivent pas : une consigne critique pour un sous-agent se répète dans la demande qui lui est faite (§1).
- Coût : permanent, à chaque requête. Moins de 100 lignes visées, 200 au maximum (§5).

### Satellite importé (`@chemin`)
- Y va : un bloc cohérent dont chaque session a besoin et qui alourdirait le maître au-delà d'une quinzaine de lignes (contexte et vocabulaire, dans `consignes/contexte.md`).
- N'y va pas : ce qui ne sert qu'à certaines tâches ; le suivi ; une longue référence.
- Chargement : avec le fichier qui l'importe, donc à chaque session. Chemin relatif au fichier qui importe ; quatre sauts au plus ; sans effet dans un code span, dans un bloc de code ou si des guillemets entourent le chemin ; approbation demandée la première fois pour un import qui sort du dossier de travail (§3).
- Coût : permanent, comme le maître. Un import organise, il n'allège pas (§3).

### Satellite à la demande (pointeur et déclencheur)
- Y va : une référence utile pour une tâche précise (conventions ou sources détaillées, procédure ponctuelle, glossaire long).
- N'y va pas : ce qui doit être appliqué à coup sûr (import, règle par chemin ou réglage).
- Chargement : seulement si Claude suit la consigne et ouvre le fichier ; lecture non garantie (§3, §4). Forme : « Avant de [tâche], lire `chemin` ».
- Coût : à l'usage.

### Règle par chemin (`.claude/rules/<sujet>.md` avec `paths`)
- Y va : une règle propre à un dossier ou à un type de fichier, par exemple `tests/**/*` ou `*.{docx,xlsx}` (exemples fictifs ; en YAML, un motif qui commence par `*` ou `{` se met entre guillemets, sinon la règle peut se charger à chaque session, sans signal, §4). Modèle : `modeles/modele-regle-chemin.md`.
- N'y va pas : une règle générale ; une procédure en plusieurs étapes (skill).
- Chargement : quand Claude lit, écrit ou modifie un fichier visé ; après une compaction, seulement quand il en retouche un. Motifs relatifs au dossier qui contient `.claude` (pour une règle de `~/.claude/rules/`, au dossier de lancement) ; seul `paths` est lu dans le frontmatter ; au-delà d'une limite de caractères, seul le début est lu (§1, §4, §5, §7).
- Coût : à l'usage. Une règle sans `paths` se charge au lancement, comme le maître : elle découpe sans alléger. En refonte, une règle sans `paths` existante et conforme (ton des documents, par exemple) reste en place et reste le lieu unique de son sujet : ne pas la migrer pour sa seule forme ; la compter dans l'estimation (section 4).
- Au maître, dans « Procédures » : « Les règles propres à `[dossier]` se chargent seules quand un fichier de ce dossier est lu ou modifié (`.claude/rules/[sujet].md`). »

### CLAUDE.md de sous-dossier
- Y va : ce qui diffère du parent ou s'y ajoute, pour un sous-dossier qui forme un ensemble (un projet, un client) et peut être ouvert seul.
- N'y va pas : la copie des règles du parent ; une règle censée « annuler » celle du parent, car tout s'additionne, sans priorité (§2).
- Chargement : quand Claude lit, écrit ou modifie un fichier du sous-dossier, ou en lit un par une commande comme `cat` ou `head` (une commande shell quelconque ne suffit pas). Si la session est ouverte dans ce sous-dossier, il se charge au lancement, avec les CLAUDE.md des dossiers parents (§1) ; la session ne reçoit pas alors les réglages `.claude/settings.json` du parent (§6).
- Coût : à l'usage depuis la racine. Pour un type de fichier réparti dans plusieurs dossiers, préférer une règle par chemin.

### Skill (`.claude/skills/<nom>/SKILL.md`)
- Y va : une procédure récurrente en plusieurs étapes, validée au bloc E, y compris un déroulé proposé par Claude puis validé explicitement. Modèle : `modeles/modele-skill-procedure.md`.
- N'y va pas : une règle permanente (le corps n'est lu qu'à l'appel) ; les règles générales du maître, hormis au plus un rappel d'une ligne du garde-fou le plus critique, marqué « (rappel du maître) » ; une tâche faite une seule fois ; l'état.
- Chargement : nom visible en permanence, description si la place le permet ; corps à l'appel `/nom` ou quand Claude juge le skill utile ; fichiers annexes au besoin. Pour une procédure qui envoie, publie ou supprime : `disable-model-invocation: true` (Claude Code uniquement ; jamais dans un skill à importer sur claude.ai, dont il ferait échouer l'import). Après une compaction, seul le début peut survivre : règles essentielles en tête (§7, §11).
- Coût : faible (la description).

### Réglage (`.claude/settings.json` : `allow`, `ask`, `deny`)
- Y va : un interdit absolu exprimable en `Outil(spécificateur)` (`deny`), outil de connecteur compris (`mcp__<serveur>__<outil>`, §6) ; une action toujours soumise à accord (`ask`) ; une commande sûre et fréquente, nommément (`allow`).
- N'y va pas : une préférence de style ; une règle qui admet des exceptions ; une autorisation large.
- Portée : Claude Code seulement (dans Cowork et claude.ai, voir section 7). `.claude/settings.json` pour le projet, partagé ; `~/.claude/settings.json` pour tous les projets ; `.claude/settings.local.json` pour l'utilisateur seul dans ce projet. Le fichier du projet est lu depuis le dossier de travail de la session : lancer Claude à la racine, ou répéter les deny dans un sous-dossier ouvert seul. Les motifs `./` partent du dossier de lancement : les réécrire depuis ce sous-dossier (`Read(./clients/rh/**)` devient `Read(./rh/**)` dans `clients/`) ou en chemin absolu (`//c/…`), puis tester chacun sur un fichier factice dans une session ouverte au sous-dossier (§6).
- Chargement : appliqué par l'outil, quoi que décide Claude. Les listes de tous les fichiers s'additionnent ; évaluation deny, puis ask, puis allow ; un deny l'emporte sur tout allow (exception des mods : §6). Les `allow` de `~/.claude/settings.json` valent aussi pour les tâches programmées locales : n'y autoriser que les commandes nécessaires, nommément (§14). Une commande qui exécute du code du dépôt que la tâche modifie vaut un joker (déduction, §6 ; `controle-qualite.md` C16) : la laisser hors de l'`allow`, sinon statut « risque accepté » et mention au maître (section 5).
- Coût : rien à compter dans l'estimation.

### Hook (option avancée du réglage)
- Y va : un interdit absolu qu'aucune règle de permission n'exprime de façon fiable, ou un contrôle qui doit s'exécuter à chaque fois.
- N'y va pas : ce qu'un réglage couvre déjà ; un script que personne ne saura maintenir.
- Chargement : commande lancée par l'outil à un moment précis du cycle. Un hook PreToolUse qui sort avec le code 2 bloque l'appel, comme un deny (même exception pour les mods, §6) ; les règles deny et ask restent évaluées quel que soit le retour du hook, qui ne lève donc pas un deny (§6).
- Coût : non documenté dans `mecanismes.md`. Tutoriel hors kit : https://code.claude.com/docs/en/hooks-guide.

### Suivi
- Y va : tâches ouvertes, échéances, statuts, dates d'événements, décisions en attente, et la prochaine revue des consignes, en tâche datée (aucune consigne ne déclenche une action à une date). Modèle : `modeles/modele-suivi.md`.
- N'y va pas : une règle ; l'historique long, qui part dans un fichier d'archive lu à la demande.
- Chargement : à la demande, par le pointeur de la section « Avant d'agir » du maître (« L'état se lit dans `chemin du suivi` »). Ne jamais l'importer avec `@`.
- Coût : à l'usage, à chaque tâche qui suit le pointeur ; le garder court. Archiver l'historique au-delà de 100 lignes ou 15 Ko, seuil par défaut ajustable au bloc H.

### Mémoire automatique (Claude Code)
- Y va : ce que Claude apprend seul en travaillant ; il la tient lui-même et y range aussi des notes sur le travail en cours (§8).
- N'y va pas (choix du kit) : une règle, car sa portée est partielle (machine locale, absente des sous-agents) ; l'état de référence, qui va au suivi. « Retiens que… » écrit en mémoire automatique : pour une règle, dire « ajoute ceci au CLAUDE.md » (§8).
- Chargement : l'index `MEMORY.md` au démarrage, 200 premières lignes ou 25 premiers Ko ; les fiches à la demande. Portée : le dépôt git ou, hors git, la racine du projet ; un sous-dossier ouvert seul hors git a sa propre mémoire (§8).
- Coût : jusqu'à 200 lignes à chaque session, hors du plan de fichiers ; signaler à l'utilisateur les règles qui s'y trouvent.

### Préférences personnelles (`CLAUDE.local.md` ou `~/.claude/CLAUDE.md`)
- Y va : les préférences de l'utilisateur seul. `CLAUDE.local.md` pour ce projet ; `~/.claude/CLAUDE.md` pour tous les projets, limité aux blocs B, F et G, moins de 50 lignes (`modeles/modele-CLAUDE-utilisateur.md`).
- N'y va pas : une règle d'équipe ; un contenu propre à un projet dans `~/.claude/CLAUDE.md` ; un secret.
- Choix : en dossier versionné ou appelé à l'être, proposer la ligne `CLAUDE.local.*` dans `.gitignore`, qui exclut aussi sa copie de sauvegarde ; en dossier synchronisé sans exclusion possible, préférer `~/.claude/CLAUDE.md`. Si le plan ne prévoit qu'un `AGENTS.md`, sans CLAUDE.md qui l'importe, éviter `CLAUDE.local.md`, qui en arrêterait la lecture sans avertissement : préférer `~/.claude/CLAUDE.md`, ou régler « Project instructions » sur `claude-md-and-agents-md` (§9).
- Chargement : au lancement ; `CLAUDE.local.md` juste après le CLAUDE.md du même dossier (§1). Pour ses skills et plugins, Cowork ne lit pas `~/.claude` ; une session Cowork sur le bureau charge en revanche `~/.claude/CLAUDE.md` et `~/.claude/rules/`, sauf les imports qui sortent du dossier de la session et les liens symboliques (§12).
- Coût : permanent ; compter ces lignes dans le total.

### Nulle part
- Ne rien écrire pour : un secret ou un identifiant ; une donnée personnelle de tiers sans usage ; une information dérivable (Claude la trouverait dans les fichiers ; exception : les commandes retenues en G2, `controle-qualite.md` C10) ; une information périmée ; une préférence invérifiable (« être clair ») ; un comportement que Claude a déjà par défaut.
- Pour un secret : le ranger hors de l'espace de travail ; un réglage `deny` n'est qu'une protection de plus (§6, et section 5 ci-dessous). Un fichier de secrets trouvé dans l'espace est un constat bloquant (une gravité, pas un arrêt) : ne pas l'ouvrir, et proposer à l'utilisateur de le sortir lui-même de l'espace. S'il le garde : deny de lecture nommé (question C4) et statut « risque accepté ». S'il annonce qu'il le sortira lui-même et que le fichier est encore là quand les réglages s'écrivent : même deny, provisoire, dit au plan et au récapitulatif (« à garder si le fichier revient, ou à retirer après sa sortie », avec sa ligne au maître), statut « sortie annoncée, blocage provisoire ». Fichier d'environnement exigé par l'outillage d'un dossier de code : cas prévu par `controle-qualite.md` C21.
- Lister à l'utilisateur ce qui a été écarté, et pourquoi.

## 3. Arbre de décision

Pour chaque information, poser les questions dans l'ordre et s'arrêter à la première qui donne une destination.

1. **Faut-il l'écrire ?** Secret, dérivable, périmé, invérifiable ou déjà fait par défaut : nulle part. Sinon, question 2.
2. **Est-ce un état qui change ?** Tâche, statut, échéance, date d'événement, « depuis le », « actuellement » : suivi. Sinon, question 3.
3. **Est-ce un apprentissage de Claude plutôt qu'une décision de l'utilisateur ?** Oui, et l'utilisateur n'en fait pas une règle : mémoire automatique, rien à écrire. Sinon, question 4.
4. **Une exception est-elle acceptable ?** Non, avec Claude Code : réglage `deny` ou `ask` dans le fichier de la bonne portée, plus une ligne au maître qui dit que l'outil l'applique ; hook en option avancée. Non, avec Cowork ou claude.ai, pour l'outil d'un connecteur : permission réglée sur Blocked ou Needs approval (section 7). Si aucun réglage ne l'exprime, ou pour le reste dans Cowork ou claude.ai : maître, section « Interdits » ou « Demander mon accord avant de », présentée comme consigne seulement. Oui : question 5.
5. **Ne vaut-elle que pour l'utilisateur ?** Oui : préférences personnelles, `CLAUDE.local.md` (ce projet) ou `~/.claude/CLAUDE.md` (tous les projets). Non : question 6.
6. **Est-ce une procédure en plusieurs étapes ?** Récurrente : skill. Ponctuelle : satellite à la demande. Non : question 7.
7. **Ne concerne-t-elle qu'un dossier ou un type de fichier ?** Un type de fichier, ou plusieurs dossiers : règle par chemin. Un sous-dossier qui forme un ensemble : CLAUDE.md de sous-dossier. Non : question 8.
8. **Chaque session en a-t-elle besoin ?** Oui, en quelques lignes : maître. Oui, en un bloc de plus d'une quinzaine de lignes : satellite importé. Non : satellite à la demande, avec son déclencheur.

En cas d'hésitation entre deux destinations, présenter les deux à l'utilisateur avec leur coût et le laisser trancher.

## 4. Estimer le contexte chargé au démarrage

Présenter l'estimation avec le plan de fichiers, en lignes : l'utilisateur peut les compter lui-même.

Compter :
- les lignes du maître (`CLAUDE.md` ou `.claude/CLAUDE.md` du dossier de lancement), moins ses commentaires HTML de bloc hors bloc de code, retirés avant l'envoi (§5) ;
- les lignes de chaque fichier importé, imports en cascade compris ;
- les lignes des règles sans `paths`, dans `.claude/rules/` et `~/.claude/rules/` ;
- les autres fichiers chargés au lancement : le CLAUDE.md géré par l'organisation s'il existe (fichier, ou clé `claudeMd` des réglages gérés, sans fichier à lire), `CLAUDE.md` et `CLAUDE.local.md` des dossiers parents, `~/.claude/CLAUDE.md`, `CLAUDE.local.md` du projet (§1) ;
- à part : l'index `MEMORY.md`, jusqu'à 200 lignes ou 25 Ko, et le nom et la description de chaque skill.

Ne pas compter : satellites à la demande, règles avec `paths`, CLAUDE.md et CLAUDE.local.md de sous-dossiers, règles d'un `.claude/rules/` de sous-dossier, corps des skills, suivi. Les donner sur une ligne « chargé seulement à l'usage ». Si « Project instructions » vaut `managed-only`, le maître et ses imports ne se chargent pas au lancement (§9) : le dire avant de présenter le plan.

Repère du kit, et non limite de l'outil : si maître, imports et règles sans `paths` dépassent 200 lignes au total, revoir le routage.

Comptage : `wc -l fichier` (macOS, Linux, Git Bash) ou `(Get-Content fichier).Count` (PowerShell). La mesure réelle se fait ensuite avec `/context all`, qui liste les fichiers chargés au lancement (§10 ; dans l'onglet Code, non documenté, à vérifier dans l'application ; voir `controle-qualite.md`, tests de recette).

Présentation (exemple fictif) :

```text
Chargé à chaque session
  CLAUDE.md (maître)               68 lignes
  @consignes/contexte.md           17 lignes
  .claude/rules/ sans paths         0 ligne
  ~/.claude/CLAUDE.md              22 lignes
  Total                           107 lignes
  En plus : index de mémoire automatique (200 lignes au plus), description d'un skill
Chargé seulement à l'usage
  consignes/conventions.md         45 lignes   avant de nommer un document
  .claude/rules/tests.md           24 lignes   en touchant un fichier de tests/
  /revue-bibliographie             80 lignes   à l'appel
```

## 5. Réglages de base (`modeles/modele-settings.json`)

Claude Code seulement. Les règles du modèle sont des propositions (section 1) : présenter avec le plan de fichiers (étape 3) celles qui répondent aux blocs C, F et G, une par une, dans l'ordre du modèle : d'abord leur effet en mots simples (« suppression : demande d'autorisation à chaque fois », « lecture du `.env` : bloquée » ; sens de ces mots : `questionnaire.md`, « Conduite de l'entretien »), puis leur syntaxe exacte. Retirer, en le disant, une règle sans objet (`git push` sans git ni git prévu, règle `PowerShell` hors Windows) ou contraire à une réponse (F1 sans déplacer ni renommer). Suppression interdite en F2 (« impossible même si je le demande ») : `deny` de `Bash(rm *)` et `PowerShell(Remove-Item *)` à la place de leur `ask`, l'utilisateur supprimant alors lui-même ; retenue à la fois en F1 et en F2 : garder l'`ask`, sans `deny` ni ligne d'interdit au maître pour cette action, signalé au résumé F (`questionnaire.md`, bloc F). Motifs de chemin (type gitignore) : `./chemin` ou `chemin` depuis le dossier de lancement ; `/chemin` depuis le dossier de lancement dans `.claude/settings.json` et `.claude/settings.local.json`, mais depuis `~/.claude` dans `~/.claude/settings.json` ; `~/chemin` depuis le dossier personnel ; `//chemin` depuis la racine du disque ; `//c/…` pour un lecteur Windows. Une règle utilisateur valable dans tous les projets s'écrit donc en `//` ou en `~/` (§6).

| Règle du modèle | Liste | Effet |
|---|---|---|
| `Read(./.env)` | `deny` | Bloque la lecture du `.env` du dossier de lancement (mots de passe, clés d'accès) |
| `Read(./.env.*)` | `deny` | Même chose pour ses variantes au même niveau, comme `.env.local` |
| `Read(./**/.env)` | `deny` | Même chose pour un `.env` placé dans un sous-dossier, à tous les niveaux |
| `Read(./**/.env.*)` | `deny` | Même chose pour ses variantes dans les sous-dossiers |
| `Read(./secrets/**)` | `deny` | Bloque le contenu du dossier `secrets/` du dossier de lancement |
| `Read(./**/*.key)` | `deny` | Bloque les fichiers `.key`, à tous les niveaux |
| `Bash(rm *)` | `ask` | Demande avant une commande Bash qui commence par `rm` (macOS, Linux, Git Bash) |
| `Bash(mv *)` | `ask` | Même chose pour `mv` (déplacer, renommer) |
| `Bash(git push *)` | `ask` | Demande avant un `git push` lancé dans Bash |
| `Bash(curl *)` | `ask` | Demande avant une commande Bash qui commence par `curl` (échange de données avec Internet) ; à garder pour un envoi soumis à accord (F1) ou un interdit d'envoi (bloc F), en `deny` si l'utilisateur veut le blocage ; sinon, règle sans objet, à retirer en le disant |
| `Bash(wget *)` | `ask` | Même chose pour `wget` |
| `PowerShell(Remove-Item *)` | `ask` | Demande avant une commande PowerShell qui commence par `Remove-Item`, alias courants compris (liste non documentée, §6) ; Windows |
| `PowerShell(Move-Item *)` | `ask` | Même chose pour `Move-Item` (déplacer) |
| `PowerShell(Rename-Item *)` | `ask` | Même chose pour `Rename-Item` (renommer) |
| `PowerShell(git push *)` | `ask` | Demande avant un `git push` lancé dans PowerShell ; Windows |
| `PowerShell(Invoke-WebRequest *)` | `ask` | Comme `Bash(curl *)`, pour une commande PowerShell qui commence par `Invoke-WebRequest`, alias courants compris (liste non documentée, §6) ; Windows |
| `PowerShell(Invoke-RestMethod *)` | `ask` | Même chose pour `Invoke-RestMethod` |
| `mcp__terminal__run_in_terminal` | `ask` | Demande avant chaque commande que l'outil de terminal de l'application de bureau tape dans un onglet de l'utilisateur, hors des règles Bash et PowerShell (déduction) ; à garder dès qu'une commande est en `deny` ou en `ask`, si l'outil figure au relevé de l'étape 1 ou si l'espace peut être ouvert dans l'application de bureau (à confirmer) ; sinon, règle sans objet, à retirer en le disant ; effet et nom exact à vérifier dans l'application (§6) |

Les deux autres clés :
- `allow` reste vide. N'y ajouter que des commandes sûres et fréquentes, nommément ; jamais une autorisation large comme `Bash(*)`, ni un interpréteur comme `python -c *`, qui laisserait passer n'importe quel code, ni un préfixe comme `npx *` ou `docker exec *`, qui autorise toute commande lancée derrière (§6). Une commande nommée qui exécute du code du dépôt (script npm ou make, lanceur de tests) vaut un tel joker tant que ce code se modifie sans demande (mode Accept edits ou auto, `Edit` en allow ; déduction, §6 ; `controle-qualite.md` C16). Ces exclusions valent pour ce que Claude propose : une autorisation que l'utilisateur garde explicitement reste, sa réponse l'emportant (section 1), avec le statut « risque accepté » de C16. Pour une commande qui exécute du code du dépôt, le maître le dit alors dans « Commandes et pièges » (avec plusieurs agents, dans le CLAUDE.md voisin) : « Un script du dépôt modifié puis lancé par `[commande]` échappe aux deny de lecture et aux règles Bash (risque accepté). » Aucun `allow` ne doit permettre d'accomplir un interdit (`Bash(git add *)` face à « Ne jamais committer `.env` », C14). Dans un `.claude/settings.json` partagé, les `allow` attendent que le dossier soit approuvé ; les `deny` et `ask` s'appliquent tout de suite (§6).
- `$schema` permet à un éditeur de signaler une faute de syntaxe.

Limites à dire à l'utilisateur :
- Un deny de lecture couvre les outils Read, Grep et Glob (au mieux), les commandes de lecture Bash reconnues (`cat`, `head`, `tail`, `sed`, `tee`) et les redirections. Il ne couvre ni un `grep -r` lancé dans le dossier, ni un script qui ouvre le fichier lui-même. Par l'outil de terminal de l'application en confirmation, une lecture ne fait que demander une autorisation (déduction, §6) ; par PowerShell (`Get-Content`, `type`), l'effet n'est pas documenté : la recette le teste sur un fichier factice. Mention au maître : SKILL.md, étape 5, « Mentions au maître ». Un secret reste donc hors de l'espace de travail ; le deny n'est qu'une protection de plus (§6).
- Réglages lus depuis le dossier de travail de la session (section 2, Réglage). En terminal, `/status` (ligne « Setting sources ») ou `/permissions` montrent les réglages chargés, pas le chemin qu'une règle vise ; dans l'onglet Code, `/permissions` est indisponible. Tester donc chaque deny sur un fichier factice, dans une session ouverte au dossier voulu (§6, §10).
- Une règle Bash porte sur le texte de la commande, pas sur le programme : `Bash(rm *)` ne voit ni `bash -c 'rm …'`, ni `/bin/rm`, ni un script ; `Bash(git push *)` ne voit ni `git -C . push` ni `git -c … push` (§6). Une règle PowerShell couvre les alias courants de la cmdlet (`PowerShell(Get-ChildItem *)` vise aussi `gci`, `ls` et `dir` ; liste exacte non documentée) et ignore la casse (§6). C'est un filet, pas une frontière de sécurité.
- Sous Windows, donner à chaque règle Bash retenue (modèle ou bloc F) son équivalent PowerShell, par exemple `PowerShell(git push *)` pour `Bash(git push *)`, sans attendre de savoir quel outil Claude emploiera.
- Une commande peut aussi partir d'un outil autre que Bash et PowerShell, relevé à l'étape 1 : par exemple `mcp__terminal__run_in_terminal` dans l'application de bureau, qui tape une commande dans un onglet de terminal de l'utilisateur. Les règles `Bash(...)` et `PowerShell(...)` ne le visent pas (déduction : la documentation n'étend les règles Bash qu'à `Monitor`, §6). Dès qu'une commande est en `deny` ou en `ask` (suppression, déplacement, réseau), proposer un `ask` sur le nom complet de cet outil (règle du modèle pour l'outil de terminal), ou son `deny` si l'utilisateur le veut ; effet à vérifier dans l'application (§6). Mention au maître d'une commande, selon les règles de ces outils : SKILL.md, étape 5, « Mentions au maître » (la ligne qui correspond).
- Un interdit de branche (« Ne jamais pousser sur `main`. ») : demander si une confirmation suffit pour les formes que les motifs ne couvrent pas.
  - Oui : deny sur les formes nommées, `Bash(git push * main)`, `Bash(git push * main *)`, `Bash(git push *:main)`, `Bash(git push *:main *)`, `Bash(git push * +main)` et `Bash(git push * +main *)` (deux règles par forme, car un `*` final ne couvre la commande nue que s'il est le seul joker, §6), avec `Bash(git push *)` gardé en `ask` comme filet. Restent en simple confirmation : un push qui ne nomme pas `main`, lancé depuis `main` (`git push`, `git push origin`, `git push -u origin HEAD`) ; un push de toutes les branches (`--all`, `--mirror`) ; l'écriture `refs/heads/main`. Au maître : l'interdit suivi de la mention d'un ask, jamais de celle d'un deny (SKILL.md, étape 5, « Mentions au maître »).
  - Non : deny de `Bash(git push *)`, à la place de l'`ask` : toute commande qui commence par `git push` est refusée, quelle que soit la branche. Au maître : l'interdit suivi de la mention d'un deny (même table), les limites ci-dessous étant dites une fois à l'utilisateur.
  - Dans les deux cas : `git -C . push`, `git -c … push`, `bash -c` et un script restent hors d'atteinte de ces règles (§6) ; leur sort dépend du mode de permission et des autres règles. En mode auto, mode de départ en terminal et dans VS Code, le classifieur laisse passer par défaut un push vers toute branche du dépôt de travail, branche par défaut comprise, hors branche de déploiement comme `production` (§6). Le plan dit ces limites. Sous Windows, chaque règle a son équivalent `PowerShell(…)`. La protection complète de la branche relève de l'hébergeur git, hors de ce kit.
- Une règle `Edit(...)` couvre tous les outils intégrés qui modifient un fichier, dont Write : création et écrasement compris ; une règle `Write(...)` n'est pas appliquée. Un deny `Read(...)` bloque aussi Edit et Write sur le même chemin, création comprise. Son effet sur une commande PowerShell qui écrit (`Set-Content`) n'est pas documenté (§6).
- Avec Cowork ou claude.ai, deux réglages seulement sont documentés : la permission d'un outil de connecteur (Blocked, Needs approval, §12) et, dans Cowork, un deny de l'outil `Bash` ou `WebFetch` entier (réglage géré par l'organisation, §6 ; depuis les réglages utilisateur ou projet : non documenté, à vérifier dans l'application). Tout autre interdit reste une consigne (section 7).
- Tester un deny seulement sur un fichier factice créé pour le test, avec accord, puis supprimé sur proposition ; jamais sur un vrai secret ni sur un vrai document sensible (`controle-qualite.md`, tests de recette). Un deny de lecture se teste par Read puis, sous Windows, par `Get-Content` dans l'outil PowerShell. Un deny sur un nom d'outil (`WebFetch`, `WebSearch`, `Artifact`, `mcp__…`) se teste sans fichier : dans une nouvelle session, Claude ne doit plus voir l'outil (§6). Pour un serveur de `.mcp.json` encore non approuvé, l'absence de ses outils ne prouve pas le deny : noter alors ce deny « à vérifier », sans mention « bloqué » au maître, jusqu'à une session où le serveur est approuvé et ses outils absents. Pour écarter le serveur entier, proposer plutôt `disabledMcpjsonServers` dans `.claude/settings.json`, qui vaut dans tous les modes (§6). De même pour un serveur installé mais pas encore connecté (en attente d'authentification, celui d'un plugin par exemple) : son deny d'avance (`mcp__plugin_<plugin>_<serveur>__*` pour un serveur de plugin, §6) reste « à vérifier » : l'effet d'un deny écrit avant la connexion, une fois le serveur connecté, n'est pas documenté. Ce service va dans « à confirmer » du récapitulatif, avec la question de recette à reposer après sa connexion (mention au maître : SKILL.md, étape 5, « Mentions au maître »).

Ajouter ensuite les interdits du bloc F qui s'expriment en `Outil(spécificateur)`, par exemple `Read(./dossier-confidentiel/**)` ou `WebFetch(domain:example.com)` (exemples fictifs). Un outil de connecteur (MCP) se bloque en `deny` par son nom canonique, `mcp__<serveur>__<outil>` (`mcp__plugin_<plugin>_<serveur>__<outil>` pour un serveur de plugin, §6), sans parenthèses, par exemple l'outil d'envoi d'un connecteur de messagerie. Ce nom varie selon le connecteur et l'interface, et peut différer du libellé de la demande d'autorisation : demander à Claude le nom exact dans sa liste d'outils. Aucun avertissement ne signale un nom faux : ouvrir ensuite une nouvelle session et vérifier que Claude ne voit plus l'outil (§6). Un interdit d'envoi ou de sortie de texte bloque aussi, par leur nom seul, les autres outils relevés à l'étape 1 ou à la dernière reprise qui le permettent, par exemple `WebFetch`, `WebSearch` ou `Artifact`, sauf refus de l'utilisateur noté au résumé F. Les outils de l'application qui transmettent seulement aux sessions ou aux appareils de l'utilisateur (messagerie entre ses sessions, envoi d'un fichier à ses appareils, notification, lancement ou transfert de session, Remote Control ; écriture dans son seul compte claude.ai, `SendToProject` ou `SendToProjectContext` par exemple, sauf publication pour des tiers, dans un projet partagé par exemple) n'entrent dans le deny proposé que si l'interdit vise tout texte qui sort de l'ordinateur, ou si l'utilisateur le demande ; s'ils restent, le maître dit « les outils d'envoi vers l'extérieur », jamais « tous les outils d'envoi » ni « rien ne sort » (`questionnaire.md`, bloc F). Chaque outil bloqué disparaît alors de la liste de Claude pour toutes les tâches ; aucun de ces deny n'arrête une commande réseau lancée par Bash ou PowerShell (documenté pour `WebFetch` et Bash, déduction pour le reste : §6 ; `questionnaire.md`, bloc F). Pour ces commandes, proposer au moins la protection d'un accord : un `ask` par défaut, ou un `deny` si l'utilisateur le veut, sur `Bash(curl *)`, `Bash(wget *)`, `PowerShell(Invoke-WebRequest *)` et `PowerShell(Invoke-RestMethod *)` (tableau ci-dessus), en plus de la règle sur l'outil de terminal de l'application (limites ci-dessus). Mention au maître de ces commandes : SKILL.md, étape 5, « Mentions au maître », ligne « Commandes réseau » ; toute autre commande réseau, dont `curl.exe` lancé par PowerShell (règle non documentée, §6), reste une consigne (`questionnaire.md`, bloc F). Serveur installé mais pas encore connecté (en attente d'authentification) : deny d'avance par préfixe, « à vérifier » (dernier point des limites ci-dessus). Mention au maître des outils d'envoi bloqués : même table, ligne « Outils d'envoi vers l'extérieur bloqués ».

Fusion avec un fichier existant :
- Lire `.claude/settings.json` s'il existe, avant de proposer quoi que ce soit.
- Ajouter les règles manquantes aux listes `deny` et `ask`. Ne retirer, ne modifier ni ne réordonner aucune règle ni aucune clé existante, sauf un retrait ou une restriction acceptés par l'utilisateur (F4, point suivant).
- Signaler à l'utilisateur une règle existante qui contredit le plan (autorisation large, accès à un dossier secret) ; ne la retirer ni la modifier sans son accord. Un `deny` ajouté l'emporte de toute façon sur un `allow` (§6).
- Avant de modifier un fichier existant, en garder une copie `settings.ancien-AAAA-MM-JJ.json` hors de `.claude/` (qu'un tel nom ne soit jamais chargé n'est pas documenté), ou un commit dans un dépôt git. Montrer les différences avant d'écrire : le tableau du plan en tient lieu s'il liste chaque règle ajoutée ou retirée, et chaque clé ajoutée (`$schema` compris), et dit que rien d'autre ne change. Vérifier ensuite que le fichier reste du JSON valide, par exemple avec `Get-Content -Raw .claude/settings.json | ConvertFrom-Json` (PowerShell).
- Le maître signale chaque interdit appliqué ; avec plusieurs agents, c'est le CLAUDE.md voisin qui le dit, jamais `AGENTS.md`.
- `.claude/settings.local.json` : le relire et signaler les autorisations larges ou ponctuelles accumulées par « Oui, ne plus demander » à une commande ou à un domaine web (§6). Ne retirer ou restreindre que les règles approuvées une à une (réponse F4) ; un « je ne sais pas » ne vaut pas accord : « à confirmer ». Avant de retirer, garder une copie `settings.local.ancien-AAAA-MM-JJ.json` à l'emplacement validé au plan, hors de `.claude/`, et hors du dépôt ou exclue par `.gitignore` (`settings.local.ancien-*`), jetons remplacés par « [retiré] ». Avec accord, y ajouter un réglage valable pour l'utilisateur seul. Différences montrées avant d'écrire, JSON vérifié après. Si ces autorisations permettent d'écrire sans demande, dire à l'étape 1 que la lecture seule du skill ne repose plus que sur la consigne.

## 6. Cas : plusieurs agents

- `AGENTS.md` porte les règles communes : une règle valable pour tous les agents y va, à la place du maître (`modeles/modele-AGENTS.md`).
- Le `CLAUDE.md` voisin contient la ligne `@AGENTS.md` (`@../AGENTS.md` depuis `.claude/CLAUDE.md` ; jamais dans `CLAUDE.local.md`, personnel), puis les seules lignes qui touchent aux fonctions de Claude Code : imports de satellites, skills, réglages, commandes `/…`, mémoire (`modeles/modele-CLAUDE-avec-AGENTS.md`). L'import ne fait jamais lire `AGENTS.md` deux fois (§9).
- Si la portée d'une règle pour l'autre agent est inconnue, la demander au bloc concerné (« pour tous les agents, ou pour Claude seul ? ») au lieu de l'écarter.
- Raison : par défaut, Claude Code ne lit `AGENTS.md` de lui-même que s'il ne trouve ni `CLAUDE.md`, ni `.claude/CLAUDE.md`, ni `CLAUDE.local.md` dans le dossier de travail ou au-dessus ; `~/.claude/CLAUDE.md`, le CLAUDE.md géré par l'organisation et les règles de `.claude/rules/` ne comptent pas. Autre voie, après accord : régler « Project instructions » sur `claude-md-and-agents-md` (§9).
- Dans `AGENTS.md`, citer les satellites en pointeurs à la demande : la lecture des imports `@` par les autres agents n'est pas documentée ici.
- Un réglage de `.claude/settings.json` ne vaut que pour Claude Code. Pour un autre agent, l'interdit écrit dans `AGENTS.md` reste une consigne tant que cet agent n'est pas réglé de son côté. Prévenir que modifier `AGENTS.md` change aussi les consignes des autres agents.
- Ni lien symbolique sous Windows, ni seconde copie tenue à la main (§9) ; pour les autres agents, se reporter à leur documentation.
- Estimation : compter `AGENTS.md` comme un fichier importé.

## 7. Cas : Cowork ou projet claude.ai

Le rendu devient le texte des instructions du projet (`modeles/modele-instructions-projet.md`) et la liste des fichiers à mettre à disposition : fichiers du dossier du projet dans Cowork, fichiers de connaissance dans un projet claude.ai. Ce texte remplace le texte actuel des instructions du projet, sans s'y ajouter. Pour ses skills et plugins, Cowork ne lit pas `~/.claude` ; une session Cowork sur le bureau charge `~/.claude/CLAUDE.md` et `~/.claude/rules/`, mais sa lecture d'un CLAUDE.md de projet n'est pas documentée (§12). Mettre donc les règles dans les instructions du projet. Claude Code et Cowork sur le même dossier : le maître fait foi. Les instructions du projet reprennent les interdits et les accords préalables du maître, et ceux des règles par chemin et des CLAUDE.md de sous-dossier, en une section par dossier (« Fichiers [motif] » pour une règle par chemin qui vise un type de fichier ; tableau ci-dessous), plus la ligne « Avant toute tâche, lire `CLAUDE.md` » (lecture non garantie). Les skills importés gardent leurs propres garde-fous. Dans cette copie, la mention que porte une ligne du maître (SKILL.md, étape 5, « Mentions au maître ») tombe, sauf pour un outil de connecteur réglé dans Cowork (Blocked, Needs approval, §12) ou l'outil `Bash` ou `WebFetch` entier bloqué par l'organisation dans Cowork (§6) : la ligne prend alors la mention de `modeles/modele-instructions-projet.md`. Un réglage de `.claude/settings.json` ne vaut que pour Claude Code. La grille de `controle-qualite.md` vérifie que chaque interdit et chaque accord du système y a sa ligne, et C14 ces mentions. Copie signalée au plan et relue à chaque revue (SKILL.md, étape 0). Avant d'écarter du projet un fichier sensible, demander quelles tâches en dépendent et dire la conséquence : une tâche qui en a besoin le garde accessible, avec ses garde-fous de contenu.

| Destination dans Claude Code | Équivalent |
|---|---|
| Maître, satellite importé | Instructions du projet, en texte court |
| Satellite à la demande, suivi | Fichier du dossier du projet (Cowork) ou fichier de connaissance (claude.ai), cité dans les instructions avec son déclencheur |
| Règle par chemin, CLAUDE.md de sous-dossier | Aucun équivalent documenté : une section par dossier dans les instructions (« Fichiers [motif] » pour un type de fichier), avec ses interdits et ses accords ; le reste de ses consignes, là ou dans un fichier à la demande |
| Skill | Skill importé sur le compte claude.ai en dossier zippé (dossier au nom du skill, `SKILL.md` dedans ; marche à suivre : `mecanismes.md` §12), frontmatter limité à `name` et `description` (§11), exécution de code et création de fichiers activées ; Cowork charge les skills activés sur le compte (§12) |
| Réglage, hook | Outil de connecteur (envoi, partage, suppression) : permission réglée sur Blocked, ou sur Needs approval pour un accord, dans Personnaliser > Connecteurs > [connecteur] > Permissions (§12) ; au texte des instructions, la ligne suivie de la mention de `modeles/modele-instructions-projet.md`. Dans Cowork, un deny de l'outil `Bash` ou `WebFetch` entier (réglage géré par l'organisation, §6 ; depuis les réglages utilisateur ou projet : non documenté, à vérifier dans l'application). Pour le reste, aucun équivalent documenté : l'interdit reste une consigne ; le dire, et garder la main sur les actions engageantes |
| Mémoire automatique | Mémoire propre du projet Cowork ; fonctionnement non détaillé dans `mecanismes.md` |
| `~/.claude/CLAUDE.md` | Chargé par une session Cowork sur le bureau, sauf les imports qui sortent du dossier de la session et les liens symboliques (§12) : ne pas en recopier les préférences dans les instructions d'un projet Cowork, ce qui ferait un doublon, sauf si ce fichier est un lien symbolique ; pour un projet claude.ai, les y reporter |

Estimation : les lignes du texte des instructions. Le chargement progressif des skills (§11) n'est décrit que pour Claude Code, celui des fichiers du projet ou de connaissance pas du tout : « non vérifié ». Aucun seuil documenté pour les instructions ; repère du kit : partie 1 sous 60 lignes (`modeles/modele-instructions-projet.md`).
